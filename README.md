# Dockerized JupyterQ

This repository provides a dockerized Jupyter environment for kdb+/q
using [JupyterQ](https://github.com/KxSystems/jupyterq).

This Docker image serves as a replacement for the unmaintained official
[JupyterQ image](https://hub.docker.com/r/kxsys/jupyterq) ( last updated 3 years
ago). Its definition follows the manual installation steps for JupyterQ and it's
not inspired in the original JupyterQ Dockerfile.

This repository does not include any software distributed by *Kx Systems*—it
only provides a Dockerfile to build the environment using the required files.
You must obtain the q distribution and license from *Kx Systems* before building
the container. You shouldn't distribute the built image, as it contains
proprietary software that requires a license from Kx Systems. 

## Setup and Usage

### Prerequisites

Before building the Docker container, you need to manually download the required
q binaries and license file from Kx Systems. You should start by downloading the
q release and license file from the link you
received from kx. 

1. Obtain the q distribution (`l64.zip`) and license file (`kc.lic`) from the
   link provided by Kx Systems.
2. Place both files inside the `assets` directory.

### Build and Run

Now you can build and run the container with the Jupyter environment.

```bash
docker build -t jupyterq
docker run -v ./notebooks:/home/kdb/notebooks -p 8888:8888 --rm jupyterq

# you can also use docker compose
docker compose build
docker compose up
```

- The `notebooks` directory on the host machine is mounted as a volume at the 
  JupyterLab's root folder. This allows you to persist your work across 
  container restarts.
- The container exposes Jupyter on port `8888`.
- The `--rm` flag ensures that the container is removed after stopping it. If
  you want persistent state for the container, remove this flag.


### Accessing jupyter

Once the container is running, open your browser and navigate to
`http://localhost:8888`. 

*Warning*: Jupyter is configured without authentication. Do not expose this
container to the internet. Use it only in a local and secure environment, behind
a firewall.
