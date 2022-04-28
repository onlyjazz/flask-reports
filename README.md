# flask-reports
Report generator

This repository includes yaml files.

The yaml files includes customer flask reports definitions.

Each customer can have a few yaml files, each yaml file for each report.

yaml file structure should be like this:

1. customer id
2. model
3. template id
4.report meta data

data-extracts repository will read the file (by file name/ id) and return the study data according to report definition.
