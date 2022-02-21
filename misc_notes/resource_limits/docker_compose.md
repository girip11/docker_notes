# Docker compose limits

## Docker swarm

```YAML
# docker swarm
services:
  service:
    image: nginx
    deploy:
        resources:
            limits:
              cpus: 0.50
              memory: 512M
            reservations:
              cpus: 0.25
              memory: 128M
```

## Docker compose

```yaml
services:
  nginx:
    image: nginx
    mem_limit: 512m
    mem_reservation: 128M
    cpus: 0.5
    ports:
      - "80:80"
```
