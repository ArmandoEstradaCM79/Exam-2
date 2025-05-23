# Usamos imagen oficial OpenJDK build
FROM maven:3.9.0-eclipse-temurin-17 AS build

WORKDIR /app

COPY pom.xml .


# Construye el JAR
RUN mvn clean package -DskipTests

# Usamos imagen oficial OpenJDK runtime
FROM eclipse-temurin:17-jdk

WORKDIR /app

# Copia el JAR generado desde el stage anterior
COPY target/login-system-0.0.1-SNAPSHOT.jar app.jar

# Copia wait-for-it.sh al contenedor
COPY wait-for-it.sh /wait-for-it.sh
RUN chmod +x /wait-for-it.sh

# Espera a que MySQL esté listo y luego ejecuta la aplicación
ENTRYPOINT ["/wait-for-it.sh", "db:3306", "--", "java", "-jar", "app.jar"]

# Expone el puerto que usa la app
EXPOSE 8080

