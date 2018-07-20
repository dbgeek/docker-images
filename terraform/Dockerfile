FROM alpine:3.7

MAINTAINER TXR Team <bnal@ba78.me>

ARG tf_version
ENV USER=tf

COPY hashicorp.asc .

RUN apk add --no-cache ca-certificates curl gnupg graphviz && \
    gpg --import hashicorp.asc && \
    curl -fsSLO https://releases.hashicorp.com/terraform/${tf_version}/terraform_${tf_version}_linux_amd64.zip && \
    curl -fsSLO https://releases.hashicorp.com/terraform/${tf_version}/terraform_${tf_version}_SHA256SUMS && \
    curl -fsSLO https://releases.hashicorp.com/terraform/${tf_version}/terraform_${tf_version}_SHA256SUMS.sig && \
    echo "$(grep terraform_${tf_version}_linux_amd64.zip terraform_${tf_version}_SHA256SUMS)" > SHA256SUMS && \
    gpg --verify terraform_${tf_version}_SHA256SUMS.sig terraform_${tf_version}_SHA256SUMS && \
    sha256sum -c SHA256SUMS && \
    unzip terraform_${tf_version}_linux_amd64.zip && \
    mv terraform /usr/bin/ && \
    rm terraform_${tf_version}_linux_amd64.zip terraform_${tf_version}_SHA256SUMS terraform_${tf_version}_SHA256SUMS.sig SHA256SUMS && \
    adduser -D $USER

USER $USER
WORKDIR /home/$USER

ENTRYPOINT ["terraform"]
