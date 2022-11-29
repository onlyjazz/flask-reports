# flask-reports
# Data management Report generator Rev 1.0

## What is Flask Reports?
Flask Reports is a Data management Report report generator for ClinCapture 2.x.  Currently it has been tested on ClinCapture 2.1 and 2.3
Flask Reports enable rapid development of online data tables to EDC databases.  We've taken a simple approach of using templates and YAML files to define reports instead of trying to make a complex UX/UI report generator.

## Introduction
Reports are defined using YAML files.  The YAML files are stored in this public Git repository in folders.

The folder naming convention is CustomerName, where CustomerName is the name chosen at time of registration.

The CustomerName can be viewed and modified by logging into app.flaskdata.io in the Customer Profile in the hamburger icon by the Customer Admin role.

## Writing reports using YAML syntax
For Flask Reports, nearly every YAML file has a list of CDASH items or EDC events. Each item in the list is a list of key/value pairs, commonly called a “hash” or a “dictionary”. So, we need to know how to write lists and dictionaries in YAML.

There’s a small quirk to YAML. All YAML files (regardless of their association with Flask Reports or not) can optionally begin with --- and end with .... This is part of the YAML format and indicates the start and end of a document.

YAMLLint
YAML Lint (http://www.yamllint.com/) helps you debug YAML syntax if you are having problems

That’s all you really need to know about YAML to start writing Flask Reports.

### What templates can I use?
1. subject_event_variables
2. subject_events_variable_pairs_with_filters
3. subject_variables
4. subject_date_time_variables
5. site_events_count_data_missing
6. site_event_count_subjects

## Got it. Now show me some examples so that I can try it out

### subject_event_variables - produce a listing of AE data
```
# AE.yml
model: pg
version: '2.1'
Name: Adverse Events
template: subject_event_variables
report:
  crf: Adverse Events
  items:
     - ADVERSE_EVENT_YESNO
     - ADVERSE_EVENT_START_DATE
     - ADVERSE_EVENT_COMPLICATION
     - ADVERSE_EVENT_OUTCOME
     - ADVERSE_EVENT_PROCEDURE_DEVICE_RELATED
```

### subject_events_variable_pairs_with_filters - show CRF item(s) in range in all events where it appears (good for treatment visits)
```
# EmptyICFDates.yml
# v2xx ClinCapture databases
model: pg
version: '2.1'
name: Informed Consent since 1970
template: subject_events_variable_pairs_with_filters
name:  ICF Dates
report:
  crf: Informed Consent
  items:
    - name: INFORMED_CONSENT_DATE
      condition: ">="
      threshold: '1970-01-01'
    - name: INFORMED_CONSENT_DATE
      condition: "<"
      threshold: '2022-01-01'
```
### subject_variables -- list items by subject
```
# ScreeningVisits.yml
model: pg
version: '2.1'
name: Dates screened
template: subject_variables
report:
  crf:
    - Date of Screening Visit
  items:
    - DATE_OF_SCREENING_VISIT
```

### subject_date_time_variables - show Event and data entry date-times
```
# WhenICFUpdated.yml
model: pg
version: '2.1'
name: ICF Dates
template: subject_date_time_variables
report:
  crf: Informed Consent
  items:
    - INFORMED_CONSENT_DATE
```

### site_events_count_data_missing - find missing required forms in visits/events
```
# MissingDatainDailyMeds.yml
model: pg
version: '2.1'
name: Missing data in daily meds
template: site_events_count_data_missing
report:
  events:
    - Daily meds
```
### site_event_count_subjects - Count patients in events, for example screening and EOS
```
# CountPatientsScreened.yml
model: pg
version: '2.1'
name: Screens and dropouts
template: site_event_count_subjects
report:
  events:
    - Screening
    - End of Study
```



## Run-time
At run-time, the data-extracts/getReportData API  reads the YAML file (using the /CustomerName file path) and returns the study data according to report definition.



Documentation: https://docs.google.com/document/d/13frwgcR4UK18NRBwmKIuVHV6zVw_FlzSHUbbYz5G6Z8/edit#
