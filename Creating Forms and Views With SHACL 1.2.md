---
title: Creating Forms and Views With SHACL 1.2
source: https://ontologist.substack.com/p/creating-forms-and-views-with-shacl?publication_id=1877971&post_id=182450360&isFreemail=true&r=7br8e&triedRedirect=true
author:
  - "[[Kurt Cagle]]"
published: 2025-12-27
created: 2025-12-27
description: An Exploration of SHACL 1.2 UI
tags:
  - clippings
  - SHACL
  - ontology
---
### An Exploration of SHACL 1.2 UI

![](https://substackcdn.com/image/fetch/$s_!BfL5!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8addd2fa-9884-4612-8da8-4817a3b605eb_2688x1536.jpeg)

A long time ago, I was part of the W3C working group for XForms, which was an early model-view-controller architecture designed to work with XML data documents. XForms was, to put it mildly, too far ahead of its time; one could create an XML data document, then use XForms to both display and manipulate that data in a way that still can’t be done easily with Javascript-based solutions; what’s more, it could be done with remarkably little extra (and in most cases, no) JavaScript code.

So why did XForms fail? It wasn’t because of the technology itself. There were limitations, yes, but they were similar to those found in React or other JavaScript MVC platforms and primarily concerned maintaining bindings across disconnected graphs. Instead, the issues came down to the following:

- It was XPath-based, and there was a deliberate effort by both client vendors and thought leaders of the time to view XPath (and anything XML) as somehow foreign to JavaScript (a sentiment that continues to this day, often with very little empirical evidence).
- It was declarative (XForms was a fairly logical extension of spreadsheet functionality). Again, at the time, the concept of working with declarative applications seemed somewhat anathema to the imperative mindset that most web developers of the period (c. 2008-2012 or so) had.
- It had namespaces (\*\*SHUDDER\*\*). I think that as JSON-LD continues to gain acceptance, there has been a renewed recognition that namespaces are necessary, but at the time, namespaces were considered harmful to programming.

I’ll be honest: SHACL 1.2 UI is the RDF version of XForms. The two are not quite the same - node expressions act as the binding layer rather than XPath expressions, the reference data format is the abstract RDF format rather than XML (which means it actually can work quite nicely with JSON-LD), and the association between SHACL 1.2 UI and the SHACL language itself is considerably closer, but in the right light, SHACL 1.2 UI is a spiritual descendent of XForms.

I contend this is a good thing, for several reasons:

- A SHACL node shape describes a predictable view of a given class or even just a generally defined node resource in a consistent manner. This means that, regardless of the development environment, having a language for describing forms guarantees that the resource's data intent is displayed or made available for editing.
- When you get into large graphs, the number of potential classes needed to display (especially when they are composite or nested forms) can grow rapidly, with the cost of building such forms (read-only or read-write) adding significantly to the overall cost of any project. By making the UI an effective part of the interface, these can be automatically generated without the need for human-generated, expensive UIUX code.
- Dynamic properties, an integral part of the SHACL 1.2 package, also enable the computation of properties at run time that are not necessarily stored directly in the knowledge graph.
- You can use groups and ordering to ensure that content is displayed in a specific manner, and you can also handle components (such as addresses) that multiple classes might utilise.
- In such a controlled form, you can incorporate logic constraints that make specific properties (or subforms) only visible or editable if you have relevant privileges, which can be stored within the graph itself or made available through system parameterisation outside of the user’s control.
- This also means you can secure personal information (PPI) or protected health information (PHI), so the information displayed changes based on a user's permissions. This is an integral part of any information system.

With these and other factors, the notion of SHACL 1.2 UI forms should be a no-brainer.

## Preparing Data For SHACL 1.2 UI

The following illustrates a sample data graph that holds address information for a given person, based on the schema.org ontology:

```markup
# Turtle - Data 
@prefix rdf:    <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs:   <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd:    <http://www.w3.org/2001/XMLSchema#> .
@prefix schema: <http://schema.org/> .
@prefix ex:     <http://example.org/> .

# =============================================================================
# Sample Address Data
# =============================================================================

ex:alice a schema:Person ;
    schema:name "Alice Nakamura" ;
    schema:email "alice.nakamura@example.com" ;
    schema:address ex:alice-address .

ex:alice-address a schema:PostalAddress ;
    rdfs:label "Alice's Home Address" ;
    schema:streetAddress "742 Evergreen Terrace, Unit 3B" ;
    schema:addressLocality "Springfield" ;
    schema:addressRegion "OR" ;
    schema:postalCode "97403" ;
    schema:addressCountry ex:USA ;
    ex:addressType ex:Residential ;
    ex:isPrimary true ;
    ex:validFrom "2020-03-15"^^xsd:date ;
    ex:deliveryInstructions "Ring doorbell twice. Leave packages at side door if no answer."@en .

# Reference data
ex:USA a schema:Country ;
    rdfs:label "United States"@en ;
    schema:identifier "US" .

ex:Residential a ex:AddressType ;
    rdfs:label "Residential"@en .

ex:Commercial a ex:AddressType ;
    rdfs:label "Commercial"@en .

ex:POBox a ex:AddressType ;
    rdfs:label "P.O. Box"@en .
```

The data is straightforward, with the caveat that the state codes are provided as two-character strings rather than enumerated instances.

## SHACL 1.2 UI Views and Editors

The SHACL UI distinguishes between SHACL used to facilitate read-only displays (**views**) and read-write forms (**editors**). In general, these are specified at the property level and make use of the new `shui:` (SHACL UI) namespace. Note that this is distinct from the earlier Data Shape (`dash:`) namespace, although they have many similar properties:

```markup
@prefix rdf:    <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs:   <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd:    <http://www.w3.org/2001/XMLSchema#> .
@prefix sh:     <http://www.w3.org/ns/shacl#> .
@prefix shui:   <http://www.w3.org/ns/shacl-ui#> .
@prefix schema: <http://schema.org/> .
@prefix ex:     <http://example.org/> .

# =============================================================================
# SHACL 1.2 UI Shapes for Postal Address
# =============================================================================

# -----------------------------------------------------------------------------
# PersonShape - Main shape for schema:Person
# -----------------------------------------------------------------------------

ex:PersonShape a sh:NodeShape ;
    sh:targetClass schema:Person ;
    rdfs:label "Person"@en ;
    rdfs:comment "Shape for validating Person entities with address information"@en ;
    sh:closed false ;
    sh:ignoredProperties ( rdf:type ) ;

    # UI Configuration for the shape
    shui:defaultView shui:FormView ;
    sh:order 1 ;
    sh:property ex:PersonShape_name, 
                ex:PersonShape_email, 
                ex:PersonShape_address.

ex:PersonShape_name a sh:PropertyShape;
        sh:path schema:name ;
        sh:name "Name"@en ;
        sh:description "The full name of the person"@en ;
        sh:datatype xsd:string ;
        sh:minCount 1 ;
        sh:maxCount 1 ;
        sh:minLength 1 ;
        sh:maxLength 200 ;
        sh:order 1 ;
        # SHACL-UI annotations
        shui:singleLine true ;
        shui:viewer shui:LiteralViewer ;
        shui:editor shui:TextFieldEditor ;
        shui:propertyRole shui:KeyInfoRole ;
    ] ;

ex:PersonShape_email a sh:PropertyShape;
        sh:path schema:email ;
        sh:name "Email Address"@en ;
        sh:description "Email address(es) for the person"@en ;
        sh:or (
            [ sh:datatype xsd:string ; sh:pattern "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$" ]
            [ sh:nodeKind sh:IRI ]
        ) ;
        sh:minCount 0 ;
        sh:order 2 ;
        # SHACL-UI annotations
        shui:singleLine true ;
        shui:editor shui:TextFieldEditor ;
        shui:viewer shui:LiteralViewer ;
        shui:placeholder "user@example.com" ;
    ] ;

ex:PersonShape_address a sh:PropertyShape;
        sh:path schema:address ;
        sh:name "Address"@en ;
        sh:description "Postal address(es) for the person"@en ;
        sh:node ex:PostalAddressShape ;
        sh:nodeKind sh:IRI ;
        sh:minCount 0 ;
        sh:order 3 ;
        # SHACL-UI annotations
        shui:viewer shui:NestedObjectViewer ;
        shui:editor shui:InstanceSelectEditor ;
        shui:canCreate true ;
        shui:createShape ex:PostalAddressShape ;
    ] .
```

The Person node shape declaration contains a single configuration:

```markup
ex:PersonShape shui:defaultView shui:FormView .
```

This indicates that, by default, the view will be read-only.

## UI Properties

The Person\_name property (here indicated as a blank node property) includes a typical entry with regard tos SHACL-UI:

```markup
# SHACL-UI annotations
      []  shui:singleLine true ; # For the name property
        shui:viewer shui:LiteralViewer ;
        shui:editor shui:TextFieldEditor ;
        shui:propertyRole shui:KeyInfoRole ;
```

This indicates that the default component is the single-line text field (as opposed to a multiline display). This is important for layout purposes, as the multi-line option may contain markup of various types that will be displayed as paragraphs in view mode and as text areas in editor mode. *Note: This feature is still in flux and may be removed.*

The following two lines indicate how the property shape is displayed when given as a read-only view (`shui:viewer`) and a read-write editor (`shui:editor`). In the viewer mode, the `shui:LiteralViewer` indicates that the literal value is shown as a read-only inline text value, based upon the property role, while in the editor mode, the same as shown as a text field (analogous to an `<input text>` field in HTML).

The `shui:propertyRole shui:KeyInfoRole` An annotation is a UI hint that marks a property as a **key identifying field** for the resource. It specifies how form generators and UI renderers should treat that property in display contexts.

**What it does:**

- **List/Table Views** — The property value appears as the primary display text when showing instances in lists, dropdowns, or search results
- **Summary Cards** — Used as the “headline” field in compact/card representations
- **Reference Links** — When another resource links to this one, the KeyInfoRole property provides the human-readable label
- **Form Headers** — May be displayed prominently at the top of edit forms

**Practical example from the shapes:**

```markup
# In PostalAddressShape
sh:property [
    sh:path rdfs:label ;
    sh:name "Address Label"@en ;
    shui:propertyRole shui:KeyInfoRole ;
    ...
] ;
```

When a Person’s address picker shows available PostalAddress instances, instead of displaying raw IRIs like `ex:alice-address`, the UI would show “Alice’s Home Address” (the `rdfs:label` value) because that property has the KeyInfoRole.

**Multiple KeyInfoRole properties:**

If multiple properties have this role, UIs typically concatenate them or use the first one by `sh:order`. For example, a Person shape might mark both `schema:name` and `schema:email` as KeyInfoRole, resulting in displays like “Alice Nakamura ([alice@example.com](https://ontologist.substack.com/p/))”.

It’s analogous to `dash:propertyRole dash:KeyInfoRole` in the TopBraid/DASH vocabulary, or the concept of a “label property” in tools like Protégé.

The property shape `ex:PersonShape_address` is worth examining in more detail:

```markup
ex:PersonShape_address a sh:PropertyShape;
        sh:path schema:address ;
        sh:name "Address"@en ;
        sh:description "Postal address(es) for the person"@en ;
        sh:node ex:PostalAddressShape ;
        sh:nodeKind sh:IRI ;
        sh:minCount 0 ;
        sh:order 3 ;
        # SHACL-UI annotations
        shui:viewer shui:NestedObjectViewer ;
        shui:editor shui:InstanceSelectEditor ;
        shui:canCreate true ;
        shui:createShape ex:PostalAddressShape ;
    ] .
```

The nested object viewer in this case lets you display subforms (such as addresses) within a containing form. The editor mode incorporates the `shui:InstanceSelectEditor` which enables you to select a particular address from the existing set of addresses, and with the `shui:canCreate` and `shui:createShape` statements, you can edit such addresses inline.

## Address UI View

Moving into the address block.

```markup
# -----------------------------------------------------------------------------
# Address View Shape (Read-Only Display)
# -----------------------------------------------------------------------------

ex:AddressViewShape a sh:NodeShape ;
    sh:targetClass schema:PostalAddress ;
    rdfs:label "Address View" ;
    rdfs:comment "Read-only view of a postal address" ;
    sh:closed false ;
    
    # Label property role - used for display title
    sh:property ex:AddressView-label ;
    
    # Core address fields in display order
    sh:property ex:AddressView-streetAddress ;
    sh:property ex:AddressView-addressLocality ;
    sh:property ex:AddressView-addressRegion ;
    sh:property ex:AddressView-postalCode ;
    sh:property ex:AddressView-addressCountry ;
    sh:property ex:AddressView-addressType ;
    sh:property ex:AddressView-isPrimary ;
    sh:property ex:AddressView-validFrom ;
    sh:property ex:AddressView-deliveryInstructions .

ex:AddressView-label a sh:PropertyShape ;
    sh:path rdfs:label ;
    sh:name "Address Label" ;
    sh:description "A human-readable label for this address" ;
    sh:order 0 ;
    sh:datatype xsd:string ;
    sh:maxCount 1 ;
    shui:propertyRole shui:LabelRole ;
    shui:viewer shui:LiteralViewer .

ex:AddressView-streetAddress a sh:PropertyShape ;
    sh:path schema:streetAddress ;
    sh:name "Street Address" ;
    sh:description "The street address including unit/apartment number" ;
    sh:order 1 ;
    sh:datatype xsd:string ;
    sh:minCount 1 ;
    sh:maxCount 1 ;
    shui:viewer shui:LiteralViewer .

ex:AddressView-addressLocality a sh:PropertyShape ;
    sh:path schema:addressLocality ;
    sh:name "City" ;
    sh:description "The city or locality" ;
    sh:order 2 ;
    sh:datatype xsd:string ;
    sh:minCount 1 ;
    sh:maxCount 1 ;
    shui:viewer shui:LiteralViewer .

ex:AddressView-addressRegion a sh:PropertyShape ;
    sh:path schema:addressRegion ;
    sh:name "State/Province" ;
    sh:description "The state, province, or region" ;
    sh:order 3 ;
    sh:datatype xsd:string ;
    sh:minCount 1 ;
    sh:maxCount 1 ;
    shui:viewer shui:LiteralViewer .

ex:AddressView-postalCode a sh:PropertyShape ;
    sh:path schema:postalCode ;
    sh:name "Postal Code" ;
    sh:description "The postal or ZIP code" ;
    sh:order 4 ;
    sh:datatype xsd:string ;
    sh:minCount 1 ;
    sh:maxCount 1 ;
    sh:pattern "^[0-9]{5}(-[0-9]{4})?$" ;
    shui:viewer shui:LiteralViewer .

ex:AddressView-addressCountry a sh:PropertyShape ;
    sh:path schema:addressCountry ;
    sh:name "Country" ;
    sh:description "The country" ;
    sh:order 5 ;
    sh:class schema:Country ;
    sh:minCount 1 ;
    sh:maxCount 1 ;
    shui:viewer shui:LabelViewer .

ex:AddressView-addressType a sh:PropertyShape ;
    sh:path ex:addressType ;
    sh:name "Address Type" ;
    sh:description "The type of address (Residential, Commercial, P.O. Box)" ;
    sh:order 6 ;
    sh:class ex:AddressType ;
    sh:maxCount 1 ;
    shui:viewer shui:LabelViewer .

ex:AddressView-isPrimary a sh:PropertyShape ;
    sh:path ex:isPrimary ;
    sh:name "Primary Address" ;
    sh:description "Whether this is the primary address" ;
    sh:order 7 ;
    sh:datatype xsd:boolean ;
    sh:maxCount 1 ;
    shui:viewer shui:LiteralViewer .

ex:AddressView-validFrom a sh:PropertyShape ;
    sh:path ex:validFrom ;
    sh:name "Valid From" ;
    sh:description "Date when this address became valid" ;
    sh:order 8 ;
    sh:datatype xsd:date ;
    sh:maxCount 1 ;
    shui:viewer shui:LiteralViewer .

ex:AddressView-deliveryInstructions a sh:PropertyShape ;
    sh:path ex:deliveryInstructions ;
    sh:name "Delivery Instructions" ;
    sh:description "Special instructions for deliveries" ;
    sh:order 9 ;
    sh:datatype rdf:langString ;
    sh:maxCount 1 ;
    shui:viewer shui:LangStringViewer .
```

This creates the following read-only form:

![](https://substackcdn.com/image/fetch/$s_!So4C!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F47af7a74-61e5-42b4-bd0d-0624d4197b0b_900x850.png)

While `shui:LiteralViewer` views make up the bulk of these entries, singleton (1:1) enumerated properties, such as isPrimary or zero-to-many enumerated properties, such as Address type, can be displayed as topic flags dynamically with the `shui:LabelViewer.` Special instructions (not shown here) might be shown as ` shui:LangStringViewer` Items with rich text displays.

## SHUI Viewers

Here’s a comprehensive list of `shui:viewer` values for SHACL-UI display rendering:

### Literal Viewers

- **shui:LiteralViewer** — Default viewer for literal values. Displays the lexical form of the literal as plain text. Handles all datatypes with appropriate formatting.
- **shui:LangStringViewer** — Displays language-tagged strings with the language tag shown as a suffix badge (e.g., “Bonjour \[fr\]”).
- **shui:HTMLViewer** — Renders HTML content (`rdf:HTML` datatype) as formatted markup rather than escaped text. Use with caution for untrusted content.
- **shui:MarkdownViewer** — Parses and renders Markdown-formatted text as styled HTML output.
- **shui:CodeViewer** — Displays code with syntax highlighting and monospace font. May support `shui:language` for highlighting mode.
- **shui:JSONViewer** — Renders JSON values with syntax highlighting, collapsible nodes, and proper indentation.
- **shui:XMLViewer** — Displays XML literals with syntax highlighting and tree-style formatting.

### Numeric Viewers

- **shui:IntegerViewer** — Displays integer values with optional thousands separators based on locale.
- **shui:DecimalViewer** — Shows decimal numbers with configurable precision via `shui:decimalPlaces`.
- **shui:PercentageViewer** — Renders numeric values as percentages with % symbol.
- **shui:CurrencyViewer** — Displays monetary values with currency symbol and proper formatting. Configure via `shui:currencyCode`.
- **shui:StarRatingViewer** — Renders numeric ratings (typically 1-5) as filled/empty star icons.
- **shui:ProgressBarViewer** — Shows numeric values as a horizontal progress bar. Requires `sh:minInclusive` and `sh:maxInclusive` for scale.
- **shui:SparklineViewer** — Renders a series of numeric values as a compact inline chart.

### Boolean Viewers

- **shui:BooleanViewer** — Displays boolean values as “Yes/No” or “True/False” text labels.
- **shui:BooleanIconViewer** — Shows boolean values as checkmark/X icons or toggle indicators.
- **shui:BooleanBadgeViewer** — Renders booleans as colored badges (e.g., green “Active” / red “Inactive”).

### Date and Time Viewers

- **shui:DateViewer** — Formats `xsd:date` values according to `shui:dateFormat` or locale defaults.
- **shui:TimeViewer** — Displays `xsd:time` values in 12-hour or 24-hour format.
- **shui:DateTimeViewer** — Combined date and time display for `xsd:dateTime` values.
- **shui:RelativeDateViewer** — Shows dates as relative time (e.g., “3 days ago”, “in 2 weeks”).
- **shui:DurationViewer** — Renders `xsd:duration` values in human-readable form (e.g., “1 year, 2 months, 3 days”).
- **shui:CalendarViewer** — Displays dates within a mini calendar widget context.
- **shui:DateRangeViewer** — Shows start/end date pairs as a formatted range (e.g., “Jan 1 – Mar 15, 2024”).

### IRI and Resource Viewers

- **shui:LabelViewer** — Resolves an IRI to its `rdfs:label` (or configured label property) and displays the human-readable text. Falls back to local name if no label found.
- **shui:URIViewer** — Displays the full IRI as a clickable hyperlink.
- **shui:PrefixedURIViewer** — Shows IRIs in CURIE/prefixed form (e.g., `schema:Person` instead of full URI).
- **shui:LocalNameViewer** — Displays only the local name portion of an IRI (fragment or last path segment).
- **shui:ExternalLinkViewer** — Renders IRIs as hyperlinks that open in a new tab, with an external link icon indicator.
- **shui:ResourceLinkViewer** — Displays the resource label as an internal navigation link within the application.
- **shui:QRCodeViewer** — Generates and displays a QR code encoding the IRI value.

### Image and Media Viewers

- **shui:ImageViewer** — Renders image URLs as inline `<img>` elements with configurable dimensions via `shui:width` and `shui:height`.
- **shui:ThumbnailViewer** — Displays images as small thumbnails, typically clickable to view full size.
- **shui:GalleryViewer** — Shows multiple image values in a grid or carousel layout.
- **shui:AvatarViewer** — Renders images in a circular avatar style, typically for profile photos.
- **shui:VideoViewer** — Embeds video content with playback controls.
- **shui:AudioViewer** — Displays audio content with a playback widget.
- **shui:MediaPlayerViewer** — Generic media viewer that auto-detects content type and renders appropriate player.
- **shui:FileIconViewer** — Shows file references with an appropriate icon based on MIME type or extension.

### Geographic Viewers

- **shui:GeoPointViewer** — Displays latitude/longitude coordinates on an embedded map marker.
- **shui:GeoRegionViewer** — Renders polygon/region geometries on an interactive map.
- **shui:AddressViewer** — Formats postal address components into standard address block layout.
- **shui:MapLinkViewer** — Shows coordinates as a link that opens in Google Maps, OpenStreetMap, etc.

### Structured Data Viewers

- **shui:NestedObjectViewer** — Recursively renders linked resources as expandable inline sub-forms. Uses `sh:node` to determine which properties to display.
- **shui:DetailsViewer** — Similar to NestedObjectViewer but displays nested content in a collapsible details/summary element.
- **shui:CardViewer** — Renders linked resources as summary cards showing key properties.
- **shui:TableViewer** — Displays multi-valued properties or nested collections in tabular format.
- **shui:ListViewer** — Shows `rdf:List` values as an ordered list with sequence numbers.
- **shui:SetViewer** — Displays multi-valued properties as an unordered bullet list or comma-separated inline list.
- **shui:TreeViewer** — Renders hierarchical data (e.g., taxonomies) as an expandable tree structure.
- **shui:JSONTableViewer** — Displays structured JSON data in a table grid format.
- **shui:KeyValueViewer** — Shows map-like structures as key-value pairs in a definition list layout.

### Badge and Status Viewers

- **shui:BadgeViewer** — Renders values as colored badge pills. Use `shui:badgeColors` to map values to colors.
- **shui:StatusViewer** — Displays enumerated status values with color-coded indicators (e.g., green/yellow/red).
- **shui:TagListViewer** — Shows multiple values as a horizontal row of tag chips.
- **shui:PriorityViewer** — Renders priority levels with appropriate icons and colors (high/medium/low).
- **shui:SeverityViewer** — Displays severity indicators (critical/warning/info) with standard iconography.

### Special Purpose Viewers

- **shui:EmailViewer** — Displays email addresses as `mailto:` hyperlinks with email icon.
- **shui:PhoneViewer** — Renders phone numbers as `tel:` hyperlinks with phone icon.
- **shui:URLViewer** — Shows URLs as clickable hyperlinks with optional favicon display.
- **shui:ColorSwatchViewer** — Displays color codes as a colored square swatch alongside the hex/RGB value.
- **shui:PasswordViewer** — Shows password fields as masked dots (••••••) with optional reveal toggle.
- **shui:CopyableViewer** — Displays text with a “copy to clipboard” button alongside.
- **shui:CountViewer** — Shows counts with singular/plural label handling (e.g., “1 item” vs “5 items”).
- **shui:BlankNodeViewer** — Renders blank node identifiers in a user-friendly format or displays contained properties inline.
- **shui:ReificationViewer** — Displays RDF-star quoted triples or reified statement metadata.

### Formatting Viewers

- **shui:InlineViewer** — Lays out multiple values horizontally inline rather than stacked vertically.
- **shui:HiddenViewer** — Suppresses display of the property entirely (for internal/system fields).
- **shui:ReadOnlyViewer** — Standard display with visual indication that the field is not editable.
- **shui:TooltipViewer** — Shows abbreviated content with full value available in hover tooltip.
- **shui:TruncatedViewer** — Displays long text truncated with ellipsis and “show more” expansion.
- **shui:HighlightedViewer** — Renders content with syntax or keyword highlighting.
- **shui:DiffViewer** — Shows value changes with additions/deletions highlighted (for version comparison).

### Computed/Derived Viewers

- **shui:ComputedViewer** — Displays values derived from `sh:values` rules with a computed/calculated indicator.
- **shui:InferredViewer** — Shows inferred values with visual distinction from asserted data.
- **shui:ExpressionViewer** — Renders SPARQL or other expression results with source attribution.
- **shui:AggregateViewer** — Displays aggregated values (sum, count, average) computed from related data.

---

### Common companion properties for viewers:

- `shui:dateFormat` — Date/time display format pattern
- `shui:decimalPlaces` — Precision for numeric display
- `shui:width` / `shui:height` — Dimensions for media viewers
- `shui:maxLength` — Truncation threshold for text display
- `shui:labelProperty` — Override property used for label resolution
- `shui:fallback` — Alternative viewer if primary fails
- `shui:emptyValue` — Text to display when value is absent (e.g., “Not specified”)
- `shui:locale` — Locale for number/date formatting
- `shui:badgeColors` — Color mappings for badge/status viewers

### Editing SHACL 1.2 Forms

The Editor form is a bit more complex:

```markup
# -----------------------------------------------------------------------------
# Address Editor Shape (Editable Form)
# -----------------------------------------------------------------------------

ex:AddressEditorShape a sh:NodeShape ;
    sh:targetClass schema:PostalAddress ;
    rdfs:label "Address Editor" ;
    rdfs:comment "Editable form for a postal address" ;
    sh:closed false ;
    
    sh:property ex:AddressEditor-label ;
    sh:property ex:AddressEditor-streetAddress ;
    sh:property ex:AddressEditor-addressLocality ;
    sh:property ex:AddressEditor-addressRegion ;
    sh:property ex:AddressEditor-postalCode ;
    sh:property ex:AddressEditor-addressCountry ;
    sh:property ex:AddressEditor-addressType ;
    sh:property ex:AddressEditor-isPrimary ;
    sh:property ex:AddressEditor-validFrom ;
    sh:property ex:AddressEditor-deliveryInstructions .

ex:AddressEditor-label a sh:PropertyShape ;
    sh:path rdfs:label ;
    sh:name "Address Label" ;
    sh:description "A friendly name for this address (e.g., 'Home', 'Work')" ;
    sh:order 0 ;
    sh:datatype xsd:string ;
    sh:maxCount 1 ;
    shui:propertyRole shui:LabelRole ;
    shui:editor shui:TextFieldEditor .

ex:AddressEditor-streetAddress a sh:PropertyShape ;
    sh:path schema:streetAddress ;
    sh:name "Street Address" ;
    sh:description "Street name, number, unit/apartment" ;
    sh:order 1 ;
    sh:datatype xsd:string ;
    sh:minCount 1 ;
    sh:maxCount 1 ;
    sh:minLength 5 ;
    sh:maxLength 200 ;
    shui:editor shui:TextAreaEditor .

ex:AddressEditor-addressLocality a sh:PropertyShape ;
    sh:path schema:addressLocality ;
    sh:name "City" ;
    sh:description "City or town name" ;
    sh:order 2 ;
    sh:datatype xsd:string ;
    sh:minCount 1 ;
    sh:maxCount 1 ;
    sh:minLength 2 ;
    sh:maxLength 100 ;
    shui:editor shui:TextFieldEditor .

ex:AddressEditor-addressRegion a sh:PropertyShape ;
    sh:path schema:addressRegion ;
    sh:name "State/Province" ;
    sh:description "Select state or province" ;
    sh:order 3 ;
    sh:datatype xsd:string ;
    sh:minCount 1 ;
    sh:maxCount 1 ;
    # US States enum
    sh:in ( "AL" "AK" "AZ" "AR" "CA" "CO" "CT" "DE" "FL" "GA" 
            "HI" "ID" "IL" "IN" "IA" "KS" "KY" "LA" "ME" "MD" 
            "MA" "MI" "MN" "MS" "MO" "MT" "NE" "NV" "NH" "NJ" 
            "NM" "NY" "NC" "ND" "OH" "OK" "OR" "PA" "RI" "SC" 
            "SD" "TN" "TX" "UT" "VT" "VA" "WA" "WV" "WI" "WY" "DC" ) ;
    shui:editor shui:EnumSelectEditor .

ex:AddressEditor-postalCode a sh:PropertyShape ;
    sh:path schema:postalCode ;
    sh:name "ZIP Code" ;
    sh:description "5-digit or 9-digit ZIP code" ;
    sh:order 4 ;
    sh:datatype xsd:string ;
    sh:minCount 1 ;
    sh:maxCount 1 ;
    sh:pattern "^[0-9]{5}(-[0-9]{4})?$" ;
    sh:message "Please enter a valid ZIP code (e.g., 97403 or 97403-1234)" ;
    shui:editor shui:TextFieldEditor .

ex:AddressEditor-addressCountry a sh:PropertyShape ;
    sh:path schema:addressCountry ;
    sh:name "Country" ;
    sh:description "Select country" ;
    sh:order 5 ;
    sh:class schema:Country ;
    sh:minCount 1 ;
    sh:maxCount 1 ;
    shui:editor shui:AutoCompleteEditor .

ex:AddressEditor-addressType a sh:PropertyShape ;
    sh:path ex:addressType ;
    sh:name "Address Type" ;
    sh:description "Type of address" ;
    sh:order 6 ;
    sh:class ex:AddressType ;
    sh:maxCount 1 ;
    shui:editor shui:InstancesSelectEditor .

ex:AddressEditor-isPrimary a sh:PropertyShape ;
    sh:path ex:isPrimary ;
    sh:name "Primary Address" ;
    sh:description "Mark as primary/default address" ;
    sh:order 7 ;
    sh:datatype xsd:boolean ;
    sh:maxCount 1 ;
    shui:editor shui:BooleanSelectEditor .

ex:AddressEditor-validFrom a sh:PropertyShape ;
    sh:path ex:validFrom ;
    sh:name "Valid From" ;
    sh:description "Date this address became effective" ;
    sh:order 8 ;
    sh:datatype xsd:date ;
    sh:maxCount 1 ;
    shui:editor shui:DatePickerEditor .

ex:AddressEditor-deliveryInstructions a sh:PropertyShape ;
    sh:path ex:deliveryInstructions ;
    sh:name "Delivery Instructions" ;
    sh:description "Special instructions for package delivery" ;
    sh:order 9 ;
    sh:datatype rdf:langString ;
    sh:maxCount 1 ;
    sh:singleLine false ;
    shui:editor shui:TextAreaWithLangEditor .
```

![](https://substackcdn.com/image/fetch/$s_!lcMr!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffe0f8390-ef6c-4234-adb0-1a292c3c451b_900x1300.png)

## Shui Editors

There are a significant number of SHACL 1.2 Editors, and it should be noted that such editors may also be extended by vendor-specific output:

Here’s a comprehensive list of `shui:editor` values for SHACL-UI form generation:

### Text Editors

- **shui:TextFieldEditor** — Single-line text input for short strings. Use with `shui:singleLine true`. Supports `shui:placeholder` for hint text.
- **shui:TextAreaEditor** — Multi-line text input for longer content. Configure rows with `shui:rows`. Suitable for descriptions, notes, addresses.
- **shui:TextFieldWithLangEditor** — Single-line text input with language tag selector dropdown (e.g., “en”, “de”, “ja”). For `rdf:langString` values.
- **shui:TextAreaWithLangEditor** — Multi-line text input with language tag selector. For longer multilingual content.
- **shui:RichTextEditor** — WYSIWYG HTML editor with formatting toolbar (bold, italic, lists, links). Outputs HTML or Markdown.
- **shui:CodeEditor** — Syntax-highlighted code input with line numbers. Often supports `shui:language` for highlighting mode (e.g., “sparql”, “turtle”, “javascript”).
- **shui:MarkdownEditor** — Markdown-aware text editor with preview pane. May include formatting toolbar.

### Numeric Editors

- **shui:IntegerEditor** — Numeric input restricted to integers. May include increment/decrement buttons. Respects `sh:minInclusive` / `sh:maxInclusive`.
- **shui:DecimalEditor** — Numeric input for decimal values. Configurable precision via `shui:decimalPlaces`.
- **shui:SliderEditor** — Horizontal slider for numeric ranges. Requires `sh:minInclusive` and `sh:maxInclusive` to define bounds.
- **shui:SpinnerEditor** — Numeric input with up/down arrow buttons for incremental adjustment.
- **shui:PercentageEditor** — Numeric input formatted as percentage (0-100 or 0.0-1.0). May display % suffix.
- **shui:CurrencyEditor** — Numeric input with currency symbol prefix/suffix. Configure via `shui:currencyCode`.

### Selection Editors

- **shui:EnumSelectEditor** — Dropdown for selecting from `sh:in` enumerated values. Use `shui:enumLabels` for human-readable labels.
- **shui:AutoCompleteEditor** — Type-ahead search dropdown. Queries instances of `shui:rootClass` using `shui:searchProperty` for matching.
- **shui:InstanceSelectEditor** — Dropdown listing all instances of the expected class. For selecting existing resources by IRI.
- **shui:InstancesSelectEditor** — Multi-select version allowing multiple instance selections. Returns a list of IRIs.
- **shui:RadioButtonsEditor** — Radio button group for mutually exclusive choices. Best for small `sh:in` lists (≤5 options).
- **shui:CheckboxGroupEditor** — Checkbox group for multi-select from enumerated values.
- **shui:TreeSelectEditor** — Hierarchical tree picker for selecting from taxonomies or class hierarchies. Uses `shui:rootClass` as tree root.
- **shui:ListBoxEditor** — Scrollable list for selection. Supports single or multi-select modes.

### Boolean Editors

- **shui:CheckboxEditor** — Simple checkbox toggle for `xsd:boolean` values.
- **shui:BooleanSelectEditor** — Dropdown with Yes/No or True/False options. Useful when a null/unset state is meaningful.
- **shui:ToggleSwitchEditor** — iOS-style on/off toggle switch. Visual alternative to checkbox.

### Date and Time Editors

- **shui:DatePickerEditor** — Calendar popup for selecting dates (`xsd:date`). Configure format with `shui:dateFormat`.
- **shui:TimePickerEditor** — Time selector for `xsd:time` values. May be 12-hour or 24-hour format.
- **shui:DateTimePickerEditor** — Combined date and time picker for `xsd:dateTime`.
- **shui:DateRangeEditor** — Dual calendar picker for selecting start/end date ranges.
- **shui:YearMonthPickerEditor** — Simplified picker for `xsd:gYearMonth` (no day selection).
- **shui:DurationEditor** — Input for `xsd:duration` values (e.g., “P1Y2M3D”). May use structured fields for years/months/days.

### IRI and URI Editors

- **shui:URIEditor** — Text input validated for URI/IRI syntax. May include protocol prefix selector.
- **shui:URILookupEditor** — URI input with external lookup/resolution capability. Validates that URI exists.
- **shui:PrefixedURIEditor** — Input supporting CURIE format (e.g., `schema:Person`). Expands using declared prefixes.
- **shui:ResourceLinkEditor** — Specialized IRI editor with “browse” button to navigate to the linked resource.

### File and Media Editors

- **shui:FileUploadEditor** — File picker with upload capability. Configure `shui:acceptedMimeTypes` for filtering.
- **shui:ImageUploadEditor** — Image-specific upload with preview thumbnail. May include cropping tools.
- **shui:ImageURLEditor** — URL input for external images with inline preview.
- **shui:MediaEditor** — Upload or URL input for audio/video with embedded player preview.
- **shui:DocumentUploadEditor** — File upload for documents (PDF, DOCX, etc.) with icon preview.

### Structured Data Editors

- **shui:NestedObjectEditor** — Inline form for editing a nested/blank node. Renders the target shape’s properties within an expandable panel.
- **shui:SubFormEditor** — Full sub-form for complex nested objects. Similar to NestedObjectEditor but always expanded.
- **shui:JSONEditor** — Raw JSON editor with syntax highlighting and validation. For `rdf:JSON` or complex embedded data.
- **shui:XMLEditor** — XML editor with syntax highlighting. For `rdf:XMLLiteral` values.
- **shui:KeyValueEditor** — Dynamic key-value pair editor for map-like structures.
- **shui:ListEditor** — Ordered list editor with add/remove/reorder controls. For `rdf:List` values.
- **shui:SetEditor** — Unordered collection editor. For multi-valued properties without ordering.

### Specialized Editors

- **shui:ColorPickerEditor** — Visual color selector with hex/RGB output. For color code strings.
- **shui:GeoPointEditor** — Map-based coordinate picker for latitude/longitude. Outputs WKT or GeoJSON.
- **shui:GeoRegionEditor** — Map-based polygon/region editor for geographic boundaries.
- **shui:PasswordEditor** — Masked text input for sensitive values. Shows dots instead of characters.
- **shui:EmailEditor** — Text input with email validation and mailto: link support.
- **shui:PhoneEditor** — Phone number input with formatting and country code support.
- **shui:URLEditor** — URL input with validation and “open in new tab” button.
- **shui:StarRatingEditor** — 1-5 star clickable rating input. For numeric rating values.
- **shui:TagsEditor** — Token-based multi-value input (type and press enter to add tags).
- **shui:CRONEditor** — Specialized editor for CRON expressions with helper UI.
- **shui:RegexEditor** — Regular expression editor with test/match preview.
- **shui:SPARQLEditor** — SPARQL query editor with syntax highlighting and prefix auto-completion.

### Read-Only / Display Editors

- **shui:ReadOnlyEditor** — Displays value as non-editable text. For computed or system-managed fields.
- **shui: HiddenEditor** — Field exists in form data but is not rendered. For internal/technical properties.
- **shui:LabelOnlyEditor** — Shows only the field label with no input. For section headers or informational text.

### Composite Editors

- **shui:BlankNodeEditor** — Creates and edits anonymous blank nodes inline. Combines NestedObjectEditor with auto-generation.
- **shui:ReificationEditor** — Editor for RDF-star quoted triples or traditional reification patterns.
- **shui:AnnotationEditor** — Specialized editor for adding annotations/metadata to statements.

---

### Common companion properties:

- `shui:placeholder` — Hint text shown when empty
- `shui:rows` — Number of rows for TextAreaEditor
- `shui:width` — “short”, “medium”, “long”, or pixel value
- `shui:readonly` — Make editor non-editable
- `shui:disabled` — Disable the input entirely
- `shui:rootClass` — Target class for instance lookups
- `shui:searchProperty` — Property to search on for autocomplete
- `shui:enumLabels` — Human-readable labels for enum values
- `shui:dateFormat` — Date display format pattern
- `shui:acceptedMimeTypes` — File type restrictions for uploads

## Implementing SHACL 1.2 UI

At the time of this writing, there are no tools for explicitly generating SHACL 1.2 UI (the spec itself is still in active development). This will likely change as the specification approaches completion. However, there are several implementations based on the older `dash:` namespace that can be used to start working with RDF-based UI:

### Active Implementations

**Commercial:**

- **TopBraid EDG/Composer** — The most mature implementation. Full support for `dash:editor`, `dash:viewer`, property groups, nested forms, and custom widgets. This is the reference implementation for DASH-based form generation.

**Open Source (Active):**

- **Kurrawong/shacl-ui** — Work-in-progress TypeScript implementation targeting the DASH vocabulary. Building a Storybook demo. (github.com/Kurrawong/shacl-ui)
- **ULB-Darmstadt/shacl-form** — HTML5 web component that generates forms from SHACL shapes. Supports plugins, theming, and validation. Has a live demo. (github.com/ULB-Darmstadt/shacl-form)
- **Shaperone** — Form generation library focused on Hydra+SHACL for hypermedia APIs. Can dynamically load data from SPARQL endpoints.

**Research/Academic:**

- **Schímatos** — SHACL-based web form generator for knowledge graph editing. Published at ISWC 2020. Includes shacl-form-react npm package (though last updated 2021).
- **CSIRO shacl-form** — Python-based HTML form generator from SHACL shapes.

### Practical Recommendation

If you want to use SHACL-driven UI generation today, replace `shui:` with `dash:` in the shapes file. The property names are largely similar since I based the hypothetical `shui:` vocabulary on DASH conventions. The DASH vocabulary documentation at **datashapes.org/forms.html** provides comprehensive guidance on form generation that current tools actually implement.

In general, there are several ways to implement such editors. In web applications, this can be facilitated using Node.js components or inline <script> elements that load both the data source and the SHACL as graphs.

These can also be used in line with multimodal agent interfaces, which would make it possible to bring up RDF-based SHACL scripts within a pane that could then generate (and update) the RDF back into a triple store, making it a powerful tool for quickly building up data content directly within chats or as part of an agentic services framework. Because this is purely declarative and deterministic, it can also be used in conjunction with other data stores, such as JSON or XML files, Excel spreadsheets, or inline PDFs.

**One final note:** This is a significant evolutionary step forward for presenting web content, in great part because it is built on a principle that was evident to me in the XForms do, but I think is becoming even more critical now:

> We are now at a stage where data is becoming responsible not only for its content but also for its presentation. Autogenerating forms and displays via LLMs is expensive, is error-prone, and still requires too much supervision. You are generating each form each time it gets displayed, and that display is inconsistent.
> 
> On the other hand, you need generate RDF forms only once (and they can be intuited fairly readily based on datatypes and similar shape structures), but once such SHACL UI schemas are generated, they can be reused again and again with a variety of data, because they are purely deterministic. The cheapest tokens are the ones you don’t need to generate in the first place.

I’m excited about SHACL 1.2 UI. I think it will shift the relationship that we have with data in significant ways.

*Disclosure: Some of the content for this article was generated by Claude Opus 4.5, but it was subsequently manually curated.*

In Media Res,

![](https://substackcdn.com/image/fetch/$s_!S4Bj!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9fd2b306-27a3-46f9-985b-4038d8a66f49_2688x1536.jpeg)

[Kurt Cagle](https://linkedin.com/in/kurtcagle)  
[The Ontologist](https://ontologist.substack.com/)

Check out my LinkedIn newsletter, [The Cagle Report](https://www.linkedin.com/newsletters/the-cagle-report-6672594836610252800/).

I am also currently seeking new projects or work opportunities. If anyone is looking for a CTO or Director-level AI/Ontologist, please get in touch with me through my Calendly:

If you want to shoot the breeze or have a cup of virtual coffee, I have a Calendly account at [https://calendly.com/theCagleReport](https://calendly.com/theCagleReport). I am available for consulting and full-time work as an ontologist, AI/Knowledge Graph guru, and coffee maker. Also, for those of you whom I have promised follow-up material, it’s coming; I’ve been dealing with health issues of late.

I’ve created a [Ko-fi account](https://ko-fi.com/E1E117YF5K) for voluntary contributions, either one-time or ongoing, or you can subscribe directly to [The Ontologist](https://ontologist.substack.com/). If you value my articles, technical pieces, or general reflections on work in the 21st century, please consider contributing to support my work and allow me to continue writing.