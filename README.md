# flask-reports
# Report generator Rev 1.0

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

## Got it. Now show me examples

### AE listing with subject_event_variables
    model: pg
    template: subject_event_variables
    report:
      crf: Adverse Events
      items:
         - ADVERSE_EVENT_YESNO
         - ADVERSE_EVENT_START_DATE
         - ADVERSE_EVENT_COMPLICATION
         - ADVERSE_EVENT_OUTCOME
         - ADVERSE_EVENT_PROCEDURE_DEVICE_RELATED

### Missing data in ePRO - with site_events_count_data_missing
    model: pg
    template: site_events_count_data_missing
    report:
      events:
        - Daily meds

### Dates of patient screening  - with subject_crf_item_values [Doesn't work]
    model: pg
    template: subject_crf_item_values
    report:
      crf:
        - Date of Screening Visit
      items:
        - DATE_OF_SCREENING_VISIT

### Count patients screened and completed Study
    model: pg
    template: site_event_subjects
    report:
      event:
        - Screening
        - End of Study

### When was ICF obtained? - with subject_crf_date_time_item_values
    model: pg
    template: subject_crf_date_time_item_values
    report:
      crf:
        - Informed Consent
      item:
        - INFORMED_CONSENT_DATE

## Run-time
At run-time, the data-extracts/getReportData API  reads the YAML file (using the /CustomerName file path) and returns the study data according to report definition.



Documentation: https://docs.google.com/document/d/13frwgcR4UK18NRBwmKIuVHV6zVw_FlzSHUbbYz5G6Z8/edit#
