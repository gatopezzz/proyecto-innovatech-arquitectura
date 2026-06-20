# ==========================================
# ETAPA 1: Construcción (Builder)
# ==========================================
FROM maven:3.9.4-eclipse-temurin-17 AS builder
WORKDIR /app

# 1. Copiamos solo el pom.xml primero. 
# Esto crea una capa en caché para las dependencias y acelera futuros builds.
COPY pom.xml .
RUN mvn dependency:go-offline

# 2. Copiamos el código fuente y compilamos el proyecto
COPY src ./src
RUN mvn clean package -DskipTests

# ==========================================
# ETAPA 2: Producción (Runtime)
# ==========================================
# Usamos una imagen Alpine (muy liviana) solo con el entorno de ejecución (JRE)
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# 3. SEGURIDAD: Creamos un usuario "no root" llamado "spring"
RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring

# 4. Copiamos el archivo .jar generado en la Etapa 1
COPY --from=builder /app/target/*.jar app.jar

# 5. Exponemos el puerto estándar de Spring Boot
EXPOSE 8080

# 6. Comando de inicio
ENTRYPOINT ["java", "-jar", "app.jar"]