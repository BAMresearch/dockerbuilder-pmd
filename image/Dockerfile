FROM pyiron/pyiron:latest

USER $DOCKER_UID

WORKDIR $HOME

# Add bam77 to config
RUN conda config --add channels bam77

# Install conda requirements from the requirements_conda.txt file
COPY --chown=${NB_UID}:${NB_GID} requirements_conda.txt /tmp/
RUN mamba install -v --yes --file /tmp/requirements_conda.txt && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}" 

WORKDIR $HOME
