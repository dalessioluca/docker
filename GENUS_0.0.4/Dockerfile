FROM rapidsai/rapidsai:cuda10.2-base-ubuntu18.04-py3.8

LABEL mainteiner="Luca Dalessio <ldalessi@broadinstitue.org>"

# Install some basic utilities
RUN apt-get update && apt-get install -y \
    curl \
    ca-certificates \
    sudo \
    git \
    bzip2 \
    libx11-6 \
 && rm -rf /var/lib/apt/lists/*

# Create a working directory
RUN mkdir /app
WORKDIR /app

# Create a non-root user and switch to it
RUN adduser --disabled-password --gecos '' --shell /bin/bash user \
 && chown -R user:user /app
RUN echo "user ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/90-user
USER user

# All users can use /home/user as their home directory
ENV HOME=/home/user
RUN chmod 777 /home/user

# Install Miniconda and Python 3.8
ENV CONDA_AUTO_UPDATE_CONDA=false
ENV PATH=/home/user/miniconda/bin:$PATH
RUN curl -sLo ~/miniconda.sh https://repo.continuum.io/miniconda/Miniconda3-py38_4.8.2-Linux-x86_64.sh \
 && chmod +x ~/miniconda.sh \
 && ~/miniconda.sh -b -p ~/miniconda \
 && rm ~/miniconda.sh \
 && conda install -y python==3.8.1 \
 && conda clean -ya

#----------- CONDA INSTALLS -------------
# CUDA 10.2 specific steps
RUN conda install -y pytorch==1.9.0 torchvision==0.10.0 torchaudio==0.9.0 cudatoolkit=10.2 -c pytorch \
 && conda clean -ya


RUN conda install -c anaconda psutil \
 && conda clean -ya

#----------- PIP INSTALLS --------------
RUN yes | pip install matplotlib==3.4.2
RUN yes | pip install scikit-image==0.18.1
RUN yes | pip install neptune-client==0.9.19
RUN yes | pip install dill==0.3.4
RUN yes | pip install python-igraph==0.9.6
RUN yes | pip install Pillow==8.2.0
RUN yes | pip install pyro-ppl==1.6.0
RUN yes | pip install ipython==7.25.0
RUN yes | pip install pyyaml==5.4.1

ENV DOCKER='true'


# Set the default command to python3
CMD ["python3"]
