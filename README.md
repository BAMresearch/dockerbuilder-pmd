# dockerbuilder-pmd

Repo for building docker images for the BAM PMD server in Github actions

## Setup guide for gui applications following [jupyterhub-deploy-docker](https://github.com/jupyterhub/jupyterhub-deploy-docker)

### docker-compose.yml: Set DISPLAY env variable in the jupyterhub server

```yaml
services:
   ...
   environment:
      ...
      DISPLAY: $(DISPLAY)
   ...
```

### jupyterhub_config.yml: Bind X11 directory in each user-container using Dockerspawner config and pass the Display variable

```python
...
c.DockerSpawner.volumes = {
   ...
   "/tmp/.X11-unix": "/tmp/.X11-unix"
}

c.DockerSpawner.environment = {
   "DISPLAY": os.environ["DISPLAY"],
   "QT_X11_NO_MITSHM": "1"
}

```
