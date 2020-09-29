# The image corresponding to this dosckerfile can be obtained by 
#docker pull us.gcr.io/broad-dsde-methods/pyro_matplotlib:0.0.6

FROM nvidia/cuda:10.2-base-ubuntu18.04

# Install curl and sudo and git and bzip2 and miniconda
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    curl \
    ca-certificates \
    sudo \
 && sudo apt-get install -y --no-install-recommends \
    git \
    bzip2 \
    vim \
 && sudo rm -rf /var/lib/apt/lists/* \
 && curl -so ~/miniconda.sh https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh \
 && chmod +x ~/miniconda.sh \
 && ~/miniconda.sh -b -p /home/user/miniconda \
 && rm ~/miniconda.sh

# Put conda command on our path
ENV PATH=/home/user/miniconda/bin:$PATH
ENV CONDA_AUTO_UPDATE_CONDA=false

# Update conda and conda-build
RUN /home/user/miniconda/bin/conda update -n base -c defaults conda \
 && /home/user/miniconda/bin/conda update conda-build \
 && /home/user/miniconda/bin/conda clean -ya

# Create a Python 3.6 environment
RUN /home/user/miniconda/bin/conda create -y --name py385 python=3.8.5 \ 
 && /home/user/miniconda/bin/conda clean -ya
ENV CONDA_DEFAULT_ENV=py385
ENV CONDA_PREFIX=/home/user/miniconda/envs/$CONDA_DEFAULT_ENV
ENV PATH=$CONDA_PREFIX/bin:$PATH

#----------- CONDA INSTALLS -------------

# CUDA 10.2-specific steps
RUN conda install -y pytorch==1.6.0 torchvision=0.7.0 cudatoolkit=10.2 -c pytorch \
 && conda clean -ya

# Install matplotlib from conda-forge
RUN conda install -y -c conda-forge matplotlib \
 && conda clean -ya

# Install skimage
RUN conda install -y -c conda-forge scikit-image \
 && conda clean -ya

#---------- PIP INSTALLS -------------

# Install pyro-ppl from PIP
RUN yes | pip install pyro-ppl==1.4.0
# && sudo rm -rf ~/.cache/pip

RUN yes | pip install plotly
RUN yes | pip install leidenalg 
RUN yes | pip install python-igraph 
RUN yes | pip install --upgrade Pillow

# Install dill which is a better version of pickle
RUN yes | pip install dill==0.3.2  

# Install neptune-client
RUN yes | pip install neptune-client
RUN yes | pip install neptune-contrib
