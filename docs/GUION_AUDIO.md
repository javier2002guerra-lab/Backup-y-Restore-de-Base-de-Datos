# Guion de audio para el video

En este video muestro el proceso de backup y restore de la base de datos Chinook usando PostgreSQL y Docker Compose.

Primero se muestra el archivo `docker-compose.yml`, donde se define el servicio de PostgreSQL, el usuario, la contraseña, el puerto `5432` y el volumen de persistencia.

Después se levanta el contenedor con el comando `docker compose up -d`. Luego se valida que el contenedor está activo usando `docker ps`, donde aparece el contenedor `chinook-postgres`.

El siguiente paso es copiar el archivo de backup `Chinook_PostgreSql.sql` al contenedor usando `docker cp`. Este archivo contiene las instrucciones SQL para crear la base de datos Chinook, sus tablas y sus registros.

Luego se ejecuta el restore dentro del contenedor con `psql -U postgres < /tmp/Chinook_PostgreSql.sql`. Este comando restaura la base de datos a partir del archivo de respaldo.

Finalmente se valida la restauración conectándose a la base `chinook`, listando las tablas con `\dt` y ejecutando consultas para comprobar que los datos fueron cargados correctamente. Se observan tablas como `artist`, `album`, `track`, `customer` e `invoice`, junto con sus cantidades de registros.

Con esto se demuestra que el contenedor PostgreSQL fue levantado correctamente, que el backup fue restaurado y que la información quedó disponible para su uso.
