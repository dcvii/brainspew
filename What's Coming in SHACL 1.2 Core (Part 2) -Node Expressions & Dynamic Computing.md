---
title: "What's Coming in SHACL 1.2 Core (Part 2) -Node Expressions & Dynamic Computing"
source: "https://ontologist.substack.com/p/whats-coming-in-shacl-12-core-part-870?publication_id=1877971&post_id=181540955&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Kurt Cagle]]"
published: 2025-12-14
created: 2025-12-14
description: "Looking into one of the more exciting features of SHACL 1.2."
tags:
  - "clippings"
---
### Looking into one of the more exciting features of SHACL 1.2.

![](https://substackcdn.com/image/fetch/$s_!Xm6s!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffaa851d7-509b-485b-8c5f-9889126249f9_2688x1536.jpeg)

[In my previous post in this series](https://ontologist.substack.com/p/whats-coming-in-shacl-12-core-part), I examined several new object classes in SHACL 1.2, including Shape classes, SHACL Lists, and Reification Shapes. This time around, I’m going to shift my focus to what I consider the most intriguing aspect of SHACL 1.2: node expressions.

## Node Expressions

Here’s an interesting question: what is the largest city in a given US state? State populations rise and fall every ten years, as each state conducts a census. Some cities grow, others shrink, so city-size rankings change; this answer will vary depending on the most recent census. In a static dataset, this might involve setting a property to a specific value (here, `ex:largestCityByPopulation`) every ten years, which can be done computationally all at once, but in cases where you have a large number of interdependent variables, this can get to be a complex update query.

A node expression is an alternative approach to running a SPARQL update query. For instance, suppose that you have the following dataset:

```markup
ex:WA a ex:State;
    ex:identifier "WA" ;
    rdfs:label "Washington" ;
    ex:city ex:Seattle, ex:Tacoma, ex:Olympia, ex:Spokane, ex:Vancouver, ex:Everett, ex:Bellevue, ex: Kirkland, ex:Redmond ;
    ex:capitalCity ex:Olympia ;
    .

ex:Seattle
    rdfs:label "Seattle" ;
    ex:population "780995"^^xs:integer;
    .

ex:Tacoma
    rdfs:label “Tacoma" ;
    ex:population “228202”^^xs:integer;
    .

ex:Olympia
    rdfs:label “Olympia” ;
    ex:population “56271”^^xs:integer;
    .

ex:Olympia
    rdfs:label “Spokane” ;
    ex:population “230609”^^xs:integer;
    .

ex:Vancouver
    rdfs:label “Vancouver” ;
    ex:population “198992”^^xs:integer;
    .
```

With SPARQL UPDATE, this becomes a pretty straightforward query.

```markup
DELETE {?state ex:largestCityByPopulation ?oldCity}
INSERT {?state ex:largestCityByPopulation ?city}
WHERE {
    VALUES ?state {ex:WA}
    OPTIONAL {
        ?state ex:largestCityByPopulation ?oldcity .
    }
    ?state ex:city ?city .
    ?city ex:population ?population .
} ORDER by desc(?population) limit 1
```

In this particular case, if a previous `ex:largestCityByPopulation` entry exists, delete it; then, for each city in the state, retrieve its population. Once this set has been defined, order these in descending order by population, and take the topmost item to then create a new `ex:largestCityByPopulation` entry. In this case, `ex:Seattle` will bubble to the top, as it is more than three times as large as any other city.

## Using SHACL-SPARQL

What is important here is that the `property ex:largestCityByPopulation` is calculated - it will change depending upon other changes in the graph (namely, city population). In SHACL, there are two alternatives available. The first is to use a SHACL-SPARQL construct:

```markup
ex:State
    a sh:ShapeClass ;
    sh:property ex:State-city ;
    sh:property ex:State-largestCityByPopulation .

ex:State-city
    a sh:PropertyShape ;
    sh:name “cities ;
    sh:description “The state’s cities.” ;
    sh:path ex:city ;
    sh:class ex:City .

ex:State-largestCityByPopulation
    a sh:PropertyShape ;
    sh:path ex:largestCityByPopulation ;
    sh:values [
        sh:select “”“
            SELECT ?city
            WHERE {
                ?this ex:city ?city .
                ?city ex:population ?pop .
            }
            ORDER BY DESC(?pop)
            LIMIT 1
        “”“
    ] .
```

In this particular case, `sh:path` identifies the property to be filled, while `?this` contains the targetNode (`ex:WA`). The `sh:values` property in this case indicates the output of the query *as an unordered list* (handling linked lists is still under discussion). As there is only one item in this case (because of the LIMIT 1 constraint), the value of the first item in the SPARQL query (here, `?city`) becomes the value of the property.

I’ll return to the use of SHACL-SPARQL in a subsequent post, but in this one, I want to focus on another way of accomplishing this kind of query: the Node Expression.

## Using Node Expressions

Node expressions are an alternative form to SPARQL queries, and use RDF within shapes (within the `shnex:` namespace) to create conditional clauses, ordering, iteration and similar constructs. An alternative to `ex:State-largestCityByPopulation` node expressions would look like the following:

```markup
ex:State-largestCityByPopulation
    a sh:PropertyShape ;
    sh:path ex:largestCityByPopulation ;
    sh:class ex:City ;
    sh:values [
        shnex:nodes [
            shnex:nodes [
                shnex:pathValues ex:city ;
            ] ;
            shnex:orderBy ex:population ;
            shnex:orderDirection shnex:Descending ; # Note, currently undefined
        ] ;
        shnex:limit 1 ;
    ] .
```

In this particular case, the `sh:values` “section” uses the `shnex:nodes` to iterate over the city nodes, ordering them by population (descending). The output is then iterated to the specified limit (here, 1).

*Note that the exact syntax for such ordering, grouping, limiting and offsets is still in discussion, which is why* `shnex:orderDirection` *and* `shnex:Descending` *are not currently defined in the specification (in other words, check with the spec before taking this as the final word).*

## Node Expressions and SHACL UI

There are two use cases for SHACL-SPARQL with regard to validation - returning a Boolean value indicating whether the given target node satisfies the query (in which case the indicated node is compliant) or not (it fails compliance), and supplying parameters to the `sh:message` statement. The SHACL-SPARQL constraints can get complex, and I’m deferring them to a future article.

Node expressions, on the other hand, don’t really factor that much into validation. They can be used for conditional expressions, but their primary use is in **user interface (UI)** design. Now, it’s worth qualifying this term, because it has a specialised meaning here. *UI describes the model presented to the user when they make a request.* For instance, in the previous example, there is no `ex:largestCityByPopulation` property in the data graph. This is a computed property.

In a SHACL-based system, if a request is made for `ex:WA` from an external client, a SHACL UI architecture would identify that `ex:WA` is a shape class (`ex:State`), and would also indicate that one of the properties of that shape class is `ex:State-largestCity`

```markup
ex:State
    a sh:ShapeClass ;
    sh:property ex:State-city ;
    sh:property ex:State-largestCityByPopulation .
```

This is a calculated property. When the request is made for that node, the SHACL UI component will examine that property, see if it is currently enabled (which it is by default), and then use the node expressions to generate the corresponding output:

```markup
ex:WA a ex:State;
    ex:identifier “WA” ;
    rdfs:label “Washington” ;
    ex:city ex:Seattle, ex:Tacoma, ex:Olympia, ex:Spokane, ex:Vancouver, ex:Everett, ex:Bellevue, ex: Kirkland, ex:Redmond ;
    ex:capitalCity ex:Olympia ;
    # New property
    ex:largestCityByPopulation ex:Seattle ;
    .
```

Similarly, it is possible to remove generated nodes from a `sh:nodes` list that satisfy a given property:

```markup
ex:PublisherShape
    a sh:NodeShape ;
    sh:targetClass ex:Publisher ;
    sh:property ex:PublisherShape-availableAuthors .

ex:PublisherShape-availableAuthors
    a sh:PropertyShape ;
    sh:path ex:availableAuthors ;
    sh:class ex:Person ;
    sh:description “Authors who are currently available (not on leave).” ;
    sh:values [
        shnex:nodes  [ shnex:pathValues ex:author ] ;           
        shnex:remove [ shnex:pathValues ex:authorOnLeave ] ;  
    ] .
```

In this case, the initial dataset for publishers includes the predicates `ex:author` and `ex:authorOnLeave`. In this case, the newly generated property `ex:availableAuthors` performs an exclusion from the total number of authors of those authors currently on leave. This is significant in part because the properties that are generated for the output (the UI) do not directly include either `ex:author` or `ex:authorOnLeave` directly (this is configurable in most cases). This means that with the following data graph:

```markup
# Data Graph

ex:BigPublisher a ex:Publisher ;
    ex:author ex:BillShakespeare, ex:EddiePoe, ex:MaryWollstone, ex:HerbWells, ex:ArtClarke ;
    ex:authorOnLeave ex:EddiePoe, ex:ArtClarke .
```

the output graph would look like:

```markup
#Output Graph

ex:BigPublisher a ex:Publisher ;
   ex:availableAuthors ex:BillShakespeak, ex:MaryWollstone, ex:HerbWells .
```

***I cannot overstate the significance of this:***

One key issue in working with graphs is that there will always be information you do not want your audience to see unless they have the appropriate permissions (Access Control Lists, or ACLs). This is one reason why, in general, you don’t expose your knowledge graph in its entirety unless there is no reason to secure it. SHACL node expressions enable precisely that: hiding sensitive parts of the graph, modifying the graph's output to provide summary information without necessarily disclosing details, and creating new properties that are easier to navigate.

Put another way, the combination of Node Expressions and SHACL UI makes it possible to provide what are known as ***views*** in other query languages. This is sort of what the CONSTRUCT statement is supposed to do, but the CONSTRUCT statement assumes that you know the underlying graph structure. A SHACL view, by contrast, provides an interface that may vary significantly from the underlying implementation. Because it is part of the model, tools can expose the shape of that interface independently of what lies beneath it.

## Enumerations and Node Expressions

One of the more vexing problems that you have with knowledge graphs is determining constraints for taxonomies. For example, if you have a given country, the states (or provinces) of the country will be different.

Node expressions can simplify this considerably. Consider the following data graph:

```markup
# Countries
ex:Australia
    a            ex:Country ;
    ex:stateCode “ACT”,
                 “NSW”,
                 “NT”,
                 “QLD”,
                 “SA”,
                 “TAS”,
                 “VIC”,
                 “WA” ;
.
ex:USA
    a            ex:Country ;
    ex:stateCode “AL”,
                 “AK”,
                 “AZ”,
                 “AR” ; # ...
.
# Addresses
ex:ArizonaAddress1
    a ex:Address ;
    ex:street “123 John Muir Ave” ;
    ex:country ex:USA ;
    ex:state “AZ” ;
.
ex:QueenslandAddress1
    a ex:Address ;
    ex:street “123 Bob Katter Cl” ;
    ex:country ex:Australia ;
    ex:state “QLD” ;
.
```

Rather than hard-coding these values into a `sh:in` statement, you can use node expressions to handle the mappings:

```markup
ex:Address
    a sh:ShapeClass ;
    sh:property ex:Address-state ;
.
ex:Address-state
    a sh:PropertyShape ;
    sh:path ex:state ;
    sh:in [
        shnex:pathValues ( ex:country ex:stateCode )
    ] .
```

In this case, each address target node checks the `ex:state` code and determines whether it is in the external `ex:country` node for that entry. This approach works nicely in that the SHACL code stays distinct from the constraint values, meaning that you can keep taxonomy information in the data graph rather than in the shape graph.

A similar capability is given wth the shnex:if|then|else commands. For example, suppose that you wanted to indicate in a pattern that the minimum age to be president in a country is 18, except in the USA, where it’s 35, you would do so as follows:

```markup
ex:PresidentShape
    a sh:NodeShape ;
    sh:targetClass ex:President ;
    sh:property ex:PresidentShape-age ;
.
ex:PresidentShape-age
    a sh:PropertyShape ;
    sh:path ex:age ;
    sh:minInclusive [
        shnex:if [
            sparql:eq (
                [ shnex:pathValues ex:country ]
                ex:USA
            )
        ]
        shnex:then 35 ;
        shnex:else 18 ;
    ] .
```

There is a similar `sparql:if()` function that performs the same type of actions in a more functional form:

```markup
ex:PresidentShape
    a sh:NodeShape ;
    sh:targetClass ex:President ;
    sh:property ex:PresidentShape-age ;
.
ex:PresidentShape-age
    a sh:PropertyShape ;
    sh:path ex:age ;
    sh:minInclusive [
        shnex:if (
            sparql:eq (
                [ shnex:pathValues ex:country ]
                ex:USA
                ) 
            35 
            18 )
       ] .
```

Other SPARQL conditional functions, such as `sparql:coalesce()` have similar representations.

## Node Expressions and Analytics

Node expressions also provide mechanisms for doing basic analytics (as well as extension mechanisms to do advanced analytics). For instance, suppose that you have the following invoice for work done:

```markup
# Data Graph

ex:Invoice123 a ex:Invoice ;
    ex:item [
       ex:code "prog" ;
       ex:label "Programming" ;
       ex:hoursBilled 24.25 ;
       ex:rate 65.00 ;
       ],[
       ex:code “mtg” ;
       ex:label “Meeting” ;
       ex:hoursBilled 15.75 ;
       ex:rate 45.00 ;
       ],[
       ex:code “dgn” ;
       ex:label “Design” ;
       ex:hoursBilled 17.00 ;
       ex:rate 75.00 ;
       ] ;
       .
```

A node expression approach can be used to determine the composite total:

```markup
ex:Invoice a sh:GraphClass ;
     sh:property ex:Invoice_Total, ex:Invoice_SubmittedTime ;
     .

ex:Invoice_Total a sh:PropertyNode ;
     sh:datatype xs:Decimal ;
     sh:path ex:invoiceTotal ; 
     sh:values [
          shnex:nodes [
               shnex:pathValues ex:item
               ];
          shnex:sum [
               sparql:multiply (ex:hoursBilled ex:rate)
               ]
          ]
     ].

ex:Invoice_SubmittedTime a sh:PropertyNode;
     sh:datatype xs:dateTime ;
     sh:path ex:submittedtime ;
     sh:values [ sparql:now () ] ;
     .
```

In this particular case, the values field iterates over the Item nodes from `ex:item`, then performs a sum on the multiplied values of ex:houseBilled and e `x:rate` from each line item. The output of this ($3560.00) is

```markup
ex:Invoice123 a ex:Invoice ;
    ex:invoiceTotal "3560.00"^^xs:decimal ;
    ex:submittedTime "2025-12-13T17:24:32"^^xs:dateTime ;
    .
```

Note the use of `sparql:now` and `sparql:multiply`. SHACL supports most of the SPARQL function set, with parameters (if any) passed as a linked list.

More complex functions (and custom functions) are possible within the SHACL node expression environment. I leave this to a later post, because it is worthwhile as a subject in its own right.

## Final Thoughts on Node Expressions

Node expressions and dynamic SHACL shift the focus of SHACL away from validation - essential but not necessarily critical - to the generation of views (aka transformations) for the language. This parallels the evolution of other schematic languages: it can be argued that XML’s XQuery and XSLT were both natural extensions of XPath on XSD as a query language for XML. While not discussed here, SHACL node expressions in conjunction with the `sparql:concat` The function enables a SHACL UI to generate text-based output, such as HTML or Markdown (as well as direct JSON structures), which cannot be generated directly from SPARQL.

This remains a work in progress, but the implications are noteworthy. Among other things, it represents a third modality of streaming nodes, distinct from sets of triples or tables on a graph, and it provides a mechanism to abstract the internal workings of a graph from its presentation layer.

Significantly, it resolves another crucial problem with SPARQL: you can store (and generate) SHACL as part of the graph. SPARQL has always been awkward in that regard - you could store it as a text literal, but there was no way that you could either construct a SPARQL query within a SPARQL query. With SHACL, on the other hand, you have a language that allows you to generate code dynamically, akin to using RNA to construct new DNA or proteins. I believe this will be a critical component of a graph-based AI system.

In Media Res,

![](https://substackcdn.com/image/fetch/$s_!P3d5!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7d2ec409-1b4f-44f5-be89-ad63f61ff0c6_2688x1536.jpeg)

[Kurt Cagle](https://linkedin.com/in/kurtcagle)  
[The Ontologist](https://ontologist.substack.com/)

Check out my LinkedIn newsletter, [The Cagle Report](https://www.linkedin.com/newsletters/the-cagle-report-6672594836610252800/).

I am also currently seeking new projects or work opportunities. If anyone is looking for a CTO or Director-level AI/Ontologist, please get in touch with me through my Calendly:

If you want to shoot the breeze or have a cup of virtual coffee, I have a Calendly account at [https://calendly.com/theCagleReport](https://calendly.com/theCagleReport). I am available for consulting and full-time work as an ontologist, AI/Knowledge Graph guru, and coffee maker. Also, for those of you whom I have promised follow-up material, it’s coming; I’ve been dealing with health issues of late.

I’ve created a [Ko-fi account](https://ko-fi.com/E1E117YF5K) for voluntary contributions, either one-time or ongoing, or you can subscribe directly to [The Ontologist](https://ontologist.substack.com/). If you find value in my articles, technical pieces, or general thoughts about work in the 21st century, please consider contributing to support my work and allow me to continue writing.