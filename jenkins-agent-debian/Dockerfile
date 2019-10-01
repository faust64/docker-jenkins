FROM debian:stretch

LABEL io.k8s.description="The jenkins agent Debian image has the tools required building debian packages." \
      io.k8s.display-name="Jenkins Agent - Debian Stretch" \
      io.openshift.tags="openshift,jenkins,agent,debian,stretch" \
      architecture="x86_64" \
      name="ci/jenkins-agent-debian" \
      maintainer="Samuel MARTIN MORO <faust64@gmail.com>" \
      help="For more information visit https://github.com/faust64/docker-jenkins" \
      version="1.0"

ENV HOME=/home/jenkins \
    DEBIAN_FRONTEND=noninteractive

USER root
ADD config/* /usr/local/bin/
RUN apt-get -y update \
    && if test "$DO_UPGRADE"; then \
	echo "# Upgrade Base Image"; \
	apt-get -y upgrade; \
	apt-get -y dist-upgrade; \
    fi \
    && echo "# Install Headless Java & Deb Utils" \
    && apt-get -y install bc gettext git subversion openjdk-8-jre-headless gnupg curl wget \
		lsof rsync tar unzip debianutils zip bzip2 make gcc g++ devscripts debhelper \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir -p /home/jenkins \
    && chown -R 1001:0 /home/jenkins \
    && chmod -R g+w /home/jenkins \
    && chmod 664 /etc/passwd \
    && chmod -R 775 /etc/alternatives /usr/lib/jvm \
    && chmod 775 /usr/bin /usr/share/man/man1

USER 1001
ENTRYPOINT ["/usr/local/bin/run-jnlp-client"]
