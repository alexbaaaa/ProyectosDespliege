# Tomcat y Maven: Aplicaiones Java
¡Hola! A continuación, te proporciono un archivo `README.md` adecuado para tu repositorio [Tomcat-Maven](https://github.com/alexbaaaa/ProyectosDespliege/tree/main/Tomcat-Maven). Este archivo está diseñado para guiar a los usuarios en la configuración y despliegue de una aplicación web Java utilizando Maven y Apache Tomcat.

```markdown
# Tomcat-Maven

Este proyecto demuestra cómo configurar y desplegar una aplicación web Java utilizando Apache Maven y Apache Tomcat.

## Prerrequisitos

Antes de comenzar, asegúrate de tener instalados los siguientes componentes:

- **Apache Tomcat 9**: Un servidor web y contenedor de servlets. Puedes descargarlo desde [tomcat.apache.org](https://tomcat.apache.org/download-90.cgi).

- **Apache Maven**: Una herramienta de gestión y comprensión de proyectos. Para instalar Maven en Debian, puedes seguir estos pasos:

  ```bash
  sudo apt update
  sudo apt install maven
  ```

  Para verificar la instalación, ejecuta:

  ```bash
  mvn -v
  ```

  Deberías ver información sobre la versión instalada de Maven.

## Configuración de Apache Tomcat

1. **Crear un usuario con permisos de despliegue**:

   Edita el archivo `tomcat-users.xml`, que generalmente se encuentra en `/etc/tomcat9/tomcat-users.xml`, y añade el siguiente contenido:

   ```xml
   <role rolename="manager-script"/>
   <user username="admin" password="your_password" roles="manager-script"/>
   ```

   Reemplaza `your_password` con una contraseña segura de tu elección.

## Configuración de Maven

1. **Configurar las credenciales en Maven**:

   Edita el archivo `settings.xml` de Maven, ubicado en `~/.m2/settings.xml`, y añade lo siguiente dentro de la sección `<servers>`:

   ```xml
   <servers>
       <server>
           <id>TomcatServer</id>
           <username>admin</username>
           <password>your_password</password>
       </server>
   </servers>
   ```

   Asegúrate de que el `<id>` coincida con el que se utilizará en el `pom.xml` del proyecto.

## Configuración del Proyecto Maven

En el archivo `pom.xml` de tu proyecto, añade la siguiente configuración dentro de la sección `<build>`:

```xml
<build>
    <finalName>tomcat-war-deployment</finalName>
    <plugins>
        <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.2</version>
            <configuration>
                <url>http://localhost:8080/manager/text</url>
                <server>TomcatServer</server>
                <path>/despliegue</path>
            </configuration>
        </plugin>
    </plugins>
</build>
```

- `<url>`: La URL del Manager de Tomcat.
- `<server>`: Debe coincidir con el `<id>` configurado en `settings.xml`.
- `<path>`: La ruta de contexto donde se desplegará la aplicación.

## Despliegue de la Aplicación

Para desplegar la aplicación en Tomcat, utiliza el siguiente comando de Maven:

```bash
mvn tomcat7:deploy
```

Otros comandos útiles incluyen:

- **Redeploy**: Para volver a desplegar la aplicación:

  ```bash
  mvn tomcat7:redeploy
  ```

- **Undeploy**: Para eliminar la aplicación del servidor:

  ```bash
  mvn tomcat7:undeploy
  ```

## Acceso a la Aplicación

Una vez desplegada, puedes acceder a la aplicación en:

```
http://localhost:8080/despliegue
```

## Recursos Adicionales

Para más información sobre cómo desplegar aplicaciones web en Tomcat utilizando Maven, puedes consultar los siguientes recursos:

- [Práctica 3.1: Instalación de Tomcat y Maven para despliegue de aplicaciones web](https://raul-profesor.github.io/DEAW/P3.1-Tomcat/)

- [Cómo desplegar un proyecto web en Tomcat con Maven](https://hanolisite.wordpress.com/2018/05/01/como-de-desplegar-un-proyecto-web-en-tomcat-con-maven/)

## Autor

Este proyecto es mantenido por [alexbaaaa](https://github.com/alexbaaaa).

```

Este `README.md` proporciona instrucciones claras sobre cómo configurar y desplegar una aplicación web Java utilizando Maven y Tomcat. Además, incluye enlaces a recursos adicionales que pueden ser útiles para los usuarios. 