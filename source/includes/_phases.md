# Phases

##### Endpoint: `/api/v1/projects/<project_id>/phases`

Phase is a subclass of [Project](#projects) which is a subclass of Assignable. You will see the id refering to a project as assignable_id in other models. A Phase always has a `parent_id` set to the id of the parent Project.

## List Phases for a Project

```
GET /api/v1/projects/<project_id>/phases
 curl 'https://api.rm.smartsheet.com/api/v1/projects/[project_id]/phases?auth=...'
```

## Create a Phase for a Project

```
curl  -d "phase_name=Winding%20up&starts_at=2013-09-15&ends_at=2013-09-16"  \
                         "https://api.rm.smartsheet.com/api/v1/projects/[project_id]/phases?auth=..."
```

## Update a Phase for a Project

```
curl  -XPUT -d "phase_name=Another%20Name&"  \
                         "https://api.rm.smartsheet.com/api/v1/projects/[project_id]/phases/456?auth=..."
```

### Bill Rates
If you wish for the phase to inherit the parent project's bill rates after create, the `use_parent_bill_rates` flag can be passed with a `PUT` request as follows:

```
curl  -XPUT -d "use_parent_bill_rates=true"  \
                         "https://api.rm.smartsheet.com/api/v1/projects/[project_id]/phases/456?auth=..."
```


## Delete a Phase for a Project

```
curl  -i -X DELETE "https://api.rm.smartsheet.com/api/v1/projects/[project_id]/phases/[phase_id]?auth=..."
```
NOTE: A phase cannot be deleted unless it contains no assignments.
