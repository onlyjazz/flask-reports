# flask-reports
# Report generator Rev 1.0

## Introduction
Reports are defined using YAML files.  The YAML files are stored in this public Git repository in folders.

The folder naming convention is CustomerName, where CustomerName is the name chosen at time of registration. 

The CustomerName can be viewed and modified by logging into app.flaskdata.io in the Customer Profile in the hamburger icon by the Customer Admin role.

## Writing reports using YAML syntax
For Flask Reports, nearly every YAML file has a list of CDASH items or EDC events. Each item in the list is a list of key/value pairs, commonly called a “hash” or a “dictionary”. So, we need to know how to write lists and dictionaries in YAML.

There’s a small quirk to YAML. All YAML files (regardless of their association with Flask Reports or not) can optionally begin with --- and end with .... This is part of the YAML format and indicates the start and end of a document.

Let's do an example:
>
> ---
> # Report for Assessment of Respiratory Failure
> model: PG
> template: subject_event_variables
> report:
>   db: rlf100
>   crf: Assessment of Respiratory Failure
> # CDASH variable names from the annotated CRF
>    items:
>      - RSRUTIDAT
>      - SHOCKDAT
>      - MORGNFLDAT
>      - RENAL
>      - CARDIO
>      - NEUROLOGICAL
>      - HEPATIC
>      - HEMATOLOGIC
> ...


YAMLLint
YAML Lint (http://www.yamllint.com/) helps you debug YAML syntax if you are having problems

That’s all you really need to know about YAML to start writing Flask Reports.

#

data-extracts repository API (getReportData) will read the file (by file path) and return the study data according to report definition.

## Version 1.0 supports 6 report templates:

1. subject_event_variables
2. subject_events_variable_pairs_with_filters
3. subject_variables
4. subject_date_time_variables
5. site_events_count_data_missing
6. site_event_count_subjects

Documentation: https://docs.google.com/document/d/13frwgcR4UK18NRBwmKIuVHV6zVw_FlzSHUbbYz5G6Z8/edit#

## TB deprecated
## Example of report metadata for each template:
1. {'db': 'rlf100', 'crf': 'Assessment of Respiratory Failure', 'items': ['RSRUTIDAT', 'SHOCKDAT', 'MORGNFLDAT', 'RENAL', 'CARDIO', 'NEUROLOGICAL', 'HEPATIC','HEMATOLOGIC']}
2. {'db': 'rlf100', 'items': [{'name':'DIABP','condition':'<','threshold':'60'},{'name':'MORGNFL','condition':'=','threshold':'1'},{'name':'SHOCKYN','condition':'=','threshold':'1'}]}
3. {'db': 'rlf100', 'items': [['DIABP','MORGNFL'],'SHOCKYN',['CMTRT','CMONGO']]}
4. {'db': 'v280', 'crf': 'Bowel movement diary','items': ['BM1', ['BM1_TIME','BM2_TIME','BM3_TIME'], ['BM1_COMPLETE_EVACUATION','BM2_COMPLETE_EVACUATION'], ['BM1_DIGITAL_MANEUVER','BM2_DIGITAL_MANEUVER']]}
5. {'db': 'rlf100', 'events': ['D1', 'D2', 'D3', 'D4']}
6. {'db': 'rlf100', 'events': ['D1', 'D2', 'D3', 'D4']}
 
