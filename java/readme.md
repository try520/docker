# 用法
 ```
FROM openjdk:11-jdk-slim AS build-env
ADD . /app/examples
WORKDIR /app
RUN javac examples/*.java
RUN jar cfe main.jar examples.HelloJava examples/*.class 

FROM try520/thin_java_11:latest
COPY --from=build-env /app /app
WORKDIR /app
CMD ["main.jar"]
```
