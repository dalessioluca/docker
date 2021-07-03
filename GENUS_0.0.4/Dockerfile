# The image corresponding to this dosckerfile can be obtained by 

FROM nvidia/cuda:11.1.1-base-ubuntu18.04

LABEL mainteiner="Luca Dalessio <ldalessi@broadinstitute.org>"

# System packages 
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
RUN apt-get update && apt-get install -y --no-install-recommends sudo

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    curl \
    ca-certificates 

RUN sudo apt-get install -y --no-install-recommends \
    git \
    bzip2 \
 && sudo rm -rf /var/lib/apt/lists/* \
 && curl -so ~/miniconda.sh https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh \
 && chmod +x ~/miniconda.sh \
 && ~/miniconda.sh -b -p /home/user/miniconda \
 && rm ~/miniconda.sh
# Put conda command on our path
ENV PATH=/home/user/miniconda/bin:$PATH
ENV CONDA_AUTO_UPDATE_CONDA=false
ENV DOCKER='true'

#----------- CONDA INSTALLS -------------
RUN conda create -n genus python=3.8
RUN conda activate genus

RUN conda install -y pytorch==1.9.0 torchvision==0.10.0 torchaudio==0.9.0 cudatoolkit=11.1 -c pytorch -c conda-forge \
 && conda clean -ya

RUN conda install -c nvidia -c rapidsai -c numba -c conda-forge cugraph cudatoolkit=11.1 \
 && conda clean -ya

RUN conda install -c anaconda psutil \
 && conda clean -ya

#----------- PIP INSTALLS --------------
RUN yes | pip install matplotlib==3.4.2
RUN yes | pip install scikit-image==0.18.1
RUN yes | pip install neptune-client==0.9.19
RUN yes | pip install dill==0.3.4
#RUN yes | pip install python-igraph==0.9.6
RUN yes | pip install Pillow==8.2.0
RUN yes | pip install pyro-ppl==1.6.0
RUN yes | pip install ipython==7.25.0
RUN yes | pip install pyyaml==5.4.1
