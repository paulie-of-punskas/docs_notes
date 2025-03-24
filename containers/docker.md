# Docker:

## How to:

#### Build and run image with Java Spring Boot, on MacBook Silicone:

```bash
docker build -t name_of_image:latest --platform linux/amd64 .
docker run -p 8080:8080 name_of_image:latest
```

#### Run docker image with environmental variables

```bash
docker run --env VARIABLE1='VALUE1' -t name_of_image:latest
```

#### Add secrets:

Sukurt `docker-compose.yaml` (pvz. apacioj). `my-secret-app` build time'e sukurs kintamuosius `marta` ir `secret_2`:  
- `marta` verte yra `/run/secrets/my_secret` content'e. File'as yra sukuriamas is zemiau esancio secrets.txt. T.y.: `secrets.txt` > `my_secret` yra reference > `/run/secrets` yra sukuriam'a automatiskai Docker compose
- `secret_2` gana aisku, definiuojam ji kaip bash'ui

```yaml
services:
  my-secret-app:
    image: docker/secrets
    environment:
      marta: /run/secrets/my_secret
      secret_2: slaptazodis_secret_2
    secrets:
      - my_secret

secrets:
  my_secret:
    file: secrets.txt
  secret_2:
    file: secret_2.txt
```

# Veikiantys java kontenerai:

### 126 MB

```
FROM eclipse-temurin:17-jdk-alpine AS build

ENV JAVA_HOME=/opt/jdk/jdk-17
ENV PATH="${JAVA_HOME}/bin:${PATH}"

RUN ["jlink", "--compress=2", \
     "--module-path", "/opt/jdk/jdk-17.0.14/jmods/", \
     "--add-modules", "java.base,java.compiler,java.desktop,java.instrument,java.management,java.naming,java.net.http,java.prefs,java.rmi,java.scripting,java.security.jgss,java.sql,jdk.jfr,jdk.unsupported", \
     "--no-header-files", "--no-man-pages", \
     "--output", "/optimized-jdk-17"]

FROM alpine:latest
COPY --from=build  /optimized-jdk-17 /opt/jdk 
ENV PATH=$PATH:/opt/jdk/bin

EXPOSE 8080
COPY ../target/track_workout-0.0.1-SNAPSHOT.jar /opt/app/
CMD ["java", "-showversion", "-jar", "/opt/app/track_workout-0.0.1-SNAPSHOT.jar"]
```

### 150 MB

```
FROM alpine:latest AS build
ENV JAVA_HOME=/opt/jdk/jdk-17.0.14
ENV PATH=$JAVA_HOME/bin:$PATH

ADD https://download.bell-sw.com/java/17.0.14+10/bellsoft-jdk17.0.14+10-linux-x64-musl.tar.gz /opt/jdk/
RUN tar -xzvf /opt/jdk/bellsoft-jdk17.0.14+10-linux-x64-musl.tar.gz -C /opt/jdk/

RUN ["jlink", "--compress=2", \
     "--module-path", "/opt/jdk/jdk-17.0.14/jmods/", \
     "--add-modules", "java.base,java.compiler,java.desktop,java.instrument,java.management,java.naming,java.net.http,java.prefs,java.rmi,java.scripting,java.security.jgss,java.sql,jdk.jfr,jdk.unsupported", \
     "--no-header-files", "--no-man-pages", \
     "--output", "/optimized-jdk-17"]

FROM alpine:latest
COPY --from=build  /optimized-jdk-17 /opt/jdk 
ENV PATH=$PATH:/opt/jdk/bin

EXPOSE 8080
COPY ../target/track_workout-0.0.1-SNAPSHOT.jar /opt/app/
CMD ["java", "-showversion", "-jar", "/opt/app/track_workout-0.0.1-SNAPSHOT.jar"]```
```

### 650 MB

```
# (1)
FROM alpine:latest AS build 

# (2)
ADD https://download.bell-sw.com/java/17.0.14+10/bellsoft-jdk17.0.14+10-linux-x64-musl.tar.gz /opt/jdk/
RUN tar -xzvf /opt/jdk/bellsoft-jdk17.0.14+10-linux-x64-musl.tar.gz -C /opt/jdk/

ENV JAVA_HOME=/opt/jdk/jdk-17.0.14
ENV PATH=$JAVA_HOME/bin:$PATH
EXPOSE 8080
COPY ../target/track_workout-0.0.1-SNAPSHOT.jar /opt/app/
CMD ["java", "-showversion", "-jar", "/opt/app/track_workout-0.0.1-SNAPSHOT.jar"]
```

# URLs:
Use secrets: 
- https://docs.docker.com/compose/how-tos/use-secrets/

Use environment variables in Compose:
- https://docs.docker.com/compose/how-tos/environment-variables/#/the-env-file
