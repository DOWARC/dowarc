Removed cloned concepts:
- dcterms:Collection
- dc:date
- dc:title
- terms:contributor
- terms:creator
- terms:language
- terms:license
- terms:publisher
- pav:authoredBy
- pav:contributedBy
- pav:createdBy
- pav:hasCurrentVersion
- pav:hasEarlierVersion
- pav:hasVersion
- pav:importedFrom
- pav:previousVersion
- frbr:Endeavour
- frbr:Expression
- frbr:Item
- frbr:Manifestation
- frbr:Work
- <http://www.loc.gov/premis/rdf/v3/Agent>
- <http://www.loc.gov/premis/rdf/v3/Event>
- <http://www.loc.gov/premis/rdf/v3/HardwareAgent>
- <http://www.loc.gov/premis/rdf/v3/IntellectualEntity>
- <http://www.loc.gov/premis/rdf/v3/Object>
- <http://www.loc.gov/premis/rdf/v3/Organization>
- <http://www.loc.gov/premis/rdf/v3/Person>
- <http://www.loc.gov/premis/rdf/v3/SoftwareAgent>
- <http://www.openarchives.org/ore/terms/Proxy>
- <http://www.w3.org/2004/03/trix/rdfg-1/Graph>
- prov:Activity
- prov:Agent
- prov:Entity
- prov:Organization
- prov:value
- prov:wasDerivedFrom
- foaf:Agent
- foaf:Organization
- foaf:Person
- <http://xmlns.com/foaf/spec/#term_Organization>
- <https://www.ica.org/standards/RiC/ontology#Activity>
- <https://www.ica.org/standards/RiC/ontology#Agent>
- <https://www.ica.org/standards/RiC/ontology#Instantiation>
- <https://www.ica.org/standards/RiC/ontology#RecordResource>
- <https://www.ica.org/standards/RiC/ontology#Thing>
- <https://www.openarchives.org/ore/terms/AggregatedResource>

Fixed:
- `@prefix premis: <http://www.loc.gov/premis/rdf/v3/>`

Removed further namespace prefixes

----------

Remove:

```
ore:aggregates
    a owl:ObjectProperty ;
    rdfs:domain dowarc:WARCcoll, dowarc:WARCfile, dowarc:WARCrecord ;
    rdfs:range dowarc:WARCrecordElement .

ore:isAggregatedBy
    a owl:ObjectProperty ;
    rdfs:domain dowarc:WARCrecordElement ;
    rdfs:range dowarc:WARCcoll, dowarc:WARCfile, dowarc:WARCrecord .
```

note: express domain and range with subclasses

```
ore:describes
    a owl:ObjectProperty ;
    rdfs:domain dowarc:WARCgraph .

ore:isDescribedBy
    a owl:ObjectProperty ;
    rdfs:domain dowarc:WARCcoll, dowarc:WARCfile, dowarc:WARCrecord ;
    rdfs:range dowarc:WARCgraph .
```

note: express domain with subclasses

```
ore:proxyIn
    rdfs:range dowarc:WARCfile, dowarc:WARCrecord .

```

note: express range with subclasses

```
ore:similarTo
    rdfs:domain dowarc:WARCcoll .
```

note: express domain with subclasses

```
pav:curatedBy
    a owl:ObjectProperty ;
    rdfs:domain dowarc:WARCcoll ;
    rdfs:range foaf:Organization, foaf:Person, dowarc:WebArchivingAgent .
```

note: its a subproperty of pav:contributedBy which is a subproperty of prov:wasAttributedTo which has domain prov:Entity and range prov:Agent. With dowarc:WebArchivingAgent beeing a subclass of prov:Agent and foaf:Agent this should be sufficient.

```
pav:retrievedBy
    a owl:ObjectProperty ;
    rdfs:comment "An entity responsible for retrieving the data from an external source. The retrieving agent is usually a software entity, which has done the retrieval from the original source without performing any transcription. The source that was retrieved should be given with pavretrievedFrom. The time of the retrieval should be indicated using pavretrievedOn. See pavimportedFrom for a discussion of import vs. retrieve vs. derived." ;
    rdfs:domain dowarc:WARCrecordElement ;
    rdfs:isDefinedBy <http://purl.org/pav/> ;
    rdfs:range dowarc:SoftwareAgent ;
    rdfs:subPropertyOf prov:wasAttributedTo .
```

note: its a sub property of prov:wasAttributedTo which has domain prov:Entity and range prov:Agent. Aligning dowarc:WARCrecordElement as subclass of prov:Entity and having dowarc:WebArchivingAgent as subclass of prov:Agent should be enough.

```
pav:derivedFrom
    a owl:ObjectProperty ;
    rdfs:comment "Derived from a different resource. Derivation conserns itself with derived knowledge. If this resource has the same content as the other resource, but has simply been transcribed to fit a different model (like XML -\"RDF or SQL -\"CVS), use pavimportedFrom. If a resource was simply retrieved, use pavretrievedFrom. If the content has however been further refined or modified, pavderivedFrom should be used. Details about who performed the derivation (e.g. who did the refining or modifications) may be indicated with pavcontributedBy and its subproperties." ;
    rdfs:domain dowarc:Derivative ;
    rdfs:isDefinedBy "http://purl.org/pav/" ;
    rdfs:range dowarc:WARCfile, dowarc:WARCgraph, dowarc:WARCrecord ;
    rdfs:subPropertyOf prov:wasDerivedFrom .

pav:retrievedFrom
    a owl:ObjectProperty ;
    rdfs:comment "The URI where a resource has been retrieved from. The retrieving agent is usually a software entity, which has done the retrieval from the original source without performing any transcription. Retrieval indicates that this resource has the same representation as the original resource. If the resource has been somewhat transformed, use pavimportedFrom instead. The time of the retrieval should be indicated using pavretrievedOn. The agent may be indicated with pavretrievedBy." ;
    rdfs:domain dowarc:WARCrecordElement ;
    rdfs:isDefinedBy "http://purl.org/pav/" ;
    rdfs:label "Retrieved from" ;
    rdfs:subPropertyOf prov:wasDerivedFrom .
```

note: its a subclass of prov:wasDerivedFrom, which has domain prov:Entity and range prov:Entity.dowarc:Derivative, dowarc:WARCfile, dowarc:WARCgraph, and dowarc:WARCrecord are all aligned with prov:Entity.

```
prov:generated
    rdfs:domain dowarc:WARCevent ;
    rdfs:range dowarc:Derivative, dowarc:WARCfile, dowarc:WARCgraph, dowarc:WARCrecord .

prov:used
    rdfs:domain dowarc:WARCevent ;
    rdfs:range dowarc:Derivative, dowarc:Identifier, dowarc:WARCfile, dowarc:WARCgraph, dowarc:WARCrecord, dowarc:WARCrecordElement .

prov:wasGeneratedBy
    rdfs:domain dowarc:WARCcdxFile, dowarc:WARCfile, dowarc:WARCrecord, dowarc:WARCrecordElement ;
    rdfs:range dowarc:WARCevent .
```

note: dowarc:WARCevent is a subclass of prov:Activity and dowarc:Derivative, dowarc:WARCcdxFile, dowarc:WARCfile, dowarc:WARCgraph, dowarc:WARCrecord, dowarc:WARCrecordElement, and dowarc:Identifier are all aligned with prov:Entity.

----------

Remove probably unwanted `rdfs:isDefinedBy` statements