# Unused Projects
This script will scan Rally/Agile Central projects and look for artifacts that have been modified in the last 60 days.  If it doesn't find anything it reports that project as unused.

The number of days can be configured via the "lookback" variable in the script.  Change it to anything that is more appropriate for you.


### Installation:
`pip install requests`

`pip install pyral`

### Usage:
`python unused_projects.py --server=<hostname> --user=<login ID> --password=<password> --workspace="<workspace>"`


### Output:
We print the project's ObjectID with the project name since it is possible to have two projects with the same name.  This helps to differentiate the project.
```
214424394628: 22 Sub 2 has no modifications within the last 60 days
220855613084: Permission Test has no modifications within the last 60 days
225197623164: HP ALM has no modifications within the last 60 days
230629220304: Tools GIS Kanban Work has no modifications within the last 60 days
230629991164: Blah has no modifications within the last 60 days
274659201916: Blah has no modifications within the last 60 days
```
