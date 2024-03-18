# Enunciado #
1. Crear un fichero docker-compose.yml con dos servicios: drupal + mysql.
2. Hacer que el servicio drupal utilice el puerto 81.
3. Hacer que ambos contenedores usen volúmenes para persistir información.
4. Comprobar que puede acceder a localhost:81 y puede visualizar la página de configuración de drupal.
# Fichero docker-compose.yml #
```
version: '3'
services:
  drupal:
    image: drupal
    ports:
      - "81:80"
    volumes:
      - drupal_data:/var/www/html
    depends_on:
      - mysql
  mysql:
    image: mysql:5.7
    environment:
      MYSQL_DATABASE: 'drupal'
      MYSQL_USER: 'drupal'
      MYSQL_PASSWORD: 'password'
      MYSQL_ROOT_PASSWORD: 'root_password'
    volumes:
      - mysql_data:/var/lib/mysql
volumes:
  drupal_data:
  mysql_data:
```
# Servicio Drupal #
- image:drupal --> Se utiliza la versión más reciente de drupal
- ports: - "81:80" --> Se establece el puerto 81 de localhost para este servicio y se mapea al puerto 80 del container en el que se corre
- volumes: - drupal_data:/var/www/html  --> Se establece que la información de nuestro servicio se guarde en el directorio /var/www/html del container en el que se ejecuta
- depends_on: - mysql --> Se ejecuta primero el servicio mysql ya que drupal depende de él

# Servicio MySQL #
- image: mysql:5.7 --> Se utiliza la versión más reciente de mysql
- environment: MYSQL_DATABASE: 'drupal' MYSQL_USER: 'drupal' MYSQL_PASSWORD: 'password' MYSQL_ROOT_PASSWORD: 'root_password' --> Se establecen las variables de entorno de nuestro servicio
- volumes: - mysql_data:/var/lib/mysql --> Se establece que la información de nuestro servicio se guarde en el directorio /var/lib/mysql del container en el que se ejecuta
![image](https://github.com/SBaston/PractDocker/assets/101277911/8163f91f-c0a1-42b5-9863-aff06dc28b29)
![image](https://github.com/SBaston/PractDocker/assets/101277911/159165b6-3fff-411c-9927-dbc503e09d0a)


