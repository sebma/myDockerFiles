# syntax=docker/dockerfile:1
FROM ubuntu:16.04
ARG apt_proxy
RUN printf "Acquire::http::Proxy   \"$apt_proxy\";\nAcquire::https::Proxy   \"$apt_proxy\";\n" > /etc/apt/apt.conf.d/00aptproxy
RUN sed -i 's|//archive|//fr.archive|' /etc/apt/sources.list
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN <<-EOF
	apt-get install -V -y tzdata --no-install-recommends
	apt-get install -V -y bash-completion ca-certificates openssh-client --no-install-recommends
	apt-get install -V -y vim command-not-found git remake emacs-nox nano --no-install-recommends # ocaml-nox
EOF
RUN echo "source /usr/share/bash-completion/completions/git" >> $HOME/.profile
RUN mkdir -vm=700 $HOME/.ssh/
# Pour les instructions COPY et WORKDIR
ENV HOME=/root
COPY config id_rsa $HOME/.ssh/
RUN mkdir $HOME/myDIR
WORKDIR $HOME
CMD ["bash","-li"]
