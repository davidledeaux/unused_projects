import sys
import urllib3

from pyral import Rally, rallyWorkset

urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

options = [arg for arg in sys.argv[1:] if arg.startswith('--')]
args    = [arg for arg in sys.argv[1:] if arg not in options]
server, user, password, apikey, workspace, project = rallyWorkset(options)

rally = Rally(server, user, password, workspace=workspace, project=project, verify_ssl_cert=False)
rally.enableLogging(dest=b'unused_projects.log', attrget=True)

# Number of days that we look for work items
lookback = 60

# These are work item types that contain a LastUpdateDate that we can use
work_item_types = ["DefectSuite", "Defect", "HierarchicalRequirement", "Task", "TestCase"]


# Get all projects first
projects = rally.get("Project")

for project in projects:
    in_use = False
    for work_item_type in work_item_types:
        artifacts = rally.get(work_item_type, project=project.Name, query="(LastUpdateDate >= today-{lookback})".format(lookback=lookback))
        if artifacts.resultCount > 0:
            in_use = True        

    if in_use == False:
        print ("{object_id}: {name} has no modifications within the last {lookback} days".format(object_id=project.ObjectID, name=project.Name, lookback=lookback))
