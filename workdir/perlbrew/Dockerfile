## -*- docker-image-name: "database-psql-centos6" -*-
FROM centos:centos6
MAINTAINER shaun.ashby@gmail.com
RUN yum install -y postgresql-server perl perl-devel gcc tar bzip2 patch

# Install perlbrew:
ENV PERLBREW_ROOT /project/perl5
RUN curl -L http://install.perlbrew.pl | /bin/bash
WORKDIR /project

# Install a version of Perl:
RUN source /project/perl5/etc/bashrc
RUN /project/perl5/bin/perlbrew install-cpanm

# Set up volumes:
VOLUME ["/data"]
VOLUME ["/app"]

CMD ["/bin/ls","-l"]

