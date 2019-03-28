ARG BASE_CONTAINER=ykawagishi/test01
FROM $BASE_CONTAINER

LABEL maintainer=y.kawagishi@bitgroove.jp

USER root

# Install all OS dependencies for fully functional notebook server
RUN apt-get update && apt-get install -yq --no-install-recommends \
    build-essential \
    vim \
    git \
    netcat \
    pandoc \
    python-dev \
    tzdata \
    unzip \
    nano \
    curl \
    && rm -rf /var/lib/apt/lists/*

USER $NB_UID

RUN conda install --quiet -y -c conda-forge jupyter_contrib_nbextensions && \
    conda clean -tipy

# Install NII Jupyter-LC_run_through plugin
RUN pip --no-cache-dir install git+https://github.com/NII-cloud-operation/Jupyter-LC_wrapper
RUN python -m lc_wrapper.ipython.install
RUN python -m lc_wrapper.bash.install

RUN pip --no-cache-dir install git+https://github.com/NII-cloud-operation/Jupyter-LC_run_through
RUN pip --no-cache-dir install git+https://github.com/NII-cloud-operation/Jupyter-multi_outputs 
RUN pip --no-cache-dir install git+https://github.com/NII-cloud-operation/Jupyter-LC_index
RUN pip --no-cache-dir install git+https://github.com/NII-cloud-operation/Jupyter-i18n_cells
RUN pip --no-cache-dir install git+https://github.com/NII-cloud-operation/Jupyter-LC_nblineage


RUN jupyter nbextension install --py lc_wrapper --user
RUN jupyter nbextension install --py lc_multi_outputs --user
RUN jupyter nbextension install --py lc_run_through --user
RUN jupyter nbextension install --py nblineage --user
RUN jupyter nbextension install --py nbextension_i18n_cells --user
RUN jupyter nbextension install --py notebook_index --user


# RUN jupyter run-through quick-setup
RUN jupyter nbextension enable --py lc_wrapper --py --user
RUN jupyter nbextension enable --py lc_multi_outputs --user
RUN jupyter nbextension enable --py lc_run_through --user
RUN jupyter nbextension enable --py nblineage --user
RUN jupyter nbextension enable --py nbextension_i18n_cells --user
RUN jupyter nbextension enable --py notebook_index --user

USER root
RUN echo "c.MultiKernelManager.kernel_manager_class = 'lc_wrapper.LCWrapperKernelManager'" >> /etc/jupyter/jupyter_notebook_config.py

# Switch back to jovyan to avoid accidental container runs as root
USER $NB_UID
