# Ubuntu/precise is the main distribution
FROM ubuntu:precise

# sanitize all package lists
RUN echo > /etc/apt/sources.list
RUN echo deb http://archive.ubuntu.com/ubuntu/ precise main restricted universe multiverse > /etc/apt/sources.list.d/precise.list
RUN echo deb http://archive.ubuntu.com/ubuntu/ precise-updates main restricted universe multiverse >> /etc/apt/sources.list.d/precise.list
RUN echo deb http://archive.ubuntu.com/ubuntu/ precise-security main restricted universe multiverse >> /etc/apt/sources.list.d/precise.list

# add chris-lea repo
RUN apt-get update
RUN apt-get install --no-install-recommends -y software-properties-common python-software-properties
RUN add-apt-repository ppa:chris-lea/node.js

# add wget and nodejs
RUN apt-get update
RUN apt-get install --no-install-recommends -y wget nodejs

# install the httpapi
RUN wget http://downloads.buddycloud.com/packages/debian/nightly/buddycloud-http-api/buddycloud-http-api-0.1+dev20140126.git.e0da321/buddycloud-http-api_0.1+dev20140126.git.e0da321-1_amd64.deb -O /tmp/buddycloud-http-api.deb -o /dev/null
RUN dpkg -i /tmp/buddycloud-http-api.deb
ADD config.js /usr/share/buddycloud-http-api/config.js

# run the httpapi
ENTRYPOINT cd /usr/share/buddycloud-http-api; node -v; node server.js
EXPOSE 9123