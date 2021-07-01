# Using secrets with docker compose

* Remember docker compose is only for development environment.

* Below configuration works in compose environment as well.

```YAML
version: "3.1"

services:
  psql:
    image: postgres
    secrets:
      - psql_user
      - psql_password
    environment:
      POSTGRES_PASSWORD_FILE: /run/secrets/psql_password
      POSTGRES_USER_FILE: /run/secrets/psql_user

secrets:
  psql_user:
    file: ./psql_user.txt
  psql_password:
    file: ./psql_password.txt
```

* Secrets works in compose but only in **file mode**. **external** key is not supported.

* The secret file is bind mounted in compose environment. Support to secrets in compose make the development environment match the production environment behavior.
