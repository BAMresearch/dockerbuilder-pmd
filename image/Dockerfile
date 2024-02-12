# FROM quay.io/jupyter/base-notebook
FROM jupyter/base-notebook:python-3.10.11

# Add bam77 to config
RUN conda config --add channels bam77

# Add gmsh shared libs
RUN sudo apt-get install -y ffmpeg libsm6 libxext6

# Install conda requirements from the requirements_conda.txt file
COPY --chown=${NB_UID}:${NB_GID} requirements_conda.txt /tmp/
RUN mamba install -v --yes --file /tmp/requirements_conda.txt && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install pip requirements from the requirements_pip.txt file
COPY --chown=${NB_UID}:${NB_GID} requirements_pip.txt /tmp/
RUN pip install --no-cache-dir --requirement /tmp/requirements_pip.txt && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"
