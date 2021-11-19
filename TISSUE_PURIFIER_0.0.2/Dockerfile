# The image corresponding to this dosckerfile can be obtained by 
#docker pull us.gcr.io/broad-dsde-methods/pyro_matplotlib:0.0.7

FROM nvidia/cuda:11.3.1-base-centos8

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


#----------- PIP INSTALLS -------------
RUN yes | pip3 install torch==1.10.0+cu113 torchvision==0.11.1+cu113 torchaudio==0.10.0+cu113 -f https://download.pytorch.org/whl/cu113/torch_stable.html
RUN yes | pip3 install -U psutil 
RUN yes | pip3 install -U matplotlib  
RUN yes | pip3 install -U scikit-image 
RUN yes | pip3 install -U neptune-client 
RUN yes | pip3 install -U python-igraph  
RUN yes | pip3 install -U leidenalg 
RUN yes | pip3 install -U Pillow  
RUN yes | pip3 install -U pyro-ppl 
RUN yes | pip3 install -U ipython 
RUN yes | pip3 install -U pyyaml
RUN yes | pip3 install -U scikit-learn
RUN yes | pip3 install -U pytorch-lightning
RUN yes | pip3 install -U umap-learn
RUN yes | pip3 install -U torchmetrics
RUN yes | pip3 install -U pandas
RUN yes | pip3 install -U google-cloud-storage
RUN yes | pip3 install -U scanpy

