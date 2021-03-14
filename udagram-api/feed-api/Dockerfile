FROM node:12.14.1

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