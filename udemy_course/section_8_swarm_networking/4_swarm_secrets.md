# Swarm secrets

* Store secrets in swarm

* Secrets like username, password, TLS certificates and keys, SSH Keys

* Docker secrets can store strings/binary content up to 500KB

* Swarm raft db is encrypted on the disk on the manager nodes. Managers and workers already have a secure control plane.

* Through the secure control plane, secrets flow down from managers to workers.

* Secrets are stored **in-memory file system** on the worker nodes where the containers are spawned.

* In-memory location `/run/secrets/<secret_name>` or `/run/secrets/<secret_alias>`

* In stack configuration, we can specify what services should access what secrets.

* In compose environment also we can use **file based secrets**(not secure). This should be used for development purposes only.

```Bash
# Value can be read from a file or STDIN
docker secret create <secret_name> <file|STDIN>

docker secret ls
```

* Secrets can be passed to docker service

```Bash
docker service create --name psql --secret psql_pass -e POSTGRES_PASSWORD_FILE=/run/secrets/psql_pass postgres:9.4
```

* Secrets can be added or removed from a container dynamically using the `docker service update` command.

```Bash
docker service update --secret-rm <secret_name>
```

## Secrets in swarm stack

* Secrets are supported from **version 3.1 of the configuration file**

```YAML
version: "3.1"
services:
  psql:
    image: postgres
    # This container can access only the below listed secrets
    secrets:
      - psql_user
      - psql_password
    environment:
      POSTGRES_PASSWORD_FILE: /run/secrets/psql_password
      POSTGRES_USER_FILE: /run/secrets/psql_user

secrets:
  psql_user:
    # If secrets were created using CLI, use
    # the external key and provide the secret name
    file: ./psql_user.txt
  psql_password:
    file: ./psql_password.txt
```

* In production placing secrets in files is not recommended.

---

## References

* [Docker Secrets](https://docs.docker.com/engine/swarm/secrets/)
