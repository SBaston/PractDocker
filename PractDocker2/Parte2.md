# Enunciado #
1. Crear un fichero docker-compose.yml con dos servicios: wordpress + mariadb.
2. Hacer que el servicio wordpress utilice el puerto 82.
3. Hacer que ambos contenedores usen la red redDocker .
4. Comprobar que puede acceder a localhost:82 y puede visualizar la página de configuración de wordpress.

# Fichero docker-compose.yml #
```
version: '3'
services:
  wordpress:
    image: wordpress
    ports:
      - "82:80"
    networks:
      - redDocker
    depends_on:
      - mariadb
  mariadb:
    image: mariadb
    environment:
      MYSQL_ROOT_PASSWORD: example
    networks:
      - redDocker

networks:
  redDocker:
```
# Servicio Wordpress #
- image: wordpress --> Se utiliza la versión más reciente de Wordpress
- ports: - "82:80" --> Se establece el puerto 82 de localhost para este servicio y se mapea al puerto 80 del container en el que se corre
- networks: - redDocker --> Se define la red con la que se comunicarán estos containers (por default es bridge porque debajo no se ha especificado ninguna por lo que se utilizará este) 
- depends_on: - mariadb --> Se ejecuta primero el servicio mariadb ya que Wordpress depende de él

# Servicio MariaDB #
- image: mariadb  --> Se utiliza la versión más reciente de MariaDB
- environment: MYSQL_ROOT_PASSWORD: example --> Se establece la variable de entorno 
- networks: - redDocker  --> Se define la red con la que se comunicarán estos containers

![image](https://github.com/SBaston/PractDocker/assets/101277911/9523619f-45d4-4c45-af73-ea6ea78ea52d)
![image](https://github.com/SBaston/PractDocker/assets/101277911/5b171687-798f-4228-a2c2-7681b68c46d3)

