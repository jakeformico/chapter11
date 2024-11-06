# #stage 1
# #Start with a base image containing Java runtime
# FROM openjdk:11-slim as build

# # Add Maintainer Info
# LABEL maintainer="Illary Huaylupo <illaryhs@gmail.com>"

# # The application's jar file
# ARG JAR_FILE

# # Add the application's jar to the container
# COPY ${JAR_FILE} app.jar

# #unpackage jar file
# RUN mkdir -p target/dependency && (cd target/dependency; jar -xf /app.jar)

# #stage 2
# #Same Java runtime
# FROM openjdk:11-slim

# #Add volume pointing to /tmp
# VOLUME /tmp

# #Copy unpackaged application to new container
# ARG DEPENDENCY=/target/dependency
# COPY --from=build ${DEPENDENCY}/BOOT-INF/lib /app/lib
# COPY --from=build ${DEPENDENCY}/META-INF /app/META-INF
# COPY --from=build ${DEPENDENCY}/BOOT-INF/classes /app

# #execute the application
# ENTRYPOINT ["java","-cp","app:app/lib/*","com.optimagrowth.license.LicenseServiceApplication"]

# #stage 1
# #Start with a base image containing Java runtime
# FROM openjdk:17 as build

# # Add Maintainer Info
# LABEL maintainer="Illary Huaylupo <illaryhs@gmail.com>"

# # The application's jar file
# ARG JAR_FILE

# # Add the application's jar to the container
# COPY ${JAR_FILE} app.jar

# #unpackage jar file
# RUN mkdir -p target/dependency && (cd target/dependency; jar -xf /app.jar)

# #stage 2
# #Same Java runtime
# FROM openjdk:17-alpine

# #Add volume pointing to /tmp
# VOLUME /tmp

# #Copy unpackaged application to new container
# ARG DEPENDENCY=/target/dependency
# COPY --from=build ${DEPENDENCY}/BOOT-INF/lib /app/lib
# COPY --from=build ${DEPENDENCY}/META-INF /app/META-INF
# COPY --from=build ${DEPENDENCY}/BOOT-INF/classes /app

# #execute the application
# ENTRYPOINT ["java","-cp","app:app/lib/*","com.optimagrowth.license.LicenseServiceApplication"]
# #stage 1
# #Start with a base image containing Java runtime
# FROM openjdk:17 as build

# # Add Maintainer Info
# LABEL maintainer="Illary Huaylupo <illaryhs@gmail.com>"

# # The application's jar file
# ARG JAR_FILE

# # Add the application's jar to the container
# COPY ${JAR_FILE} app.jar

# #unpackage jar file
# RUN mkdir -p target/dependency && (cd target/dependency; jar -xf /app.jar)

# #stage 2
# #Same Java runtime
# FROM openjdk:17

# #Add volume pointing to /tmp
# VOLUME /tmp

# #Copy unpackaged application to new container
# ARG DEPENDENCY=/target/dependency
# COPY --from=build ${DEPENDENCY}/BOOT-INF/lib /app/lib
# COPY --from=build ${DEPENDENCY}/META-INF /app/META-INF
# COPY --from=build ${DEPENDENCY}/BOOT-INF/classes /app

# #execute the application
# ENTRYPOINT ["java","-cp","app:app/lib/*","com.optimagrowth.license.LicenseServiceApplication"]

#stage 1
#Start with a base image containing Java runtime
FROM openjdk:17 as build

# Add Maintainer Info
LABEL maintainer="Illary Huaylupo <illaryhs@gmail.com>"

# The application's jar file
ARG JAR_FILE

# Add the application's jar to the container
COPY ${JAR_FILE} app.jar

#unpackage jar file
RUN mkdir -p target/dependency && (cd target/dependency; jar -xf /app.jar)

# Stage 2
# Same Java runtime
FROM openjdk:17-alpine
 
# Add volume pointing to /tmp
VOLUME /tmp
 
# Copy unpackaged application to new container
ARG DEPENDENCY=/target/dependency
COPY --from=build ${DEPENDENCY}/BOOT-INF/lib /app/lib
COPY --from=build ${DEPENDENCY}/META-INF /app/META-INF
COPY --from=build ${DEPENDENCY}/BOOT-INF/classes /app
 
# Set environment variable for JVM options
ENV JAVA_OPTS="--add-opens java.base/java.nio.charset=ALL-UNNAMED"
 
# Execute the application
ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -cp app:app/lib/* com.optimagrowth.license.LicenseServiceApplication"]