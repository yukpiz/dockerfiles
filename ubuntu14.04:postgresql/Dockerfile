# Docker image build file.
# TAG: yukpiz/ubuntu:c-dev

FROM yukpiz/ubuntu:develop
MAINTAINER yukpiz<yukpiz@gmail.com>

RUN apt-get update
RUN apt-get install -y -q postgresql-9.3 libpq-dev postgresql-client-9.3 postgresql-contrib-9.3

USER postgres
RUN /etc/init.d/postgresql start &&\
    psql --command "CREATE USER docker WITH SUPERUSER PASSWORD 'docker';" &&\
    psql --command "CREATE DATABASE docker WITH OWNER docker TEMPLATE template0 ENCODING 'utf8';"

RUN echo "host    all    all    192.168.201.0/24    md5" >> /etc/postgresql/9.3/main/pg_hba.conf
RUN echo "listen_addresses='*'" >> /etc/postgresql/9.3/main/postgresql.conf

EXPOSE 5432
VOLUME ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql"]

CMD ["/usr/lib/postgresql/9.3/bin/postgres", "-D", "/var/lib/postgresql/9.3/main", "-c", "config_file=/etc/postgresql/9.3/main/postgresql.conf"]


