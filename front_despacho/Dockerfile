# ==========================================
# ETAPA 1: Construcción (Builder)
# ==========================================
FROM node:20-alpine AS builder
WORKDIR /app

# 1. Copiamos solo los archivos de dependencias primero (Limpieza de capas / Caché)
COPY package*.json ./
RUN npm install

# 2. Copiamos el resto del código fuente
COPY . .

# 3. Construimos el proyecto para producción (Vite generará una carpeta "dist")
RUN npm run build

# ==========================================
# ETAPA 2: Producción (Runtime)
# ==========================================
# Usamos una imagen oficial de Nginx preconfigurada como USUARIO NO ROOT
FROM nginxinc/nginx-unprivileged:alpine

# 4. Copiamos los archivos compilados de la Etapa 1 a la carpeta pública de Nginx
# Nota: Vite por defecto genera el build en la carpeta /app/dist
COPY --from=builder /app/dist /usr/share/nginx/html

# 5. Exponemos el puerto 8080 (los usuarios no root no pueden usar el puerto 80 por seguridad)
EXPOSE 8080

# 6. Comando de inicio del servidor web
CMD ["nginx", "-g", "daemon off;"]