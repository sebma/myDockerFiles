FROM coreapps/ubuntu16.04:2024-11-24
ARG apt_proxy
RUN echo "Acquire::http::Proxy   \"$apt_proxy\";" >  /etc/apt/apt.conf.d/00aptproxy
RUN sed -i 's|//archive|//fr.archive|' /etc/apt/sources.list
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt install -V -y command-not-found bash-completion git remake vim emacs-nox nano openssh-server bind9-host # ocaml-nox
RUN echo "source /usr/share/bash-completion/completions/git" >> $HOME/.profile
RUN mkdir -vm=700 $HOME/.ssh/
COPY ./config /root/.ssh/
COPY id_rsa /root/.ssh/
WORKDIR /root
RUN mkdir /myDIR
ENTRYPOINT ["bash","-li"]
