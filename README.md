# 🚀 InnovaTech - Arquitectura Cloud y Microservicios

![AWS](https://img.shields.io/badge/AWS-ECS_Fargate-FF9900?style=for-the-badge&logo=amazonaws)
![Docker](https://img.shields.io/badge/Docker-Multi--Stage-2496ED?style=for-the-badge&logo=docker)
![GitHub Actions](https://img.shields.io/badge/CI%2FCD-GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions)
![Spring Boot](https://img.shields.io/badge/Backend-Spring_Boot-6DB33F?style=for-the-badge&logo=spring)

## 📌 Descripción del Proyecto
InnovaTech es una plataforma empresarial moderna basada en una arquitectura de microservicios. Este repositorio contiene el código fuente completo, la configuración de infraestructura como código (IaC) y los pipelines de automatización (CI/CD) para los módulos de **Ventas**, **Despachos** y el **Frontend**.

El proyecto ha sido diseñado priorizando la alta disponibilidad, la seguridad perimetral y la automatización total del despliegue mediante un entorno Cloud nativo y *Serverless*.

---

## 🏗️ Arquitectura de la Solución
La infraestructura está dividida en tres capas de responsabilidad claramente delimitadas:
1. **Capa de Presentación (Frontend):** Aplicación SPA servida a través de Nginx optimizado, aislada en subredes públicas.
2. **Capa de Lógica (Backend Serverless):** Microservicios de Ventas y Despachos ejecutados en **Amazon ECS con AWS Fargate**.
3. **Capa de Persistencia (Base de Datos):** Motor MySQL alojado en una instancia EC2, restringido mediante Security Groups para recibir tráfico únicamente del clúster de ECS.

---

## 🔐 Seguridad y Buenas Prácticas Implementadas
Este proyecto cumple con los más altos estándares de la industria tecnológica (DevSecOps):
* **Imágenes Minimalistas y Multietapa:** Uso de distribuciones `alpine` para reducir la superficie de ataque y el peso de los contenedores.
* **Principio de Mínimo Privilegio (Contenedores):** El Frontend utiliza la imagen `nginxinc/nginx-unprivileged`, ejecutándose como usuario *non-root* y exponiendo el puerto 8080 en lugar del 80.
* **Aislamiento de Red:** Uso de redes segmentadas (`public_net` y `private_net`) en Docker Compose para aislar completamente la Base de Datos del tráfico público.
* **Gestión de Accesos (AWS IAM):** Integración continua autenticada mediante Access Keys seguras en GitHub Secrets, otorgando únicamente los permisos necesarios para interactuar con ECR y ECS.

---

## ⚙️ Entorno de Desarrollo Local
El ecosistema puede ser levantado localmente utilizando **Docker Compose**. La configuración orquesta la creación de los contenedores, redes privadas, inyección de variables de entorno y volúmenes persistentes.

### Prerrequisitos
* Docker Desktop o Docker Engine instalado.
* Git.

### Instrucciones de Ejecución
1. Clonar el repositorio:
   ```bash
   git clone [https://github.com/tu-usuario/innovatech-cloud.git](https://github.com/tu-usuario/innovatech-cloud.git)
   cd innovatech-cloud