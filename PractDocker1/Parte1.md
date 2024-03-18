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
