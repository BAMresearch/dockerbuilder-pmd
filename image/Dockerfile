FROM quay.io/jupyter/base-notebook

# Install from the requirements.txt file
COPY --chown=${NB_UID}:${NB_GID} requirements.yml /tmp/
RUN mamba install --yes --file /tmp/requirements.yml && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"
