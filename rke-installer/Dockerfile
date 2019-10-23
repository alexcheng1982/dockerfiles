FROM dtzar/helm-kubectl:2.14.3

RUN curl -LSs https://github.com/rancher/rke/releases/download/v0.3.1/rke_linux-amd64 > /usr/local/bin/rke
RUN chmod +x /usr/local/bin/rke

RUN echo "===> Installing sudo to emulate normal OS behavior..."  && \
    apk --update add sudo                                         && \
    \
    \
    echo "===> Adding Python runtime..."  && \
    apk --update add python3 openssl ca-certificates    && \
    apk --update add --virtual build-dependencies \
                python3-dev libffi-dev openssl-dev build-base  && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \            
    pip3 install --upgrade pip setuptools wheel cffi                           && \
    \
    \
    echo "===> Installing Ansible..."  && \
    pip3 install ansible                && \
    \
    \
    echo "===> Installing handy tools (not absolutely required)..."  && \
    pip3 install --upgrade pycrypto pywinrm         && \
    apk --update add sshpass openssh-client rsync  && \
    \
    \
    echo "===> Removing package list..."  && \
    apk del build-dependencies            && \
    rm -rf /var/cache/apk/*               && \
    \
    \
    echo "===> Adding hosts for convenience..."  && \
    mkdir -p /etc/ansible                        && \
    echo 'localhost' > /etc/ansible/hosts

RUN pip3 install boto3 && \
  pip3 install boto

WORKDIR /etc/ansible 