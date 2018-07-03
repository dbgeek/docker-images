FROM alpine:3.7 as builder

ENV GO_VERSION=1.8
ENV GOPATH=/

# Disable cgo, to allow static linking of the resulting go binary.
ENV CGO_ENABLED=0

RUN apk add --no-cache bash unzip curl go make git musl-dev && \
 mkdir -p $GOPATH/src/github.com/terraform-providers && \
 cd $GOPATH/src/github.com/terraform-providers && \
 git clone  https://github.com/dbgeek/terraform-provider-aws.git && \
 cd $GOPATH/src/github.com/terraform-providers/terraform-provider-aws && \
 make build && \
 mkdir -p /root/.terraform.d/plugins && \   
 cp $GOPATH/bin/terraform-provider-aws /root/.terraform.d/plugins/terraform-provider-aws_v1.25.0_x4

FROM alpine:3.7
ENV tf_version=0.11.7
RUN apk add --no-cache bash unzip curl && \
 curl -fsSLO https://releases.hashicorp.com/terraform/${tf_version}/terraform_${tf_version}_linux_amd64.zip && \
 unzip terraform_${tf_version}_linux_amd64.zip && \
 mv terraform /usr/bin/ && \
 rm terraform_${tf_version}_linux_amd64.zip && \
 mkdir -p /root/.terraform.d/plugins

 COPY --from=builder /bin/terraform-provider-aws /root/.terraform.d/plugins/terraform-provider-aws_v1.25.0_x4

ENTRYPOINT ["terraform"]