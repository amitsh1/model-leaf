ARG cuda_version=10.0
ARG cudnn_version=7

FROM nvidia/cuda:10.0-base-ubuntu16.04

COPY environment.yml /.
COPY entrypoint.sh /

RUN apt-get update && apt-get install -y \
	wget \
	vim \
	bzip2\
    libglib2.0-0\
    libsm6\
    libxext6\
    libxrender-dev

# Install Miniconda
RUN wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O Miniconda.sh && \
	/bin/bash Miniconda.sh -b -p /opt/conda && \
	rm Miniconda.sh

ENV PATH /opt/conda/bin:$PATH

#Install ANACONDA Environment
RUN conda env create -f environment.yml
RUN conda init bash
RUN echo "conda activate model-env" > ~/.bashrc

## Jupyter
EXPOSE 8888
## Tensorboard
EXPOSE 6006

ENTRYPOINT [ "/entrypoint.sh" ]