# biomarkers

This repository exists to collect information about (initially) metabolite biomarkers. All content
in this repository is available as CCZero. If you like to contribute, please make a fork, make
changes, and send me a pull request. By making a pull request, you make all content in the pull
request avaiable as CCZero too.

## data model

Data from every separate data source is placed in a separate data file (in the Turtle format).
The files are structured such that changes are mostly centered around single lines; that explains
why the ; to seperate triples is expected to be found at the start of a line.

The data model itself is very much in flux and should be considered alpha. Additional triples
are most welcome, though metabolite information is supposed to be stored in Wikidata and not
reproduced here. Federated queries will allow linking things together.

### metabolites

Metabolites are identified by their Wikidata IRI and most come with a rdfs:label. For example:

    wd:Q408256 rdfs:label "biopterin" .

### diseases

Diseases are identified by their UMLS IRI and most come with a rdfs:label. For example:

    umls:C0268467 rdfs:label "GTP cyclohydrolase deficiency" .

### biomarkers

Biomarker information is linked to a metabolite via the http://egonw.github.com/biomarkers/bioMarker
predicate. BioMarkers are so far anynomous and untyped classes. Each biomaker is further linked
to a disease. Annotation with up or downregulatation is strongly encouraged, but currently not
worked out in schema form yet.

An example:

    wd:Q408256 rdfs:label "biopterin"
      ; :bioMarker [ :for umls:C0268467
    ]

