# dockerized jupyter environment for kdb+/q

## Configure and run

### Prerequisites

You should start by downloading the q release and license file from the link you
received from kx. Once you have them you should save them in the `docker/assets`
folder as `l64.zip` and `kx.lic`.

Now you can build and run the container with the jupyter environment.

```bash
# using docker command
docker build -t jupyterq
docker run -v ./notebooks:/home/kdb/notebooks -p 8888:8888 --rm jupyterq
```

The `notebooks` folder will be mounted as a docker volume into jupyter lab roots
folder.
