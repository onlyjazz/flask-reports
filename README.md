# flask-reports
Report generator

This repository includes folders with yaml files.

Each customer should have 1 folder like customer name.

The customer folder's yaml files includes flask customer reports definitions.

Each customer can have a few yaml files.

## yaml file structure should be like this:

1. customer id
2. model
3. template id
4. report meta data

data-extracts repository API (getReportData) will read the file (by file path) and return the study data according to report definition.

## For now there are 6 report templates:

1. subject_event_variables
2. subject_events_variable_pairs_with_filters
3. subject_variables
4. subject_date_time_variables
5. site_events_count_data_missing
6. site_event_count_subjects

Documentation: https://docs.google.com/document/d/13frwgcR4UK18NRBwmKIuVHV6zVw_FlzSHUbbYz5G6Z8/edit#

## Example of report metadata for each template:
1. {'db': 'rlf100', 'crf': 'Assessment of Respiratory Failure', 'items': ['RSRUTIDAT', 'SHOCKDAT', 'MORGNFLDAT', 'RENAL', 'CARDIO', 'NEUROLOGICAL', 'HEPATIC','HEMATOLOGIC']}
2. {'db': 'rlf100', 'items': [{'name':'DIABP','condition':'<','threshold':'60'},{'name':'MORGNFL','condition':'=','threshold':'1'},{'name':'SHOCKYN','condition':'=','threshold':'1'}]}
3. {'db': 'rlf100', 'items': [['DIABP','MORGNFL'],'SHOCKYN',['CMTRT','CMONGO']]}
4. {'db': 'v280', 'crf': 'Bowel movement diary','items': ['BM1', ['BM1_TIME','BM2_TIME','BM3_TIME'], ['BM1_COMPLETE_EVACUATION','BM2_COMPLETE_EVACUATION'], ['BM1_DIGITAL_MANEUVER','BM2_DIGITAL_MANEUVER']]}
5. {'db': 'rlf100', 'events': ['D1', 'D2', 'D3', 'D4']}
6. {'db': 'rlf100', 'events': ['D1', 'D2', 'D3', 'D4']}
 
