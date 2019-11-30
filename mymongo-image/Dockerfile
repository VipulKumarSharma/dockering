# Setup a Base Image
FROM alpine

# Install a software (i.e. binutils), using alpine OS command
RUN echo 'http://dl-cdn.alpinelinux.org/alpine/v3.6/main' >> /etc/apk/repositories
RUN echo 'http://dl-cdn.alpinelinux.org/alpine/v3.6/community' >> /etc/apk/repositories

RUN apk update
RUN apk add mongodb
RUN apk add binutils

# Configure that software
VOLUME [ "/data/db" ]
WORKDIR /data
EXPOSE 27017
RUN apk add isl

# Set default commands
CMD [ "mongod" ]

