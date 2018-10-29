FROM gcr.io/cloud-builders/gcloud

ENV TERRAFORM_VERSION=0.11.8
ENV TERRAFORM_VERSION_SHA256SUM=84ccfb8e13b5fce63051294f787885b76a1fedef6bdbecf51c5e586c9e20c9b7

RUN apt-get update && \
    apt-get -y install curl unzip ca-certificates && \
    curl https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
      > terraform_linux_amd64.zip && \
    echo "${TERRAFORM_VERSION_SHA256SUM} terraform_linux_amd64.zip" > terraform_SHA256SUMS && \
    sha256sum -c terraform_SHA256SUMS --status && \
    unzip terraform_linux_amd64.zip -d /builder/terraform && \
    rm -f terraform_linux_amd64.zip && \
    curl  -L https://github.com/DeviaVir/terraform-provider-gsuite/releases/download/v0.1.9/terraform-provider-gsuite_0.1.9_linux_amd64.zip \
      > terraform_gsuite_linux_amd64.zip && \
    mkdir -p ${HOME}/.terraform.d/plugins && \
    echo "Home directory..." && \
    echo $HOME && \
    unzip terraform_gsuite_linux_amd64.zip -d ${HOME}/.terraform.d/plugins/ && \
    rm -f terraform_gsuite_linux_amd64.zip

ENV PATH=/builder/terraform/:$PATH
COPY entrypoint.bash /builder/entrypoint.bash
ENTRYPOINT ["/builder/entrypoint.bash"]
