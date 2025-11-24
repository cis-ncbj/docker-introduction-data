# Base image
FROM node:4
MAINTAINER Konrad Klimaszewski <konrad.klimaszewski@ncbj.gov.pl>

# Add local user
RUN groupadd -r flask && useradd -r -g flask flask

# install system-wide deps for python and node
RUN echo "deb [trusted=yes] http://archive.debian.org/debian jessie main" > /etc/apt/sources.list
RUN apt-get update --allow-unauthenticated \
 && apt-get install -y --no-install-recommends --allow-unauthenticated \
      python-pip python-dev dnsutils \
 && rm -rf /var/lib/apt/lists/*

# Copy dependency lists
COPY flask-app/requirements.txt flask-app/package.json /opt/flask-app/
WORKDIR /opt/flask-app

# Install app specific dependencies
RUN npm install
RUN pip install -r requirements.txt

# Copy our application code
COPY flask-app /opt/flask-app

# Build application (compactify json, css, etc)
RUN npm run build

# Run the application as normal user
USER flask

# expose port
EXPOSE 5000

# start app
CMD [ "python", "./app.py" ]
