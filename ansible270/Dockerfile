FROM alpine:3.15

LABEL maintainer="daniel@mail.nixbyte.net"

RUN CARGO_NET_GIT_FETCH_WITH_CLI=1 && \
    apk --no-cache add \
        python3\
        py3-pip \
        openssl \
        ca-certificates \
        sshpass \
        openssh-client \
        rsync \
        git && \
    apk --no-cache add --virtual build-dependencies \
        python3-dev \
        libffi-dev \
        musl-dev \
        gcc \
        cargo \
        openssl-dev \
        libressl-dev \
        build-base && \
    pip install --upgrade pip wheel && \
    pip install --upgrade cryptography cffi && \
    pip install ansible==2.7.0 && \
    pip install --upgrade pywinrm && \
    apk del build-dependencies && \
    rm -rf /var/cache/apk/* && \
    rm -rf /root/.cache/pip && \
    rm -rf /root/.cargo

# TODO: Run ansible with limited privileges

RUN mkdir -p /opt/ansible /etc/ansible && \
    echo 'localhost' > /etc/ansible/hosts
#     adduser -D -h /opt/ansible -s $(which sh) -g ansible -u 1001 ansible && \
#     chown -R ansible:ansible /opt/ansible /etc/ansible

# USER ansible

WORKDIR /opt/ansible

CMD [ "ansible-playbook", "--version" ]
