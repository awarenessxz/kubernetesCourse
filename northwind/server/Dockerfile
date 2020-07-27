# this image will be based on Node v14
FROM node:14

# the environment variable to define my workspace
ENV APP_DIR=/app APP_PORT=3000
ENV DB_USER="root" DB_PASSWORD="changeit"

# create and cd into APP_DIR (mkdir /app && cd /app)
WORKDIR ${APP_DIR}

# copy the file from fortune into /app  (ADD local image)
# copy files
ADD main.js .
ADD package.json .
ADD package-lock.json .
# copy directories
ADD public public
ADD views views
ADD config config

# install the dependencies
RUN npm install

# Anything Above is for building the image
# Anything Below is for running the image

# Add Health Check
HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3 \
    CMD curl -s -f http://localhost:${APP_PORT}/health || exit 1

# inform the container the port that the application is exposing
# only for documentation, not exposing doesn't affects anything
EXPOSE ${APP_PORT}

# run the application
ENTRYPOINT ["node", "main.js"]

