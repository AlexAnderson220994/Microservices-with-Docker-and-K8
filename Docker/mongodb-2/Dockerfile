# Use an mongo
FROM mongo:4.4

# Copy your custom mongod.conf file to the container
COPY mongod.conf /etc/mongod.conf.orig

# Expose the default MongoDB port
EXPOSE 27017

# Start MongoDB with your custom configuration
CMD ["mongod"]
