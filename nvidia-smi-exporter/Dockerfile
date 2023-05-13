FROM nvidia/dcgm-exporter:3.1.7-3.1.4-ubuntu20.04

#RUN echo "Acquire::Check-Valid-Until \"false\";\nAcquire::Check-Date \"false\";" | cat > /etc/apt/apt.conf.d/10no--check-valid-until
#
#RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys A4B469963BF863CC

ENV TARGET='deb http://developer.download.nvidia.com'
ENV REP = 'deb [by-hash=no] http://developer.download.nvidia.com'
RUN sed -i "s/${TARGET}/${REP}/g" /etc/apt/sources.list

RUN apt-get update

RUN apt install -y ca-certificates --fix-missing

RUN update-ca-certificates




RUN apt-get install wget -y \
    && wget -qO- https://get.docker.com | sh \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

COPY nvidia-smi-ps /usr/local/bin
COPY nvidia-smi-exporter /usr/local/bin

RUN chmod +x /usr/local/bin/nvidia-smi-*

ENTRYPOINT [ "nvidia-smi-exporter" ]