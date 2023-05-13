FROM nvcr.io/nvidia/k8s/dcgm-exporter:3.1.7-3.1.4-ubuntu20.04

RUN rm /etc/apt/sources.list.d/cuda.list
RUN ls -l /etc/apt/sources.list.d/
RUN apt-key del 7fa2af80
RUN apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/3bf863cc.pub
RUN apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/7fa2af80.pub

RUN apt-get update

RUN apt install -y ca-certificates --fix-missing

RUN update-ca-certificates

RUN apt-get install wget -y \
    && apt-get install -y nvidia-container-toolkit \
    && wget -qO- https://get.docker.com | sh \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

COPY nvidia-smi-ps /usr/local/bin
COPY nvidia-smi-exporter /usr/local/bin

RUN chmod +x /usr/local/bin/nvidia-smi-*

ENTRYPOINT [ "nvidia-smi-exporter" ]