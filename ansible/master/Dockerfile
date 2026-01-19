
FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=UTC

RUN sed -i 's|archive.ubuntu.com|security.ubuntu.com|g' /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y \
    tzdata \
    python3 \
    python3-pip \
    openssh-client \
    sshpass \
    vim \
    curl \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install --no-cache-dir ansible

RUN mkdir -p /root/.ssh && chmod 700 /root/.ssh

RUN mkdir -p /ansible

RUN mkdir -p /ansible && \
    echo "[slaves]" > /ansible/inventory
    
RUN echo "[defaults]" > /ansible/ansible.cfg

WORKDIR /ansible


CMD ["/bin/bash"]






