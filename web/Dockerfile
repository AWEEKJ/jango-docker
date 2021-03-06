FROM ubuntu:16.04

MAINTAINER Hanju Jo <dev.hanju.jo@gmail.com>

# Update the default application repository sources list
RUN apt-get update && apt-get -y upgrade
RUN apt-get install -y \
    python3 \
    python3-dev \
    python3-pip \
    python3-setuptools

# Set variables for project name, and where to place files in container.
ENV PROJECT=web
ENV CONTAINER_HOME=/usr/src/app
ENV CONTAINER_PROJECT=$CONTAINER_HOME/$PROJECT

# Create application subdirectories
WORKDIR $CONTAINER_HOME
RUN mkdir logs

# Copy application source code to $CONTAINER_PROJECT
COPY . $CONTAINER_PROJECT

# Install Python dependencies
RUN pip3 install --upgrade pip && pip3 install -r $CONTAINER_PROJECT/requirements_prod.txt

# Port to expose
# 80 = Nginx
# 8000 = Gunicorn
# 5432 = Postgresql
EXPOSE 80 8000 5432

WORKDIR $CONTAINER_PROJECT
COPY ./entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]