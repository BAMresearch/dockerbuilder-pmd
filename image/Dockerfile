# FROM quay.io/jupyter/base-notebook
FROM jupyter/base-notebook:python-3.10.11

USER root

# Add bam77 to config
RUN conda config --add channels bam77

# Add gmsh shared libs
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y libgl1 libxcursor-dev libxft2 libx11-dev libxinerama-dev
RUN apt install -y libxext6 git

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

RUN git clone https://github.com/tpaviot/pythonocc-utils.git

RUN pip install ./pythonocc-utils && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"
