FROM quay.io/centos/centos:stream9

ENV container=docker
ENV LANG=en_US.UTF-8

RUN dnf -y update && \
    dnf -y install --allowerasing \
        openssh-server \
        sudo \
        python3 \
        curl \
        wget \
    && dnf clean all

RUN mkdir -p /var/run/sshd

RUN useradd -m -s /bin/bash ansible && \
    echo "ansible:ansible" | chpasswd && \ 
    echo "ansible ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN mkdir -p /home/ansible/.ssh && \
    chmod 700 /home/ansible/.ssh && \
    chown ansible:ansible /home/ansible/.ssh



RUN sed -i 's/^#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config && \
    sed -i 's/^PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config && \
    sed -i 's/^#PubkeyAuthentication yes/PubkeyAuthentication yes/' /etc/ssh/sshd_config

EXPOSE 22

CMD ["/bin/bash", "-c", "ssh-keygen -A && /usr/sbin/sshd -D"]
