# biomarkers

> *a journey of a thousand miles begins with a single step* -- Laozi

This repository exists to collect information about (initially) metabolite biomarkers.
Originally, I was going for metabolite-disease biomarker relationships, but it turns out
there is also literature with process-metabolite relationships, like biomarkers for
coffee consumption. The are modelled similarly.

All content in this repository is available as CCZero. If you like to contribute, please make a
fork, make changes, and send me a pull request. By making a pull request, you make all content
in the pull request avaiable as CCZero too.

Attribution to this data collection can, at this momoment, be made to this GitHub repository:

    Willighagen, E.L., 2016, Biomarkers, GitHub, Available from https://github.com/egonw/biomarkers/

Additionally, a (future) data deposition can be cited.

## data depositions

For every 100 biomarker-disease or biomarker-process relationships a data deposition will be created,
probably at Figshare.

## data model

Data from every separate data source is placed in a separate data file (in the Turtle format).
The files are structured such that changes are mostly centered around single lines; that explains
why the ; to seperate triples is expected to be found at the start of a line.

The data model itself is very much in flux and should be considered alpha. Additional triples
are most welcome, though metabolite information is supposed to be stored in Wikidata and not
reproduced here. Federated queries will allow linking things together.

### namespaces

    @prefix : <http://egonw.github.com/biomarkers/> .
    @prefix wd: <http://www.wikidata.org/entity/> .
    @prefix umls: <http://bioportal.bioontology.org/ontologies/umls/> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix omim: <http://bio2rdf.org/omim:> .
    @prefix doi: <http://dx.doi.org/> .
    @prefix cito: <http://purl.org/spar/cito/> .
    @prefix void: <http://rdfs.org/ns/void#> .
    @prefix dcterms: <http://purl.org/dc/terms/> .
    @prefix chebi: <http://purl.obolibrary.org/obo/CHEBI_> .
    @prefix ncit: <http://ncicb.nci.nih.gov/xml/owl/EVS/Thesaurus.owl#> .

### the data set

The data set is described with a minimal bit of VoID content, linking the data set to the source
of the information, using a DOI IRI:

    :Blau a void:Dataset ;
      cito:citesAsDataSource <http://dx.doi.org/10.1007/978-3-642-40337-8_1> .

Any additional detail is welcome, but not expected.

Metabolites, diseases, and processes are typed using a classes from ontologies, e.g.
metabolite are typed with the 'molecule' class from the ChEBI ontology, and diseases
with a class from the NCIT ontology.

### metabolites

Metabolites are identified by their Wikidata IRI and most come with a rdfs:label. For example:

    wd:Q408256 rdfs:label "biopterin" ;
      a chebi:25367 .

### causes

Various causes are supported, like diseases (and/or disorders) and processes, like consumption.

#### diseases

Diseases are identified by their UMLS IRI and most come with a rdfs:label. For example:

    umls:C0268467 a ncit:C7057 ; 
      rdfs:label "GTP cyclohydrolase deficiency" .

If no UMLS IRI is available, then OMIM can be used:

    omim:264070 a ncit:C7057 ; 
      rdfs:label "pterin-4a-carbinoamine dehydratase deficiency" .

### biomarkers

Biomarker information is linked to a metabolite via the http://egonw.github.com/biomarkers/bioMarker
predicate. BioMarkers are so far anynomous and untyped classes. Each biomaker is further linked
to a disease. Annotation with up or downregulatation is strongly encouraged, but currently not
worked out in schema form yet.

An example:

    wd:Q408256 rdfs:label "biopterin"
      ; :bioMarker [ :for umls:C0268467
        ; :observedIn :U, :CSF, :DBS
      ]

The annotation where the biomarker is observed is not strictly required, but experimentally
important. Sometimes changes only happen in one fluid.

#### biomarker concentration change

The change itself is not formally modelled and the data uses various approaches. The reason
for this is that the data sources use different approaches. This may be formalized at some
future point.
