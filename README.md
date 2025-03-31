# Proyecto-Clientes-Alianza

Esta aplicación, desarrollada con **Angular Material** en el frontend y **Spring Boot** en el backend, está conteinerizada con **Docker**. Permite la gestión de clientes mediante un **CRUD** con:

- Filtros de búsqueda por distintos criterios.  
- Tabla con información de clientes registrados.  
- Exportación de datos en formato **CSV**.  

> **Objetivo:** Demostrar habilidades en arquitectura escalable, patrones de diseño y despliegue con contenedores.  

## Tecnologías Utilizadas  

- **Backend:** Java, Spring Boot  
- **Frontend:** Angular, Angular Material  
- **Infraestructura:** Docker, Nginx  
- **Control de Versiones:** Git  

## Arquitectura del Proyecto  

### Diseño General  

El proyecto está diseñado para ser escalable y modular. El backend provee servicios **REST**, mientras que el frontend interactúa con ellos mediante un proxy inverso configurado en **Nginx**. Se siguen principios de **separación de responsabilidades** para facilitar su mantenimiento y extensibilidad.  

### Esquema de Capas  

El proyecto sigue el modelo de **arquitectura hexagonal (Clean Architecture)** para desacoplar la lógica de negocio de las tecnologías subyacentes.  

Las principales capas son:  

1. **Dominio**: Contiene entidades y objetos de valor, asegurando independencia tecnológica.  
2. **Aplicación**: Define casos de uso y reglas de negocio. Interactúa con infraestructura y presentación.  
3. **Infraestructura**: Implementaciones de persistencia, conexiones a bases de datos y configuraciones de frameworks.  
4. **Presentación**: Capa responsable de la interacción con el usuario a través del frontend.  
![Arquitectura Hexagonal](docs/arquitectura_hexagonal.png)

## Flujo de Datos  

### Interacción de Componentes  

1. El usuario interactúa con el frontend (**Angular**).  
2. Las solicitudes se envían mediante **Nginx** como proxy inverso al backend (**Spring Boot**).  
3. El backend procesa la solicitud y persiste los datos en una base de datos en memoria (**H2**).  
4. La respuesta se retorna al frontend para su visualización.  

## Despliegue e Infraestructura  

### Clonación del Proyecto  

Para clonar este proyecto con los repositorios de frontend y backend incluidos como submódulos, ejecute:  

```sh
git clone --recurse-submodules https://github.com/TU_USUARIO/Proyecto-Cliente-Alianza.git


## Ejecución en Local y en Producción  

### Instalación y Configuración  

1. Instalar y ejecutar **Docker Desktop**.  
2. Clonar el repositorio con todos los componentes (**backend, frontend y Docker Compose**).  
3. Ejecutar el siguiente comando:  

   ```sh
   docker-compose up --build
4. Acceder a http://localhost en el navegador.


## Despliegue en Producción  

Para un entorno de producción, se recomienda configurar un servidor con **Docker y Nginx** para exponer los servicios de manera segura.  

### Configuración de Nginx  

El proyecto utiliza **Nginx** como proxy inverso para gestionar el tráfico entre el frontend y el backend.  

Se recomienda la siguiente configuración en `nginx.conf`:  

```nginx
server {
    listen 80;
    server_name localhost;

    location / {
        root /usr/share/nginx/html;
        index index.html;
        try_files $uri /index.html;
    }

    location /api/ {
        proxy_pass http://backend:8080/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

## Seguridad  

### Mejoras Pendientes  

- Implementar un **sistema de autenticación y autorización** con credenciales de usuario.  
- Manejo de **variables de entorno** para gestionar configuraciones según el entorno de despliegue.  
- Configuración de **CORS** en el backend para pruebas locales.  

## Buenas Prácticas y Decisiones Técnicas  

### Patrones de Diseño Aplicados  

- **Repository Pattern**: Manejo de persistencia desacoplada.  
- **Singleton**: Uso en `RequestResponseLoggingFilter` para la gestión de logs.  
- **Adapter**: Implementado en la comunicación entre capas, por ejemplo, al usar `JpaRepository`.  

### Decisiones Claves  

- Uso de **Angular Material** para una interfaz visual moderna.  
- Implementación de **módulos standalone en Angular** para facilitar la mantenibilidad.  
- Infraestructura basada en **Docker y Nginx** para escalabilidad.  
- Estructura de **4 capas**: **Dominio, Aplicación, Infraestructura, Presentación**.  

## Pruebas y Calidad de Código  

### Pruebas Implementadas  

- **Pruebas Unitarias** en el backend con:  
  - **JUnit 5** (framework de pruebas en Java).  
  - **Mockito** (para simulación de dependencias y pruebas de servicios).  

## Referencias y Recursos Adicionales  

- [Documentación oficial de **Spring Boot, Angular, Docker y Nginx**.](https://docs.spring.io/spring-boot/docs/current/reference/html/)
- https://angular.io/docs
- https://docs.docker.com/?utm_source=chatgpt.com
- [Guías sobre **arquitectura hexagonal y Clean Architecture**.  ](https://medium.com/%40oliveraluis11/arquitectura-hexagonal-con-spring-boot-parte-1-57b797eca69c?utm_source=chatgpt.com)
- https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
- https://github.com/kamranahmedse/developer-roadmap

## Conclusión  

Este documento proporciona una guía clara sobre el desarrollo, despliegue y estructura del **Proyecto-Clientes-Alianza**.  
Se destacan buenas prácticas en **arquitectura, patrones de diseño y gestión de infraestructura con Docker**, asegurando una aplicación **escalable y mantenible**.  
