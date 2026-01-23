---
title: What's Coming in SHACL 1.2 Core (Part 1)
source: https://ontologist.substack.com/p/whats-coming-in-shacl-12-core-part?publication_id=1877971&post_id=181248315&isFreemail=true&r=7br8e&triedRedirect=true
author:
  - "[[Kurt Cagle]]"
published: 2025-12-12
created: 2025-12-13
description: A sneak peak into the constraint language.
tags:
  - clippings
  - SHACL
---
### A sneak peak into the constraint language.

![](https://substackcdn.com/image/fetch/$s_!OErx!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2f458080-280f-447c-bd0e-0fcb779f770b_2688x1536.jpeg)

While SHACL may seem like a new technology, it’s worth noting that the SHACL 1.0 specification was released in 2017, making it eight years old this year. In that time, it has gained a slow but steady fan base as a structural alternative to OWL. It is looking increasingly likely that SHACL 1.2 will be released as a formal spec towards the end of 2026 or early 2017 at the latest. A recent drop on [11 December 2025](https://w3c.github.io/data-shapes/shacl12-core/) provides a good indication of what the final specification will look like, including a [summary of changes](https://w3c.github.io/data-shapes/shacl12-core/#changes-12) from the SHACL 1.0 Core specification.

I want to cover these changes and discuss their implications:

## Shape Classes and sh:shape

As I’ve been stressing in previous articles, a node shape is not necessarily a class. However, in many cases, the two are structurally close enough that it makes sense to treat them as the same. Thus, the expression:

```markup
ex:PersonShape a sh:NodeShape;
    sh:targetClass ex:Person .
```

tends to occur a lot in SHACL 1.0. Given that, in SHACL 1.2, the working group made a formal sh:ShapeClass:

```markup
ex:Person a sh:ShapeClass .
```

A Shape Class is a shape that is also a class. It does not require a separate `sh:targetClass` predicate and can be thought of as being equivalent to the previous expression.

One advantage of this is that you can use the new `sh:shape` property with such shape classes:

```markup
ex:Person a sh:ShapeClass .

ex:JaneDoe sh:shape ex:Person .
ex:JohnSmith sh:shape ex:Person .
```

without needing to declare it as formally `rdf:type`. `sh:shape` can also be used with other shapes, but if the node shape is not formally a shape class, then you would need to declare it explicitly to indicate that it has a separate class:

```markup
ex:PersonShape a sh:NodeShape .
ex:Person a rdfs:Class .

ex:JaneDoe a ex:Person, sh:shape ex:PersonShape .

# or

ex:Person a rdfs:Class .
ex:PersonShape a sh:NodeShape ;
    sh:targetClass ex:Person .

ex:JaneDoe a ex:Person .
```

The `sh:ShapeClass` was introduced to make such logic cleaner in those cases where the node shape WAS also an RDF Class, and it is used by other properties introduced in SHACL 1.2.

## sh:targetWhere

A common requirement in SHACL is to identify a subset of nodes that belong to a class but satisfy additional constraints. For example, suppose you have a graph of potential voters and want to identify those who live in the Pacific Northwest (Washington, Oregon, Idaho, Montana, and Alaska) in the United States. This kind of scenario occurs often enough that a new property called `sh:targetWhere` was introduced in SHACL 1.2.

```markup
# Shape Graph
#============#

ex:NWPerson_Shape
    a sh:NodeShape ;
    sh:targetWhere [
        sh:class ex:Person ;
        sh:property ex:NWPerson_state_PropertyShape ;
    ] ;
    sh:property ex:NWPerson_votedFor_PropertyShape ;
    .

ex:NWPerson_state_PropertyShape
    a sh:PropertyShape ;
    sh:path ex:state ;
    sh:minCount 1 ;
    sh:in (ex:WA ex:OR ex:ID ex:MT ex:AK) ;
    sh:message “Person is not in the Pacific Northwest” ;
    .

ex:NWPerson_votedFor_PropertyShape
   sh:path ex:votedFor ;
   sh:class ex:Person ;
   sh:minCount 1 ;
   sh:maxCount 1 ;
   .

#Data Graph
#============#

ex:JaneDoe a ex:Person ;  # Is selected by #NWPerson_Shape
   ex:state ex:WA ;
   ex:Thelma .

ex:BobJones a ex:Person ;  # Is not selected by #NWPerson_Shape
   ex:state ex:CA ;
   ex:Louise .

# Generated Report Graph (in ex:Graph_Results )
#============#

sh:ValidationResult
   sh:focusNode ex:JaneDoe ;
   sh:conforms true ;
   .

sh:ValidationResult
   sh:focusNode ex:BobJones ;
   sh:sourceShape ex:NWPerson_state_PropertyShape ;
   sh:conforms false ;
   sh:path ex:state ;
   sh:value ex:CA ;
   sh:resultMessage "Person is not in the Pacific Northwest"
   .
```

In this particular case, the valid (selected) nodes are those `ex:Person` nodes where the `ex:state` property is one of the states in the `sh:in` list.

Note that for each node in the dataset, there is a report that is generated as to whether it confirms (`sh:conforms true`) or doesn’t (`sh:conforms false`). Conforming nodes can be passed on to other queries or similar operations, while non-conforming nodes have indications for why they don’t conform. This is probably less efficient than a SPARQL query, but it provides additional metadata on why non-conforming nodes fail.

Validation results are frequently written to named graphs (here, `ex:Graph_Results`). Once you validate a nodeset, you can then extract the results with a SPARQL query:

```markup
select ?node where {
    graph ex:Graph_Results {
        ?result sh:focusNode ?node .
        ?result sh:conforms true .
    }
}
```

## SHACL Lists and List Predicates

Lists have always been a bit problematic in RDF. An RDF List is a hybrid structure that may not appear to be a list at first glance. A list with three items looks like this in RDF:

```markup
ex:MyList rdf:value _:b1.
_:b1 rdf:first ex:Item1 .
_:b1 rdf:rest _:b2 .
_:b2 rdf:first ex:Item2 .
_:b2 rdf:rest _:b3 .
_:b3 rdf:first ex:Item3 .
_:b3 rdf:rest rdf:nil .
```

Turtle encodes this in an abstraction layer consisting of each item, separated by a space, encased in parentheses:

```markup
ex:MyList rdf:value (ex:Item1 ex:Item2 ex:Item3) .
```

It should be noted that there is a difference between a comma-separated list in Turtle, which is unordered, and an RDF linked list, which is ordered. The operations in this section specifically focus on the latter.

SHACL continues this abstraction of lists, though this didn’t really emerge until SHACL 1.1 and the introduction of SHACL Lists. Still, SHACL 1.2 significantly expands upon the operations that can be done on them.

For instance, let’s say that you have a property called ex:speakerOrder for a conference of class ex:Conference:

```markup
# data graph
ex:Conference123 a ex:Conference; 
  ex:speakerOrder ( “Alice” “Bob” “Charlie” ) .
# or
ex:Conference123 a ex:Conference; 
  ex:speakerOrder ( ex:Alice ex:Bob ex:Charlie ) .
```

In SHACL, the definition for this would look as follows:

```markup
ex:ConferenceShape
  a sh:NodeShape ;
  sh:targetClass ex:Conference ;
  sh:or ([
    sh:path ( sh:zeroOrMorePath rdf:rest ] rdf:first ) ;
    sh:datatype xsd:string ;
    sh:minCount 1 ;
  ]
  [
    sh:path ( [ sh:zeroOrMorePath rdf:rest ] rdf:first ) ;
    sh:class ex:Speaker ;
    sh:minCount 1 ;
  ])
  .
```

The `sh:or` A predicate is a way of bundling alternative property definitions. Note that it is itself a linked list. The `sh:path` statement similarly is a linked list, in this case, indicating the same thing as the SHACL pattern `rdf:rest*/rdf:first`. The `sh:class` The second property definition indicates the class of each item in the sequence, with the caveat that you can either have all strings or all IRI nodes (of class `ex:Speaker`), but not both intermixed.

> The `sh:class` or `sh:datatype` in this case resolves to the class of the item, not the class of the list.

There are a few additions in SHACL 1.2 for lists. The first, sh:memberShape, identifies the shape of the members without necessarily formally specifying a class. For instance, if you ONLY wanted node IRIs in the list (not strings), you could rewrite the above as:

```markup
ex:ConferenceShape
    a sh:NodeShape ;
    sh:targetClass ex:Conference ;
    sh:property ex:ConferenceShape-speakerOrder ;
.
ex:ConferenceShape-speakerOrder
    a sh:PropertyShape ;
    sh:path ex:speakerOrder ;
    sh:memberShape [
        sh:nodeKind sh:IRI ;
        sh:class ex:Speaker ;
    ] .
```

Note here that you are implicitly assuming that the path has a target of a list, rather than needing to enumerate the ordering, through the presence of the explicitly `sh:memberShape` predicate. This can make SHACL code that contains extensive lists considerably more legible, because you’re replacing the `rdf:rest*/rdf:first` expression with an abstraction.

If you want to extend this such that there is a minimum of one speaker and a maximum of five speakers, you can use the `sh:minListLength` and `sh:maxListLength` properties:

```markup
ex:ConferenceShape
    a sh:NodeShape ;
    sh:targetClass ex:Conference ;
    sh:property ex:ConferenceShape-speakerOrder ;
.
ex:ConferenceShape-speakerOrder
    a sh:PropertyShape ;
    sh:path ex:speakerOrder ;
    sh:memberShape [
        sh:nodeKind sh:IRI ;
        sh:class ex:Speaker ;
        sh:minListLength 1;
        sh:maxListLength 5;
    ] .
```

Finally, you can catch situations where the same item is listed more than once with the Boolean sh:uniqueMembers flag:

```markup
ex:ConferenceShape-speakerOrder
    a sh:PropertyShape ;
    sh:path ex:speakerOrder ;
    sh:memberShape ex:ConferenceShape-speakerOrder-ListShape ;

ex:ConferenceShape-speakerOrder-ListShape
    a sh:NodeShape ;
    sh:nodeKind sh:BlankNode ;
    sh:class ex:Speaker ;
    sh:minListLength 1;
    sh:maxListLength 5;
    sh:uniqueMembers true ;
    ] .
```

Thus, the data graph

```markup
ex:Conference123 a ex:Conference ; 
  ex:speakerOrder ( ex:Alice ex:Bob ex:Charlie ex:Alice ) .
```

will raise an error because `ex:Alice` is repeated in the list:

```markup
sh:ValidationResult
   sh:focusNode ex:Conference123 ;
   sh:sourceShape ex:ConferenceShape-speakerOrder-ListShape ;
   sh:conforms false ;
   sh:path ex:speakerOrder ;
   sh:value ex:Alice ;
   sh:resultMessage “Duplicate items in list.”
   .
```

## Reification Shapes

It’s perhaps coincidental that reification (RDF-Star) and SHACL both began to gain traction around the same time. Reification - annotations on a given triple - was part of RDF from the beginning, but the original implementation was awkward, and had the potential of causing the number of triples in the triple stores to explode; it was also something that wasn’t a key feature of OWL, so there was a tacit agreement to largely ignore reification until the introduction of Neo4J introduced a model where reifications were (somewhat) baked into the architecture.

As has been noted elsewhere, you can get by without reification in RDF - reification can be thought of as setting up a secondary class that represents an interaction between two resources. For instance, in the statement

```markup
ex:Liz ex:married ex:Richard .
```

there is an implicit “Marriage class” that is implied with the statement, with the assumption that `ex:Liz` (the subject) is identified with the property ex:spouse1 and `ex:Richard` (the object) is identified with the property ex:spouse2.

As an aside, there are many ways to model this. For instance, you can make the statement:

```markup
ex:Marriage1 a ex:Marriage ;
   ex:hasSpouses (ex:Liz ex:Richard) .
```

This solves one of the significant problems with reifications, such as the case where a property is symmetric (such as `ex:married`) or where there are more than two members in a relationship (in an open marriage, for instance, where there may be three or more participants. However, this probably belongs in the previous section. FOAF runs into the same problem, by the way.

Let’s take this model as a starting point, and assume that in such a marriage (whether legal or not in a given jurisdiction). Liz marries Richard, and at some point, Joan joins them; Richard dies a few years later.

This can be viewed as three marriages, but it is also an example of a single marriage with different spouses moving in and out. This latter would look like the following:

```markup
# Data Graph
ex:Marriage1 a ex:Marriage ;
    ex:hasSpouses 
       (ex:Liz ex:Richard) ~ _:marriageSpouseList1 { 
           a ex:MarriageSpouseList;
           ex:begins "1992"^^xs:gYear; 
           ex:ends "1994"^^xs:gYear;
           }, 
       (ex:Liz ex:Richard ex:Joan) ~ _:marriageSpouseList2 { 
           a ex:MarriageSpouseList;
           ex:begins “1995”^^xs:gYear; 
           ex:ends “2012”^^xs:gYear;
           },
       (ex:Liz ex:Joan) ~ _:marriageSpouseList3 { 
           a ex:MarriageSpouseList;
           ex:begins “2012”^^xs:gYear; 
           ex:ends “2025”^^xs:gYear;
           }  .
```

*Note: for those uncomfortable with the notion of open marriage, the same model can be used for any team with members joining and leaving over time.*

We can use SHACL to describe this (somewhat crazy) data structure by using the `sh:reificationShape` property.

```markup
ex:Marriage a sh:ShapeClass ;
    sh:property ex:Marriage_hasSpouses_PropertyShape ;
    .

ex:Marriage_hasSpouses_PropertyShape as sh:PropertyShape ;
   sh:path ex:hasSpouses ;
   sh:class ex:Person ;
   sh:memberShape ex:Marriage_SpouseList ;
   sh:reifierShape ex:Marriage_Submarriage ;
   sh:reificationRequired true ;
   .

ex:Marriage_SpouseList
   a sh:NodeShape ;
   sh:minListLength 2 ;
   sh:uniqueMembers true ;
   .

ex:Marriage_SubMarriage
   a sh:NodeShape ;
   sh:property [
      sh:path ex:begins;
      sh:datatype xs:gYear;
      sh:minCount 1;
      sh:maxCount 1;
      ],
      [
      sh:path ex:ends;
      sh:datatype xs:gYear;
      sh:minCount 0;
      sh:maxCount 1;
      ].
```

The reification exists on the `ex:hasSpouses` property, with the associated shape eing the e `x:Marriage_SubMarriage` shape. Note that this differs from the shape used to describe the list of spouses (`ex:Marriage_SpouseList) in that ex:Marriage_SubMarriage ` talks about the statement as a whole, while `  ex:Marriage_SpouseList  ` just describes the list of spouses.

Finally, note that in `ex:Marriage_hasSpouses_PropertyShape,` the statement `sh:reificationRequired true` indicates that for `ex:hasSpouses` triple, the reification *must be present.* This becomes a part of the data structure, rather than simply an annotation.

The reification capability of SHACL 1.2 is critical because it makes it possible to establish a data model for the body of reified statements, something that currently does not exist in OWL (it may eventually; there is an effort to build up RDF-Star capability as part of the general RDF upgrade, but it’s not as big a priority at the moment).

## sh:codeIdentifier

On the topic of annotations, the `sh:name` property in SHACL was initially intended as a descriptive label for properties (analogous to `rdfs:label`), but because SHACL emerged around the same time as GraphQL, the `sh:name` property increasingly became associated with the programmatic name of a property in GraphQL, essentially driving GraphiQL interfaces via TypeScript.

After a lot of discussion, the working group created a second property `sh:codeIdentifier` that serves the purpose of providing a binding name for an external code language interface. In general, the intention is for such names to follow the convention

```markup
coalesce(sh:codeIdentifier,sh:name, local-name(sh:path))
```

This also has interesting implications for JSON-LD files, as graph-to-JSON-LD converters can use SHACL to obtain the code identifier as a name declared in the @context section of the JSON-LD file.

## Summary

There’s considerably more to the SHACL 1.2 core, which I’ll deal with in Part II of this series, including node expressions, list unions, shacl imports, subclassing, recursion, and validator configurations. Part III will likely be deferred for a bit, as it covers rules, SPARQL-SHACL, UI, and other dynamic uses of SHACL, which are on a longer track than SHACL 1.2 core, and are still under foundational development.

Note that the topics discussed in this post are preliminary and may change before the final version. I’ll try to revise this article when this happens.

In Media Res,

![](https://substackcdn.com/image/fetch/$s_!P3d5!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7d2ec409-1b4f-44f5-be89-ad63f61ff0c6_2688x1536.jpeg)

[Kurt Cagle](https://linkedin.com/in/kurtcagle)  
[The Ontologist](https://ontologist.substack.com/)

Check out my LinkedIn newsletter, [The Cagle Report](https://www.linkedin.com/newsletters/the-cagle-report-6672594836610252800/).

I am also currently seeking new projects or work opportunities. If anyone is looking for a CTO or Director-level AI/Ontologist, please get in touch with me through my Calendly:

If you want to shoot the breeze or have a cup of virtual coffee, I have a Calendly account at [https://calendly.com/theCagleReport](https://calendly.com/theCagleReport). I am available for consulting and full-time work as an ontologist, AI/Knowledge Graph guru, and coffee maker. Also, for those of you whom I have promised follow-up material, it’s coming; I’ve been dealing with health issues of late.

I’ve created a [Ko-fi account](https://ko-fi.com/E1E117YF5K) for voluntary contributions, either one-time or ongoing, or you can subscribe directly to [The Ontologist](https://ontologist.substack.com/). If you find value in my articles, technical pieces, or general thoughts about work in the 21st century, please consider contributing to support my work and allow me to continue writing.