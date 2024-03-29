FROM golang:1.8-alpine AS builder

WORKDIR /go/src/github.com/optiopay/klar

COPY assets ./assets
COPY clair ./clair
COPY docker ./docker
COPY utils ./utils
COPY vendor ./vendor
COPY *.go ./

RUN apk --update add git \
    && go get -d github.com/coreos/clair/database \
    && CGO_ENABLED=0 go build -a -installsuffix cgo . \
    && cp ./klar /klar

FROM openshift/jenkins-slave-base-centos7

LABEL com.redhat.component="jenkins-agent-klar" \
      io.k8s.description="The jenkins agent klar image has the tools scanning Docker images against CoreOS Clair." \
      io.k8s.display-name="Jenkins Agent - Klar" \
      io.openshift.tags="openshift,jenkins,agent,clair,klar" \
      architecture="x86_64" \
      name="ci/jenkins-agent-klar" \
      maintainer="Samuel MARTIN MORO <faust64@gmail.com>" \
      help="For more information visit https://github.com/faust64/docker-jenkins" \
      version="1.0"

COPY --from=builder /klar /usr/local/bin/klar

RUN if yum -y install epel-release; then \
	if test "$DO_UPGRADE"; then \
	    yum -y upgrade; \
	fi \
	&& yum -y install ca-certificates jq; \
    else \
	curl https://github.com/stedolan/jq/releases/download/jq-1.6/jq-linux64 -o /usr/bin/jq; \
	&& chmod +x /usr/bin/jq; \
    fi

USER 1001
