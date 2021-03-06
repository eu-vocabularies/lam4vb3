# Initiative for Modeling the Legal Analysis Methodology

**Homepage**: [eu-vocaularies/lam4vb3](https://github.com/eu-vocabularies/lam4vb3)

The aim of the project is to provide a level of formalisation to the Legal Analise Methodology used at the European Publications Office for the legal document metadata. 

The formalisation steps are as follows: 
- from unstructured text (e.g. word files) to controlled tabular structure (e.g. Excel)
- from controlled tabular structure to a tailor made SKOS representation, called LAM-SKOS-AP
- from LAM-SKOS-AP representation to OWL2 formal ontology
- from LAM-SKOS-AP representation to a structured technical documentation and a user manual

  
| Key | Value |
| :--- | :--- | 
| Project start| June 2019 |
| Project expected end| December 2019 |
| Authors | Eugeniu Costetchi |
| Contributors | Juraj Kuba, Marcin Baryn |
 
 
# Project deliverables 

The project is split into two phases aiming at providing three kinds of deliverables: documents, transformation scripts and formal data/models. The originally planned deliverables are as follows. 

## Phase 1
| Key | Value |
| :--- | :--- | 
| Status | Finished |
| Expected delivery | October 2019|
| Delivered | 2nd of October 2019|

| Work package | Description |
| :--- | :--- |
|  WP1.1 | [(Doc1)](deliverables/wp1-1-ontology-requirements/main.pdf) Requirements specification - A preliminary requirement specification for LAM project (based on the preliminary analisys) |
|  WP1.2 | [(Model spec1)](deliverables/wp1-2-lam-skos-ap/main.pdf) LAM-SKOS-AP model - A model to structure LAM data suitable for loading into VocBench3 |
|  WP1.3 | [(Script1)](lam4vb3/excel2rdf.py) Excel to LAM-SKOS-AP transformation script  - A command line script to transform the Structured Excel files into LAM-SKOS-AP suitable for loading into VB3 |
|  WP1.4 | [(Doc2)](deliverables/wp1-4-excel-structure/main.pdf) Documentation of Excel structure - Specification of how the excel files should be structured in order to undergo the transformation, i.e. the description of the input data for the script. |
|  WP1.5 | [(Data1)](data) LAM data and loading it into VocBench 3 – Load and setup data in VocBench3 OP environment |

## Phase 2
| Key | Value |
| :--- | :--- |
|Status| ongoing |
|Expected delivery | December 2019| 


| Work package  | Description |
| :--- | :--- |
|  WP2.1 | [(BugFix1)](https://github.com/eu-vocabularies/lam4vb3/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aclosed) Bug fixes in LAM-SKOS-AP (errata) and transformation script (Script1) – based on the new findings |
|  WP2.2 | (Assistance1) Assistance/training for LAM team to edit data in VocBench3 |
|  WP2.3 | (Model spec2) Transformation rules from LAM-SKOS-AP data into formal LAM ontology and SHACL shapes |
|  WP2.4 | [(Script2)](deliverables/wp2-4-script-lam-skos-ap-2-owl) Script to transform LAM-SKOS-AP data into formal LAM OWL ontology  – the desired LAM ontology |
|  WP2.5 | [(Script3)](deliverables/wp2-5-script-lam-skos-ap-2-shacl) Script to transform LAM-SKOS-AP data into formal LAM SHACL shapes– the desired shapes for validation purposes |
|  WP2.6 | [(Script4)](lam2doc) Script to transform LAM-SKOS-AP data into a structured document (e.g. DITA) for PDF/HTML/DocBook disseminations |
|  WP2.7 | [(Data2)](deliverables/wp2-7-lam-ontology-data) test release of LAM OWL ontology |
|  WP2.8 | [(Data3)](deliverables/wp2-8-lam-shapes-data) test release of LAM SHACL shapes |
|  WP2.9 | [(Data4)](deliverables/wp2-9-lam-documentation-data) test release of LAM HTML documentation | 
|        | Example [LAM properties HTML](http://htmlpreview.github.io/?https://github.com/eu-vocabularies/lam4vb3/blob/master/deliverables/wp2-9-lam-documentation-data/lam_project_properties_v2/main.html)  |
|        | Example [LAM classes HTML](http://htmlpreview.github.io/?https://github.com/eu-vocabularies/lam4vb3/blob/master/deliverables/wp2-9-lam-documentation-data/lam_project_classes_v2/main.html) |


# Running the script Deliverable wp1.3  
  This script  transforms an Excel file (compliant to specification in wp1.4) into RDF representation structured according to LAM-SKOS-AP application profile (described in wp1.2). 

## Installation 

This transformation script is provided as a Jupyter Notebook. To run it is necessary to have Python 3.6+ installed along with [Jupyter Notebook](https://jupyter.org/install) or preferably [Jupyter Lab](https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html).

To install Jupyter Lab please refer to [the installation manual](https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html).  


In addition the libraries listed in the *requirements.txt* file should be installed by running the following command.  

```shell script
pip install -r ./requirements.txt
```

## Usage

Install the necessary dependecies.

```shell script
make install
```

Make sure that the TinkerPop server is running.

```shell script
make restart-gremlin
```

### Transformation pipeline

The Excel file constituting the input for the transformation is hardcoded in the Makefile as _INPUT_EXCEL_. If a new version is available, update the value of this variable.
 
To run all the transformations at once simply run 
```shell script
make transform-full
```

Transform Excel to RDF. 
```shell script
make clear
make transform-excel2rdf
```

Transform RDF to JSOn.
```shell script
make transform-rdf2json
```

Transform JSON to HTML. 
```shell script
make transform-json2html
```

### Uploading data into a development environment

The data can be uploaded into a dev environment at http://dev.meaningfy.ws:3030 triple-store. To do so automatically run

```shell script
make upload_to_fuseki_meaningfy_ws
```

### Running the Unit tests

```shell script
make test
```
 
### Jupyer notebook (outdated)
Run the Jupyter Lab and then execute all the cells in the notebook file *lam2vb3_v1.ipynb*.
The script, by default, searches for an excel file in the *./doc/semi-structured* folder and outputs RDF data in Turtle format in the *./output* folder. 

It is possible to modify the input/output parameters by updating the constants in the first cell. 
```Python
INPUT_FILE = 'path/to/the/file'
OUTPUT_FILE_LAM_PROPERTIES = 'path/to/the/file' 
OUTPUT_FILE_LAM_CLASSES = 'path/to/the/file'
OUTPUT_FILE_CELEX_CLASSES = 'path/to/the/file'
OUTPUT_FILE_CELEX_PROPERTIES = 'path/to/the/file'
``` 

###  Command line
It is possible to run the same transformation operation using the command line. To run it simply execute

```shell script
python ./lam4vb3/excel2rdf.py ./path/to/input/folder ./path/to/output/folder
```

This script takes all Excel files (*.xlsx) from an input folder, transforms them into LAM-SKOS-AP RDF and writes them 
into the output folder.
For example the following parameters shall generate complete output for *LAM_metadata_04_ECO.xlsx*: input *./doc/semi-structured* and output  *./output*. 

```shell script
python ./lam4vb3/excel2rdf.py ./docs/semi-structured/ ./output
```

After the processing each input file is moved into the output folder as well. Leaving the input folder clean.
This gives the possibility of installing a cron task to continuously monitor a particular input folder. 


