FROM pyiron/pyiron:latest

USER $DOCKER_UIDs
WORKDIR $HOME
ARG PYTHON_VERSION=default

RUN conda config --add channels bam77

COPY . ${HOME}/
RUN mamba env update -n base -f ${HOME}/environment.yml && \
    mamba clean --all -f -y && \
    mamba list

USER root
ENV NOTEBOOK_DIR=${HOME}/notebooks_pyiron
RUN chmod +x ${HOME}/include_notebooks.sh && \
    /bin/bash include_notebooks.sh &&\
    fix-permissions $CONDA_DIR && \
    fix-permissions ${HOME}

# Switch back to pyiron to avoid accidental container runs as root
USER $DOCKER_UID

WORKDIR $HOME
