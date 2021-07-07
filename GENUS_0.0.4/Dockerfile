# The image corresponding to this dosckerfile can be obtained by 
#docker pull us.gcr.io/broad-dsde-methods/genus:0.0.4

FROM rapidsai/rapidsai-core:cuda10.2-base-ubuntu18.04-py3.8

LABEL mainteiner="Luca Dalessio <ldalessi@broadinstitute.org>"

RUN /bin/bash -c ". activate rapids && \
    pip install torch torchvision torchaudio && \
    pip install psutil && \
    pip install matplotlib==3.4.2 && \
    pip install scikit-image==0.18.1 && \
    pip install neptune-client==0.9.19 && \
    pip install dill==0.3.4 && \
    pip install Pillow==8.3.0 && \
    pip install pyro-ppl==1.6.0 && \
    pip install ipython==7.25.0 && \
    pip install pyyaml==5.4.1"

ENV PATH=/opt/conda/envs/rapids/bin:$PATH
ENV CONDA_AUTO_UPDATE_CONDA=false
ENV DOCKER='true'
