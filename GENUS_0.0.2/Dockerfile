# The image corresponding to this dosckerfile can be obtained by 
#docker pull us.gcr.io/broad-dsde-methods/pyro_matplotlib:0.0.7

FROM nvidia/cuda:11.1.1-base-ubuntu18.04

MAINTAINER Luca Dalessio <ldalessi@broadinstitue.org>
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


#----------- CONDA INSTALLS -------------

# CUDA 11.1 specific steps
RUN conda install -y pytorch==1.8.1 torchvision torchaudio cudatoolkit=11.1 -c pytorch -c conda-forge \
 && conda clean -ya

RUN conda install -c anaconda psutil \
 && conda clean -ya

#----------- PIP INSTALLS --------------
RUN yes | pip install matplotlib==3.4.1
RUN yes | pip install scikit-image==0.18.0
RUN yes | pip install neptune-client==0.9.1
RUN yes | pip install dill==0.3.3
RUN yes | pip install python-igraph==0.9.1
RUN yes | pip install leidenalg==0.8.3
RUN yes | pip install Pillow==8.2.0
RUN yes | pip install pyro-ppl==1.6.0
RUN yes | pip install ipython==7.22.0
RUN yes | pip install pyyaml==5.3.1
