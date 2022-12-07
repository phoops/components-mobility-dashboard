# Local setup

## Mongo setup

Mongo comes with "admin" db only.

Setup a database and assign a user to authenticate with

```shell
docker compose exec -it mongo /bin/bash
mongo mongodb://root:example@mongo:27017/admin
```

In mongo

```shell
use dashboard
db.createUser(
  {
    user: "dashboardUser",
    pwd:  "dashboardPassword",   // or passwordPrompt()
    roles: [ { role: "readWrite", db: "dashboard" },
           ]
  }
)
```
