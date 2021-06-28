# The image corresponding to this dosckerfile can be obtained by 
#docker pull us.gcr.io/broad-dsde-methods/pyro_matplotlib:0.0.7

FROM rapidsai/rapidsai:21.06-cuda11.1-runtime-ubuntu18.04-py3.7

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
RUN conda install -y pytorch torchvision torchaudio cudatoolkit=11.1 -c pytorch -c nvidia \
 && conda clean -ya

RUN conda install -c anaconda psutil \
 && conda clean -ya

#----------- PIP INSTALLS --------------
RUN yes | pip install matplotlib
RUN yes | pip install scikit-image
RUN yes | pip install neptune-client
RUN yes | pip install dill
RUN yes | pip install python-igraph
RUN yes | pip install Pillow
RUN yes | pip install pyro-ppl
RUN yes | pip install ipython
RUN yes | pip install pyyaml
