# COMPLETAR  

# Reflexión sobre el Aprendizaje: Configuración de SonarQube y PostgreSQL con Docker Compose

## Conocimientos Previos

Antes de realizar esta práctica, tenía una comprensión general de Docker y Docker Compose, así como conocimientos básicos sobre cómo funcionan los contenedores y la orquestación de servicios. Sabía cómo iniciar contenedores individuales y cómo mapear volúmenes y puertos. Sin embargo, mi experiencia en la configuración de servicios más complejos como SonarQube y PostgreSQL juntos, y en el uso de características avanzadas de Docker Compose como `healthchecks`, era limitada.

## Aprendizajes Clave

Después de completar esta práctica, he adquirido una serie de conocimientos y habilidades que han mejorado significativamente mi formación profesional en el ámbito de DevOps y la administración de sistemas.

1. **Integración de Servicios con Docker Compose:**
   - Aprendí cómo configurar múltiples servicios que dependen entre sí usando Docker Compose. En este caso, cómo SonarQube y PostgreSQL pueden interactuar a través de una red compartida.
   - La configuración de variables de entorno fue crucial para asegurar que ambos servicios pudieran comunicarse correctamente, especialmente en entornos donde la seguridad y la configuración precisa son críticas.

2. **Persistencia de Datos con Volúmenes:**
   - Me familiaricé con la importancia de los volúmenes en Docker para la persistencia de datos. Aprendí a mapear correctamente los directorios de los contenedores a volúmenes nombrados, asegurando que los datos de la base de datos y de SonarQube se preserven incluso si los contenedores son reiniciados.

3. **Healthchecks:**
   - Entendí la importancia de los `healthchecks` para monitorizar y asegurar la disponibilidad y el correcto funcionamiento de los servicios. Implementé comandos específicos para verificar la salud de PostgreSQL (`pg_isready`) y SonarQube (`curl`), lo que me enseñó a diagnosticar y resolver problemas de disponibilidad de los servicios.

4. **Configuración de Redes:**
   - Aprendí cómo utilizar redes de tipo bridge en Docker Compose para permitir la comunicación entre los contenedores. Esto fue esencial para que los servicios SonarQube y PostgreSQL pudieran interactuar sin problemas.

5. **Variables de Entorno Específicas:**
   - Investigando las variables de entorno específicas necesarias para la configuración de SonarQube y PostgreSQL, comprendí mejor cómo cada servicio utiliza estas variables para conectarse y operar en un entorno contenedorizado.

## Problemas y Soluciones

Durante la práctica, encontré algunos problemas que me proporcionaron una valiosa experiencia en la resolución de problemas:

1. **Problema de Conexión entre SonarQube y PostgreSQL:**
   - **Problema:** Inicialmente, SonarQube no podía conectarse a PostgreSQL. Recibía errores de conexión en los logs de SonarQube.
   - **Solución:** Verifiqué las variables de entorno y me aseguré de que la `SONAR_JDBC_URL` estuviera correctamente configurada con el nombre del servicio PostgreSQL (`postgresql-service`). Además, me aseguré de que el contenedor de PostgreSQL estuviera completamente levantado y saludable antes de que SonarQube intentara conectarse.

2. **Configuración de Healthchecks:**
   - **Problema:** Al principio, los `healthchecks` no estaban reportando correctamente el estado de los servicios.
   - **Solución:** Ajusté los comandos y parámetros de `healthcheck`, especialmente el comando `pg_isready` para PostgreSQL y `curl` para SonarQube, y ajusté los intervalos y tiempos de espera (`timeout`, `interval`, `retries`) para reflejar mejor el tiempo necesario para que los servicios se inicien y estén disponibles.

3. **Persistencia de Datos:**
   - **Problema:** Los datos no se persistían correctamente entre los reinicios de los contenedores.
   - **Solución:** Revisé la configuración de los volúmenes y me aseguré de que estuvieran correctamente mapeados a los directorios necesarios en los contenedores (`/var/lib/postgresql/data` para PostgreSQL y `/opt/sonarqube/*` para SonarQube). Esto garantizó que los datos se almacenaran fuera de los contenedores y se mantuvieran persistentes.

## Impacto en la Formación Profesional

Completar esta práctica me ha dado una comprensión más profunda y práctica del uso de Docker Compose para orquestar servicios complejos. Estas habilidades son fundamentales en el campo de DevOps y la ingeniería de software moderna, donde la capacidad de desplegar y administrar aplicaciones de manera eficiente y confiable es crucial.

En el futuro, podré aplicar estos conocimientos a una amplia variedad de proyectos, desde la configuración de entornos de desarrollo hasta el despliegue de aplicaciones en producción. La experiencia adquirida me permitirá abordar con confianza desafíos similares y contribuir a la automatización y optimización de los flujos de trabajo en entornos de desarrollo y producción.

## Prueba de la Configuración

Para completar la práctica y asegurarme de que todo funcionaba correctamente, seguí estos pasos:

1. **Guardar el archivo:** Guarda el contenido en un archivo llamado `docker-compose.yaml`.

2. **Iniciar los servicios:** Ejecuta el siguiente comando para iniciar los servicios:
   ```bash
   docker-compose up -d
