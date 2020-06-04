#invoke npm in jenkinsfile: sh "scl enable rh-nodejs6 'npm run build'"
FROM quay.io/openshift/origin-jenkins-agent-base:4.4

ENV NODEJS_VERSION=12 \
    NPM_CONFIG_PREFIX=$HOME/.npm-global \
    PATH=$HOME/node_modules/.bin/:$HOME/.npm-global/bin/:$PATH \
    CHROME_BIN=/bin/google-chrome

COPY src/google-chrome.repo ubi.repo /etc/yum.repos.d/

# RUN yum -y --disablerepo='rhel-*' localinstall https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

RUN curl --silent --location https://rpm.nodesource.com/setup_${NODEJS_VERSION}.x | bash -

RUN INSTALL_PKGS="nodejs redhat-lsb libXScrnSaver xdg-utils google-chrome-stable" && \
    DISABLE_REPOS=--disablerepo='rhel-*' && \
    yum $DISABLE_REPOS -y update && \
    yum $DISABLE_REPOS install -y --setopt=tsflags=nodocs \
      $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y && \
    rm -rf /var/cache/yum

USER 1001
