# Guion breve para grabar el video

El video debe durar máximo 3 minutos. Estos comandos cubren todos los puntos obligatorios.

```bash
type docker-compose.yml
```

```bash
docker compose up -d
```

```bash
docker ps
```

```bash
docker cp backup/Chinook_PostgreSql.sql chinook-postgres:/tmp/Chinook_PostgreSql.sql
```

```bash
docker exec -it chinook-postgres sh
```

Dentro del contenedor:

```bash
psql -U postgres < /tmp/Chinook_PostgreSql.sql
```

```bash
exit
```

Validación:

```bash
docker exec -it chinook-postgres psql -U postgres -d chinook -c "\dt"
```

```bash
docker exec -it chinook-postgres psql -U postgres -d chinook -c "SELECT artist_id, name FROM artist ORDER BY artist_id LIMIT 10;"
```
