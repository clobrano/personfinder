FROM phusion/baseimage
MAINTAINER Carlo Lobrano <c.lobrano@gmail.com>

CMD ["/sbin/my_init"]

# Get rid of debconf complaining about noninteractive mode
ENV DEBIAN_FRONTEND noninteractive
ENV PATH $PATH:/opt/google_appengine
ENV APPENGINE_DIR /opt/google_appengine/
ENV PERSONFINDER_DIR /opt/personfinder
ENV INIT_DATASTORE 0

RUN apt-get update
RUN apt-get install -y build-essential unzip
RUN apt-get install -y python2.7 libpython2.7-dev
RUN apt-get install -y python-setuptools
RUN apt-get install -y git
RUN apt-get install -y wget
RUN apt-get install -y time

WORKDIR /opt/
RUN wget http://effbot.org/downloads/Imaging-1.1.7.tar.gz
RUN tar xvfz Imaging-1.1.7.tar.gz && cd Imaging-1.1.7 && python2.7 setup.py install

WORKDIR   /opt/
RUN wget  https://storage.googleapis.com/appengine-sdks/featured/google_appengine_1.9.25.zip
RUN unzip google_appengine_1.9.25.zip 

RUN easy_install-2.7 pytest
RUN apt-get install -y gettext

ADD gae-run-app.sh      /usr/bin/
ADD setup_datastore.sh  /usr/bin/

RUN mkdir -p /opt/personfinder
WORKDIR /opt/personfinder

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
