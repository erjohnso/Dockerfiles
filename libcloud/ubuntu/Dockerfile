FROM ubuntu:trusty
MAINTAINER Eric Johnson <erjohnso@google.com>

WORKDIR /virtualenv

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get upgrade -y
RUN apt-get install python2.7-dev python3.4-dev python-pip git vim -y
RUN apt-get clean

RUN pip install virtualenv
RUN virtualenv --python=/usr/bin/python2.7 py27
RUN ["/bin/bash", "-c", "source py27/bin/activate; pip install tox"]
RUN virtualenv --python=/usr/bin/python3.4 py34
RUN ["/bin/bash", "-c", "source py34/bin/activate; pip install tox"]

RUN adduser --disabled-password --quiet erjohnso
RUN echo "erjohnso:erjohnso" | chpasswd
RUN su -l -c 'git clone https://github.com/erjohnso/dotfiles' erjohnso
RUN su -l -c 'dotfiles/install.sh' erjohnso

CMD ["su", "-l", "erjohnso"]
