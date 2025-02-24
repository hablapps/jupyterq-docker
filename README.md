# Dockerized Jupyter environment for kdb+/q

This repository provides a Dockerized Jupyter environment for kdb+/q,
integrating [embedPy](https://github.com/KxSystems/embedPy) and
[JupyterQ](https://github.com/KxSystems/jupyterq) for interactive development
with Jupyter notebooks. ## Configure and run

## Setup and Usage

### Prerequisites

Before building the Docker container, you need to manually download the required
q binaries and license file from Kx Systems. You should start by downloading the
q release and license file from the link you
received from kx. 

1. Obtain the q distribution (`l64.zip`) and license file (`kc.lic`) from the
   link provided by Kx Systems. ### Build and run
2. Place both files inside the `docker/assets/` directory.

### Build and Run

Now you can build and run the container with the jupyter environment.

```bash
docker build -t jupyterq
docker run -v ./notebooks:/home/kdb/notebooks -p 8888:8888 --rm jupyterq
```

- The `notebooks` directory on the host machine is mounted as a volume at the 
  jupyter lab's root folder. This allows you to persist your work across 
  container restarts.
- The container exposes Jupyter on port `8888`.
- The `--rm` flag ensures that the container is removed after stopping it. If
  you want persistent state for the container, remove this flag.


### Accessing jupyter

Once the container is running, open your browser and navigate to
`http://localhost:8888`. 

*DANGER*: Jupyter is configured to run without authentication so no password is
required. Only run this container in local and if you are behind some firewall.
