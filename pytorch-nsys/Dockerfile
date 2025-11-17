ARG BASE_IMAGE="ghcr.io/jkminder/dlab-runai-images/pytorch:master"

FROM ${BASE_IMAGE}

# install nsight-systems-cli (nsys)
RUN apt-get clean && \
	rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/* && \
	apt-get update && \
	apt-get install -y --no-install-recommends curl ca-certificates gpg && \
	curl -fsSL https://developer.download.nvidia.com/devtools/repos/ubuntu2204/amd64/nvidia.pub | gpg --dearmor -o /usr/share/keyrings/nvidia-devtools.gpg && \
	echo "deb [signed-by=/usr/share/keyrings/nvidia-devtools.gpg] https://developer.download.nvidia.com/devtools/repos/ubuntu2204/amd64/ /" > /etc/apt/sources.list.d/nvidia-devtools.list && \
	apt-get update && \
	apt-get install -y -o APT::Keep-Downloaded-Packages="false" --no-install-recommends nsight-systems-cli && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*
