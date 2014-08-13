FROM ubuntu:precise

#install syslibs needed
RUN apt-get update -y
RUN DEBIAN_FRONTEND=noninteractive apt-get install libssl-dev swig python-dev curl git -y

# install pip
RUN curl --silent --show-error --retry 5 https://raw.github.com/pypa/pip/master/contrib/get-pip.py | python2.7

# mount the current project workspace under /project inside the container
ADD . /project

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install perlbrew:
ENV PERLBREW_ROOT /project/perl5
RUN curl -L http://install.perlbrew.pl | /bin/bash
WORKDIR /project

# Install a version of Perl:
RUN ./perl5/bin/perlbrew install perl-5.14.4
