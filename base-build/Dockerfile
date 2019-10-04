FROM debian:stretch-slim

ENV LC_ALL C.UTF-8

ENV SKAFFOLD_VERSION 0.39.0
ENV HELM_VERSION v2.14.3
ENV HELM_HOME /root/.helm

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
       git python3-pip wget curl build-essential apt-transport-https ca-certificates gnupg2 software-properties-common jq \
# Prepare Kubectl
  && curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - \
  && add-apt-repository "deb https://apt.kubernetes.io/ kubernetes-xenial main" \
# Prepare docker
  && curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \
  && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" \
# Install docker & kubectl
  && apt-get update \
  && apt-get install -y --no-install-recommends kubectl docker-ce-cli \
# Install bump2version
  && pip3 install bump2version \
# Install yq https://github.com/kislyuk/yq
  && pip3 install setuptools wheel \
  && pip3 install yq \
# Install Skaffold
  && curl -Lo skaffold https://storage.googleapis.com/skaffold/releases/v$SKAFFOLD_VERSION/skaffold-linux-amd64 \
  && chmod +x skaffold \
  && mv skaffold /usr/local/bin \
# Install Helm
  && curl -L https://git.io/get_helm.sh | bash -s -- --version $HELM_VERSION \
  && helm init -c\
  && helm plugin install https://github.com/chartmuseum/helm-push \
# Clean
  && rm -rf /var/lib/apt/lists/*
