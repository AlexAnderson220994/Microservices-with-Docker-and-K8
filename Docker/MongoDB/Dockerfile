# Use an official MongoDB image as a base
FROM mongo:latest

COPY mongod.conf.orig /etc/mongod.conf.orig

# Expose the default MongoDB port
EXPOSE 27017

# Specify the command to run MongoDB
CMD ["mongod"]
