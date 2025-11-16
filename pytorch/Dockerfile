ARG BASE_IMAGE="ghcr.io/jkminder/dlab-runai-images/base:master"

FROM ${BASE_IMAGE}

# install conda environment
COPY pytorch/environment.yml /tmp/environment.yml
COPY pytorch/requirements.txt /tmp/requirements.txt
RUN /opt/conda/bin/mamba env create -f /tmp/environment.yml -n default && \
    /opt/conda/bin/mamba clean -y --all
RUN rm /tmp/environment.yml

# install requirements
RUN . /opt/conda/etc/profile.d/conda.sh && \
    conda activate default && \
    mamba clean -y --all && \
    pip install -r /tmp/requirements.txt --no-cache-dir &&\
    rm /tmp/requirements.txt && \
    chmod -R 777 /opt/conda/envs/default

# install ngrok
RUN curl -s https://ngrok-agent.s3.amazonaws.com/ngrok.asc \
	| sudo tee /etc/apt/trusted.gpg.d/ngrok.asc >/dev/null \
	&& echo "deb https://ngrok-agent.s3.amazonaws.com buster main" \
	| sudo tee /etc/apt/sources.list.d/ngrok.list \
	&& sudo apt update \
	&& sudo apt install ngrok

# install nsight-systems-cli (nsys)
RUN apt-get update && \
	apt-get install -y --no-install-recommends gnupg && \
	echo "deb http://developer.download.nvidia.com/devtools/repos/ubuntu$(. /etc/lsb-release; echo "$DISTRIB_RELEASE" | tr -d .)/$(dpkg --print-architecture) /" | tee /etc/apt/sources.list.d/nvidia-devtools.list && \
	apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub && \
	apt-get update && \
	apt-get install -y nsight-systems-cli && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*
