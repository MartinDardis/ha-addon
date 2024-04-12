# Usa una imagen base de Debian para ARM
#FROM arm32v7/debian:buster-slim
FROM debian:buster-slim

# Actualiza los paquetes e instala las dependencias necesarias
RUN apt-get update && \
    apt-get install -y curl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Instala Node.js 14.x
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs

ENV CK_API_ENV=prod
RUN apt-get update && apt-get install -y python build-essential
RUN mkdir -p /workspace/node_modules
COPY ["./dist", "./package.json", "/workspace/"]
WORKDIR /workspace
RUN npm install --production --save-exact
COPY ["./node_modules", "/workspace/node_modules/"]
EXPOSE 3000
CMD npm start
