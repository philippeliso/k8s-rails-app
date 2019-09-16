# Pull from Oficial Ruby
FROM ruby:2.4.1

RUN printf "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list

# Install dependencys
RUN apt-get update && \
	apt-get install -qq -y \
	locales \
	telnet \
	tzdata \
	vim \
	bundler \
	build-essential \
	nodejs \
	libpq-dev \
	imagemagick \
	libmagickwand-dev \
	postgresql-client --fix-missing --no-install-recommends

# Locales
RUN locale-gen en_US.UTF-8
ENV LANG="en_US.UTF-8" 
ENV LANGUAGE="en_US:en"
ENV LC_ALL="en_US.UTF-8"

# Timezone
RUN ln -fs /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime && \
	dpkg-reconfigure -f noninteractive tzdata

# Create and set Workdir
RUN mkdir /opt/company-webservice
WORKDIR /opt/company-webservice

# Install Rails
#RUN gem install rails -v 4.2.5 && \
#	gem install bundler
RUN gem install bundler

# Trick for git clone command without cache on Dockerfile
# Passar --build-arg CACHEBUST=$(date +%s) na hora do build
ARG CACHEBUST=1

# Project Clone and bundle
RUN cd /opt/company-webservice && \
	git clone -b azure-kube-qa https://some-repository.git . && \
	bundle install

# Expose port
EXPOSE 3000
EXPOSE 3001
