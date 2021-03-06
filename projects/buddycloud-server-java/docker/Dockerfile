# Ubuntu/precise is the main distribution
FROM ubuntu:precise

# sanitize all package lists
RUN echo > /etc/apt/sources.list
RUN echo deb http://archive.ubuntu.com/ubuntu/ precise main restricted universe multiverse > /etc/apt/sources.list.d/precise.list
RUN echo deb http://archive.ubuntu.com/ubuntu/ precise-updates main restricted universe multiverse >> /etc/apt/sources.list.d/precise.list
RUN echo deb http://archive.ubuntu.com/ubuntu/ precise-security main restricted universe multiverse >> /etc/apt/sources.list.d/precise.list

# add java
RUN apt-get update
RUN apt-get install --no-install-recommends -y openjdk-7-jdk dbconfig-common

# add python deps
RUN apt-get install --no-install-recommends -y python-setuptools postgresql-server-dev-9.1 libsqlite3-dev build-essential python-dev
RUN easy_install psycopg2

# install the java-server
ADD buddycloud-server-java.deb /tmp/buddycloud-server-java.deb
ADD external-domain-checker /usr/bin/external-domain-checker
RUN DEBIAN_FRONTEND=noninteractive dpkg -i /tmp/buddycloud-server-java.deb
RUN chmod +x /usr/bin/external-domain-checker
RUN cd /usr/share/buddycloud-server-java; mv channelserver*jar-with-dependencies.jar channelserver-jar-with-dependencies.jar

# update configuration files
ADD configuration.properties /usr/share/buddycloud-server-java/configuration.properties
ADD log4j.properties /usr/share/buddycloud-server-java/log4j.properties
ADD replace-tigase-vars /usr/share/buddycloud-server-java/replace-tigase-vars

# run java-server
ENTRYPOINT cd /usr/share/buddycloud-server-java; env; ./replace-tigase-vars; java -jar channelserver-jar-with-dependencies.jar
