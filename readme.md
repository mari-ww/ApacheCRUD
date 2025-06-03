# CRUD Apache Cassandra

## Como rodar o Cassandra com Docker

```bash
docker-compose up -d
```

## Acessando o CQL Shell (cqlsh)...

```bash
docker exec -it cassandra-node1 cqlsh
```

## Criando um Keyspace...
```sql
CREATE KEYSPACE undertale_db WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 3 } AND DURABLE_WRITES = true;

USE undertale_db;
```

## Criando a Tabela battles...
```sql
CREATE TABLE battles ( player_id uuid, encounter_time timestamp, character_name text, encounter_type text,damage_caused int,fled boolean,PRIMARY KEY (player_id, encounter_time));
```

## Inserindo Dados...
```sql
INSERT INTO battles (player_id, encounter_time, character_name, encounter_type, damage_caused, fled) VALUES (123e4567-e89b-12d3-a456-426614174000, '2025-06-03 15:00 +0000', 'Sans', 'Battle', 12, false);

INSERT INTO battles (player_id, encounter_time, character_name, encounter_type, damage_caused, fled) VALUES (123e4567-e89b-12d3-a456-426614174000, '2025-06-03 15:05 +0000', 'Papyrus', 'Battle', 8, true);
```

## Consultando Dados...
```sql
SELECT * FROM battles WHERE player_id = 123e4567-e89b-12d3-a456-426614174000;
```

## Atualizando Registros...
```sql
UPDATE battles SET damage_caused = 15, fled = false WHERE player_id = 123e4567-e89b-12d3-a456-426614174000 AND encounter_time = '2025-06-03 15:05 +0000';
```

## Alterando a Tabela...
- [x] adiciona coluna
```sql
ALTER TABLE battles ADD location text;
```

- [x] remove coluna
```sql
ALTER TABLE battles DROP encounter_type;
```

## Deletando Dados...
- [x] exclui linha
```sql
DELETE FROM battles WHERE player_id = 123e4567-e89b-12d3-a456-426614174000 AND encounter_time = '2025-06-03 15:00 +0000';
```

- [x] exclui colunas
```sql
DELETE damage_caused, fled FROM battles WHERE player_id = 123e4567-e89b-12d3-a456-426614174000;
```

- [x] exclui tabela
```sql
DROP TABLE battles;
```
