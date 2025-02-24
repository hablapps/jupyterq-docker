FROM python:3.13

ENV QHOME=/opt/q
ENV PATH="${QHOME}/l64:${PATH}"
ENV NOTEBOOK_DIR=/home/kdb/notebooks

RUN apt update && apt install -y wget unzip
RUN pip install --upgrade pip

RUN mkdir -p ${QHOME}
WORKDIR ${QHOME}

COPY assets/l64.zip ${QHOME}/
COPY assets/kc.lic ${QHOME}

RUN unzip l64.zip && \
    rm l64.zip && \
    chmod +x l64/q

WORKDIR /home/kdb

RUN wget https://github.com/KxSystems/embedPy/releases/download/1.5.0/embedPy_linux-1.5.0.tgz && \
    mkdir -p embedPy_linux && \
    tar -xvzf embedPy_linux-1.5.0.tgz -C embedPy_linux && \
    mv embedPy_linux/p.q embedPy_linux/p.k /opt/q/ &&\
    mv embedPy_linux/l64/p.so /opt/q/l64 &&\
    rm -rf embedPy_linux embedPy_linux-1.5.0.tgz

RUN wget https://github.com/KxSystems/jupyterq/releases/download/1.1.14/jupyterq_linux-1.1.14.tgz &&\
    mkdir -p jupyterq && \
    tar -xvzf jupyterq_linux-1.1.14.tgz -C jupyterq &&\
    rm -rf jupyterq_linux-1.1.14.tgz

RUN pip install -r jupyterq/requirements.txt && jupyterq/install.sh

RUN useradd kdb &&\
    chown -R kdb:kdb /home/kdb

USER kdb

RUN jupyter kernelspec install --user /home/kdb/jupyterq/kernelspec\
    && rm -rf jupyterq

EXPOSE 8888

CMD jupyter lab \
    --ip=0.0.0.0 \
    --no-browser \
    --ServerApp.root_dir="${NOTEBOOK_DIR}" \
    --NotebookApp.token='' \
    --NotebookApp.allow_origin='*'
