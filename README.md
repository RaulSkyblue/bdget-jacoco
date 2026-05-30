# bdget-jacoco

# BDGET - Pipeline CI/CD con Seguridad y Contenedores

## Integrantes

* Raúl Álvarez
* Cristofer Barrueto

## Descripción del Proyecto

BDGET es un microservicio desarrollado con Spring Boot que implementa una arquitectura basada en contenedores y un pipeline CI/CD automatizado utilizando GitHub Actions.

El objetivo del proyecto es automatizar el ciclo de vida completo de la aplicación, desde la integración continua hasta el despliegue automatizado en un entorno simulado, incorporando pruebas automatizadas, análisis de seguridad y orquestación de contenedores.

---

# Arquitectura Utilizada

## Tecnologías

* Java 17
* Spring Boot 3.3.7
* Maven
* Docker
* Docker Compose
* GitHub Actions
* SonarCloud
* Snyk
* Dependabot
* Oracle Database

---

# Pipeline CI/CD

El pipeline fue implementado utilizando GitHub Actions y consta de las siguientes etapas:

## 1. Snyk Security Scan

Analiza las dependencias del proyecto para detectar vulnerabilidades conocidas.

Objetivo:

* Mejorar la seguridad del proyecto.
* Detectar dependencias vulnerables.

---

## 2. Tests Automatizados y JaCoCo

Ejecución automática de pruebas unitarias.

Objetivo:

* Garantizar estabilidad.
* Validar funcionamiento antes del despliegue.

Además, se genera un reporte de cobertura mediante JaCoCo.

---

## 3. SonarCloud

Realiza análisis estático de código.

Objetivo:

* Detectar errores.
* Detectar vulnerabilidades.
* Mejorar mantenibilidad.
* Aplicar estándares de calidad.

---

## 4. Build de la Aplicación

Compilación automática del microservicio mediante Maven.

Comando utilizado:

```bash
mvn clean package -DskipTests
```

---

## 5. Construcción de Imagen Docker

El pipeline genera automáticamente una imagen Docker del microservicio.

Objetivos:

* Portabilidad.
* Consistencia entre ambientes.
* Facilidad de despliegue.

---

## 6. Despliegue Simulado

La aplicación es desplegada automáticamente mediante Docker Compose.

Objetivos:

* Validar el despliegue.
* Simular un entorno cloud.
* Comprobar disponibilidad del servicio.

---

# Seguridad Implementada

## SonarCloud

Permite detectar:

* Bugs
* Vulnerabilidades
* Code Smells
* Problemas de mantenibilidad

## Snyk

Permite detectar:

* Dependencias vulnerables
* Riesgos de seguridad
* Librerías desactualizadas

## GitHub Secrets

Las credenciales sensibles se almacenan mediante:

* SONAR_TOKEN
* SNYK_TOKEN

Evita exponer información sensible dentro del repositorio.

## Dependabot

Dependabot monitorea automáticamente las dependencias del proyecto y genera alertas cuando existen versiones vulnerables o desactualizadas.

---

# Escalabilidad

La escalabilidad fue considerada mediante el uso de contenedores Docker y Docker Compose.

La arquitectura permite:

* Replicar instancias del microservicio.
* Escalar horizontalmente la aplicación.
* Mantener consistencia entre ambientes.

Ejemplo de escalamiento:

```bash
docker compose up --scale bdget=3
```

Esto permite ejecutar múltiples instancias del microservicio para responder a un aumento en la demanda.

---

# Orquestación de Contenedores

La orquestación se realiza mediante Docker Compose.

Beneficios:

* Administración centralizada.
* Configuración reproducible.
* Facilidad de despliegue.
* Escalabilidad futura.

---

# Trazabilidad

La trazabilidad se garantiza mediante:

* Control de versiones con GitHub.
* Historial de commits.
* Ejecuciones registradas en GitHub Actions.
* Reportes de SonarCloud.
* Reportes de Snyk.
* Artefactos generados automáticamente.

Esto permite seguir el recorrido completo de la aplicación desde el desarrollo hasta el despliegue.

---

# Evidencias

## GitHub Actions

<img width="1440" height="111" alt="image" src="https://github.com/user-attachments/assets/6001e876-ec18-482e-827f-e1bab7639579" />


## SonarCloud

(Agregar captura)

## Snyk

(Agregar captura)

## Docker Compose

(Agregar captura)

---

## Despliegue en AWS Academy

Además del entorno local y la validación mediante Docker Compose en GitHub Actions, el proyecto se encuentra desplegado en AWS Academy utilizando Infraestructura como Código (IaC) con Terraform.

### Infraestructura provisionada

* VPC personalizada
* Subred pública
* Internet Gateway
* Tabla de rutas
* Security Group
* Instancia EC2 Amazon Linux 2

### Tecnologías utilizadas

* Terraform
* AWS Academy
* Amazon EC2
* Docker
* GitHub Actions

### Flujo de despliegue

1. Terraform crea automáticamente la infraestructura en AWS Academy.
2. GitHub Actions ejecuta el pipeline CI/CD.
3. El pipeline realiza:

   * Análisis de seguridad con Snyk.
   * Ejecución de pruebas unitarias con JaCoCo.
   * Análisis de calidad con SonarCloud.
   * Construcción del artefacto JAR.
   * Construcción de la imagen Docker.
4. GitHub Actions se conecta por SSH a la instancia EC2.
5. Se actualiza el código fuente mediante Git.
6. Se reconstruye y despliega automáticamente el contenedor Docker.

### Acceso a la aplicación

La aplicación se ejecuta dentro de un contenedor Docker en una instancia EC2 de AWS Academy y puede ser accedida mediante su dirección IP pública y el puerto 8080.



# Conclusión

La solución implementa un pipeline CI/CD completo que automatiza la integración continua, validación de calidad, análisis de seguridad, contenerización y despliegue automatizado del microservicio, asegurando trazabilidad, escalabilidad y buenas prácticas DevOps.
