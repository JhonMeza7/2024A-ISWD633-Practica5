# Ejercicio
Configurar SonarQube utilizando Docker Compose, para esto necesitas dos servicios:
- Servicio: SonarQube
- Desde el host es necesario acceder a SonarQube por lo que necesitas mapear el puerto correspondiente.
- Servicio: PostgreSQL (existen otras opciones: Microsoft SQL Server, Oracle)
- Coloca un healtcheck para cada uno de los servicios.
- Los dos servicios deben pertenecer a uan red de tipo bridge
- Investiga cuáles son los volúmenes necesarios para cada servicio
- Investiga cuáles son las variables de entorno para que los servicios funcionen de manera adecuada.
  
# Una vez creado tu archivo .yaml realiza la respectiva prueba 

[Uploadversion: '3.8'

services:
  postgresql-service:
    image: postgres:14
    container_name: postgresql-container
    environment:
      POSTGRES_USER: sonarqube
      POSTGRES_PASSWORD: sonarqube_password
      POSTGRES_DB: sonarqube_db
    volumes:
      - postgresql-data:/var/lib/postgresql/data
    networks:
      - sonarnet
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U $POSTGRES_USER -d $POSTGRES_DB -h localhost"]
      interval: 20s
      timeout: 10s
      retries: 5
      start_period: 30s

  sonarqube-service:
    image: sonarqube:community
    container_name: sonarqube-container
    ports:
      - "9000:9000"
    environment:
      SONAR_JDBC_URL: jdbc:postgresql://postgresql-service:5432/sonarqube_db
      SONAR_JDBC_USERNAME: sonarqube
      SONAR_JDBC_PASSWORD: sonarqube_password
      SONARQUBE_JDBC_MAXACTIVE: 60
      SONARQUBE_JDBC_MAXIDLE: 5
      SONARQUBE_JDBC_MINIDLE: 2
      SONARQUBE_JDBC_MAXWAIT: 10000
    volumes:
      - sonarqube-data:/opt/sonarqube/data
      - sonarqube-logs:/opt/sonarqube/logs
      - sonarqube-extensions:/opt/sonarqube/extensions
    networks:
      - sonarnet
    healthcheck:
      test: ["CMD-SHELL", "curl -f http://localhost:9000 || exit 1"]
      interval: 20s
      timeout: 20s
      retries: 5
      start_period: 60s

volumes:
  postgresql-data:
  sonarqube-data:
  sonarqube-logs:
  sonarqube-extensions:

networks:
  sonarnet:
    driver: bridge
ing compose2.yaml…]()

# COMPLETAR CON UNA CAPTURA DE PANTALLA LUEGO DE EJECUTAR EL ARCHIVO
![image](https://github.com/JhonMeza7/2024A-ISWD633-Practica5/assets/89060377/3d559172-bc91-45b4-9b68-52ee90899d2c)

# ACCEDER A LOCALHOST:puertoDefinido para ingresar a SonarQube
![image](https://github.com/JhonMeza7/2024A-ISWD633-Practica5/assets/89060377/6e3aaa10-1cec-410a-90c9-3e1bcbdfe609)
![image](https://github.com/JhonMeza7/2024A-ISWD633-Practica5/assets/89060377/0eef9a60-c954-4a45-8ba4-aeb5c504ede3)

