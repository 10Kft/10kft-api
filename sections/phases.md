# Phases

##### Endpoint: `/api/v1/projects/<project_id>/phases`

Phase is a subclass of [Project](projects) which is a subclass of Assignable. You will see the id refering to a project as assignable_id in other models. A Phase always has a `parent_id` set to the id of the parent Project.

## List Phases for a Project

```
GET /api/v1/projects/<project_id>/phases
 curl 'https://vnext.10000ft.com/api/v1/projects/4/phases?auth=...'
```

## Create a Phase for a Project

```
curl  -d "phase_name=Winding%20up&starts_at=2013-09-15&ends_at=2013-09-16"  \
                         "https://vnext.10000ft.com/api/v1/projects/4/phases?auth=..."
```

## Update a Phase for a Project

```
curl  -XPUT -d "phase_name=Another%20Name&"  \
                         "https://vnext.10000ft.com/api/v1/projects/4/phases/456?auth=..."
```
