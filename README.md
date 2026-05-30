# Backup y Restore de Base de Datos

Repositorio para la tarea de Administración y continuidad de aplicaciones empresariales. El objetivo es levantar PostgreSQL con Docker Compose, restaurar el backup de la base de datos Chinook y validar que los datos fueron cargados correctamente.

## Arquitectura utilizada

La solución usa un contenedor Docker con PostgreSQL 16 definido en `docker-compose.yml`.

- Servicio: `postgres`
- Contenedor: `chinook-postgres`
- Usuario: `postgres`
- Password: `postgres`
- Puerto local: `5432`
- Persistencia: volumen Docker `postgres_data`
- Backup: `backup/Chinook_PostgreSql.sql`

El volumen `postgres_data` permite conservar los datos del contenedor aunque el servicio se detenga o se vuelva a iniciar.

## Requisitos

- Docker Desktop instalado y en ejecución.
- Git instalado.
- Terminal PowerShell, CMD o Git Bash.

## Ejecución

Levantar el contenedor de PostgreSQL:

```bash
docker compose up -d
```

Verificar que el contenedor está en ejecución:

```bash
docker ps
```

Copiar el archivo de backup al contenedor:

```bash
docker cp backup/Chinook_PostgreSql.sql chinook-postgres:/tmp/Chinook_PostgreSql.sql
```

Ingresar al contenedor:

```bash
docker exec -it chinook-postgres sh
```

Ejecutar el restore dentro del contenedor:

```bash
psql -U postgres < /tmp/Chinook_PostgreSql.sql
```

Salir del contenedor:

```bash
exit
```

## Validación

Listar las bases de datos disponibles:

```bash
docker exec -it chinook-postgres psql -U postgres -c "\l"
```

Listar las tablas restauradas en la base de datos `chinook`:

```bash
docker exec -it chinook-postgres psql -U postgres -d chinook -c "\dt"
```

Consultar cantidad de registros por tabla:

```bash
docker exec -it chinook-postgres psql -U postgres -d chinook -c "SELECT 'artist' AS tabla, COUNT(*) AS registros FROM artist UNION ALL SELECT 'album', COUNT(*) FROM album UNION ALL SELECT 'track', COUNT(*) FROM track UNION ALL SELECT 'customer', COUNT(*) FROM customer UNION ALL SELECT 'invoice', COUNT(*) FROM invoice;"
```

Consulta simple de evidencia:

```bash
docker exec -it chinook-postgres psql -U postgres -d chinook -c "SELECT artist_id, name FROM artist ORDER BY artist_id LIMIT 10;"
```

## Conceptos

Un backup es una copia de seguridad de datos que se guarda para proteger la información ante errores, fallos, eliminación accidental o incidentes.

Un restore es el proceso de recuperación de datos desde un backup hacia una base de datos, para devolver la información a un estado funcional.

## Limpieza del ambiente

Detener el contenedor:

```bash
docker compose down
```

Detener el contenedor y borrar el volumen de datos:

```bash
docker compose down -v
```

## Evidencia esperada

Para el video se debe mostrar:

1. El archivo `docker-compose.yml`.
2. El contenedor levantado con `docker compose up -d` y `docker ps`.
3. La copia del backup con `docker cp`.
4. El ingreso al contenedor con `docker exec -it chinook-postgres sh`.
5. La ejecución del restore con `psql -U postgres < /tmp/Chinook_PostgreSql.sql`.
6. La validación con `\dt` o con una consulta `SELECT`.

