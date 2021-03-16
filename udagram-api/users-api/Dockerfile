FROM node:12-alpine

RUN apk upgrade --no-cache \
    && apk add --no-cache zip \
    # Do some cleanup
    && apk del -rf --purge --no-cache tzdata \
    && rm -rf /usr/include  /var/cache/apk/* /root/.node-gyp /usr/share/man /tmp/* \
    && echo "apk fin"

RUN apk add --no-cache --virtual .build-deps build-base python2
RUN npm i -g node-gyp make

ENV POSTGRES_USERNAME=$POSTGRES_USERNAME
ENV POSTGRES_PASSWORD=$POSTGRES_PASSWORD
ENV POSTGRES_DB=$POSTGRES_DB
ENV POSTGRES_HOST=$POSTGRES_HOST

# Add package file
COPY package*.json ./

# Install deps
RUN npm i

# Copy source
COPY src ./src
COPY tsconfig.json ./tsconfig.json
COPY tslint.json ./tslint.json
COPY .npmrc ./.npmrc

# Build dist
RUN npm run build

# Expose port
EXPOSE 8100

CMD npm run start