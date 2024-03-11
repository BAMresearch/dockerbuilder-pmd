FROM jupyter/scipy-notebook:python-3.11.8 

USER root

# Add bam77 to config
RUN conda config --add channels bam77

# Add gmsh shared libs
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y libgl1 libxcursor-dev libxft2 libx11-dev libxinerama-dev
RUN apt install -y libxext6 git libgl1-mesa-dev xvfb

# Install conda requirements from the requirements_conda.txt file
COPY --chown=${NB_UID}:${NB_GID} requirements_conda.txt /tmp/
RUN mamba install -v --yes --file /tmp/requirements_conda.txt && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

