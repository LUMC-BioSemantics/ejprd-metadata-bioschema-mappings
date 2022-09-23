![GitHub](https://img.shields.io/github/license/ejp-rd-vp/resource-metadata-schema)
![GitHub tag (latest by date)](https://img.shields.io/github/v/tag/ejp-rd-vp/resource-metadata-schema)
![GitHub tag (funder)](https://img.shields.io/badge/funder-EJP%20RD-brightgreen)

# ejprd-metadata-bioschema-mappings
This repository contains the mappings between the [EJPRD metadata model](https://github.com/ejp-rd-vp/resource-metadata-schema) and the bioschemas.org model.

### The mapping
The mapping file contains both OWL-based mappings and SKOS-based mappings. The latter is used to provide a more accurate semantic to the mappings, as some OWL-based mappings (e.g., owl:sameAs) might be too strict. Still, we maintained the OWL-based mappings to provide an automatic machine-actionable translation of the EJP RD metadata resources to bioschema.org concepts.


### Demo
We hosted the mapping files and some of the EJPRD resources metadata in this [triplestore](http://178.63.49.197:7300/) under the repository `ejprd-metadata-model-mappings`. Below you can find examples of `SPARQL` queries that make use of these mappings.

**Note:** The SPARQL queries below are written from the `schema.org/bioschema` perspective. So the concepts and properties related to the `schema.org/bioschema` are shown in the queries.


##### Get datasets and its properties

```SPARQL
PREFIX schema: <https://schema.org/>

SELECT DISTINCT ?dataset ?name ?theme WHERE { 
	?dataset a schema:Dataset;
    	schema:name ?name;
     	schema:about ?theme.
}

```  


##### Get catalogs and its properties

```SPARQL
PREFIX schema: <https://schema.org/>

SELECT DISTINCT ?catalog ?name WHERE { 
	?catalog a schema:Dataset;
    	schema:name ?name.
}
```  


##### Get patient registry and its properties

```SPARQL
PREFIX schema: <https://schema.org/>
PREFIX ejprd: <http://purl.org/ejp-rd/vocabulary/>

SELECT DISTINCT ?patient_registry ?name ?theme WHERE { 
	?patient_registry a schema:Thing, ejprd:PatientRegistry;
    	schema:name ?name;
     	schema:about ?theme.
}
```  
**Note:** In this query we used both `schema.org/bioschema` and `ejprd` concepts to retrieve patient registry resources. This approach is required since we can only map `ejprd:Patient Registry` concept to the generic `schema:Thing` concept.



##### Get biobank and its properties

```SPARQL
PREFIX schema: <https://schema.org/>
PREFIX ejprd: <http://purl.org/ejp-rd/vocabulary/>

SELECT DISTINCT ?biobank ?name ?theme WHERE { 
	?biobank a schema:Thing, ejprd:Biobank;
    	schema:name ?name;
     	schema:about ?theme.
}
```  
**Note:** In this query we used both `schema.org/bioschema` and `ejprd` concepts to retrieve patient registry resources. This approach is required since we can only map `ejprd:Biobank` concept to the generic `schema:Thing` concept.
