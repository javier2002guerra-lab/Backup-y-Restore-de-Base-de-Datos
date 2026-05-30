# Backup y Restore de Base de Datos

## Nombre completo

Javier Alejandro Guerra Zepeda

## Arquitectura utilizada

Se utilizó Docker Compose para levantar un servicio de PostgreSQL 16 en un contenedor llamado `chinook-postgres`. La base de datos usa el usuario `postgres`, contraseña `postgres` y expone el puerto `5432`. La persistencia se maneja con un volumen Docker llamado `postgres_data`, lo cual permite conservar los datos aunque el contenedor sea reiniciado.

El archivo de respaldo utilizado fue `backup/Chinook_PostgreSql.sql`, el cual crea y carga la base de datos `chinook`.

## Pasos realizados

1. Se creó el archivo `docker-compose.yml` con el servicio de PostgreSQL.
2. Se levantó el contenedor con `docker compose up -d`.
3. Se verificó el contenedor activo con `docker ps`.
4. Se copió el backup al contenedor con `docker cp backup/Chinook_PostgreSql.sql chinook-postgres:/tmp/Chinook_PostgreSql.sql`.
5. Se ingresó al contenedor con `docker exec -it chinook-postgres sh`.
6. Se ejecutó el restore con `psql -U postgres < /tmp/Chinook_PostgreSql.sql`.
7. Se validó la restauración listando tablas y ejecutando consultas sobre la base `chinook`.

## Backup y restore

Un backup es una copia de seguridad de la información de una base de datos. Sirve para proteger los datos ante errores humanos, fallos técnicos, daños en el sistema o incidentes de seguridad.

Un restore es el procedimiento de recuperación de la información desde un backup. En esta tarea, el restore permitió crear nuevamente la base de datos Chinook dentro del contenedor PostgreSQL y cargar sus tablas y registros.

## Validación realizada

Se verificó que la base de datos `chinook` fue creada correctamente y que las tablas principales quedaron disponibles. Para validar los datos se usaron comandos como:

```bash
docker exec -it chinook-postgres psql -U postgres -d chinook -c "\dt"
```

```bash
docker exec -it chinook-postgres psql -U postgres -d chinook -c "SELECT artist_id, name FROM artist ORDER BY artist_id LIMIT 10;"
```

También se puede verificar la cantidad de registros:

```bash
docker exec -it chinook-postgres psql -U postgres -d chinook -c "SELECT 'artist' AS tabla, COUNT(*) AS registros FROM artist UNION ALL SELECT 'album', COUNT(*) FROM album UNION ALL SELECT 'track', COUNT(*) FROM track UNION ALL SELECT 'customer', COUNT(*) FROM customer UNION ALL SELECT 'invoice', COUNT(*) FROM invoice;"
```

## Enlace al video en Google Drive

Pegar aquí el enlace del video con permisos de visualización:

`ENLACE_DEL_VIDEO`

## Enlace al repositorio público de GitHub

https://github.com/javier2002guerra-lab/Backup-y-Restore-de-Base-de-Datos
