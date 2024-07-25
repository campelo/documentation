---
title: 
published: false
description: 
tags: ''
cover_image: ../../assets/cover.png
canonical_url: null
id: 
---

###### :postbox: Contact :brazil: :us: :fr:

[Twitter](https://twitter.com/campelo87)
[LinkedIn](https://www.linkedin.com/in/flavio-campelo/?locale=en_US)

# Basic actions
## Dockerfile BE
```
# Use the official .NET SDK image to build the app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy the csproj and restore as distinct layers
COPY ./ ./
RUN dotnet restore 

# Copy the remaining files and build the app
RUN dotnet publish ./path/to/my.project.csproj -c Release -o out

# Use the official .NET runtime image to run the app
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

# Install Python and pip
RUN apt-get update && \
    apt-get install -y python3 python3-pip python3-venv && \
    rm -rf /var/lib/apt/lists/*

# Create a virtual environment and install xxx package
RUN python3 -m venv /opt/venv && \
    /opt/venv/bin/pip install xxx

# Ensure the virtual environment is used
ENV PATH="/opt/venv/bin:$PATH"

COPY --from=build /app/out .

# Set the entry point for the container
ENTRYPOINT ["dotnet", "my.project.dll"]

# Expose port 8080
EXPOSE 8080

```

## Dockerfile FE
```
# Stage 1: Build the custom library
FROM node:alpine AS build-core

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm install

COPY ./ ./
RUN npm run build custom-lib-name

# Stage 2: Build the Angular app
FROM node:alpine AS build

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm install

COPY ./ ./

# Ensure the custom-lib-name build output is available
COPY --from=build-core /app/dist/custom-lib-name /app/dist/custom-lib-name

RUN npm run prod:all

# Stage 3: Serve the Angular app with nginx
FROM nginx:alpine

# Copy the Angular app to the nginx html directory
COPY --from=build /app/dist/my-project-name /usr/share/nginx/html

COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

```

### nginx sample
```
# # the events block is required
events {
    worker_connections 1024;
}

http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    server {
        listen 80;
        server_name localhost;

        root /usr/share/nginx/html;
        index index.html index.htm;

        # Serve the Angular app from the /esquinao/ base URL
        location / {
            try_files $uri $uri/ /index.html;
        }

        # Serve 404 errors with the index.html page (important for SPAs)
        error_page 404 /index.html;
    }
}
```

## docker-compose 

### file
```
version: '3.8'

services:
  mssql-sample:
    image: mcr.microsoft.com/mssql/server:2022-latest
    ports:
      - "8002:1433"
    environment:
      - ACCEPT_EULA=Y
      - MSSQL_SA_PASSWORD=yourStrong!Password
    volumes:
      - ./my/path/:/usr/src/app/
    entrypoint: ["/bin/bash", "/usr/src/app/entrypoint.sh"]

  mysql-sample:
    image: mysql:8.0.37
    ports:
      - "8003:3306"
    command: --lower_case_table_names=1
    environment:
      - MYSQL_ROOT_PASSWORD=yourStrong!Password
      - MYSQL_DATABASE=myDbName
    volumes:
      - ./my/path/mysql-init.sql:/docker-entrypoint-initdb.d/mysql-init.sql

  backend-dev:
    build:
      context: ./my/be/path
      dockerfile: Dockerfile
    ports:
      - "8001:8080"
    volumes:
      - ./my/path:/app/data/mypathname
    environment:
      - MySql__ConnectionString=Server=host.docker.internal;Port=8003;Database=EsquinaoDev;Uid=root;Pwd=yourStrong!Password;
      - Database__ConnectionString=Server=host.docker.internal,8002;Database=EsquinaoDev;User Id=sa;Password=yourStrong!Password;TrustServerCertificate=True;
    depends_on:
      - mysql-sample
      - mssql-sample

  frontend-dev:
    build:
      context: ./my/fe/path
      dockerfile: Dockerfile
    ports:
      - "8000:80"
    depends_on:
      - backend-dev
    environment:
      - API_URL=http://localhost:8001
```

### up/down
```bash
docker-compose up --build
```

Finally, you can access the service at [http://localhost:8000](http://localhost:8000/)

To ensure all new configurations are applied in all containers
```bash
# Stop and remove containers
docker-compose down

# Remove unused images, containers, and volumes
docker system prune -af
```

## image
```
# list containers
docker container ls

# commit new changes (save current container status)
docker commit {image-hash} {image-name}:{version-or-latest}

# add a new tag...
docker tag {image-name} {container-registry}/{image-name}:{version-or-latest}

# send image to remote container registry...
docker push {container-registry}/{image-name}:{version-or-latest}

# get remote container registry...
docker pull {container-registry}/{image-name}:{version-or-latest}

# run image
docker run -p {local-port}:{internal-port} --name my-container-name {image-name}

# removing image
docker image rm {container-registry}/{image-name}:{version-or-latest}
```

---

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.