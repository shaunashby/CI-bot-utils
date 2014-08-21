# Dockerfile to run a PostgreSQL sandbox, based on Postgres 9.x

FROM ubuntu:14.04
#
MAINTAINER shaun.ashby@gmail.com
#
# Update package repositories:
RUN apt-get update -y

# Install required packages:
RUN DEBIAN_FRONTEND=noninteractive apt-get install postgresql-9.3 postgresql-client-9.3 postgresql-server-dev-9.3 postgresql-plperl-9.3 postgresql-plpython-9.3 postgresql-9.3-plsh -y

# Run next commands as the postgres user:
USER postgres
RUN /etc/init.d/postgresql start && psql --command "CREATE USER docker WITH SUPERUSER PASSWORD 'docker+999';" && createdb -O docker docker

# Allow for remote connections to the database. Listen on all addresses:
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql/9.3/main/pg_hba.conf
RUN echo "listen_addresses='*'" >> /etc/postgresql/9.3/main/postgresql.conf

# Expose the PostgreSQL port:
EXPOSE 5432

# Add VOLUMEs to allow backup of config, logs and databases:
VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql"]

# Start the database when starting the container:
CMD ["/usr/lib/postgresql/9.3/bin/postgres", "-D", "/var/lib/postgresql/9.3/main", "-c", "config_file=/etc/postgresql/9.3/main/postgresql.conf"]
