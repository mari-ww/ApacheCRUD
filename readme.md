# Apache Cassandra

- [ ] Deploy
- [ ] CQLSH
- [ ] Keyspace
- [ ] Tabelas
- [ ] Insert
- [ ] Select
- [ ] Update
- [ ] Alter Table
- [ ] Delete

## Deploy

```bash
docker-compose up -d

docker exec -it cassandra-node1 nodetool status
```

## CQLSH

```bash
docker exec -it cassandra-node1 cqlsh
```

## Keyspace
```sql
CREATE KEYSPACE pets_db WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 3 } AND DURABLE_WRITES = true;

USE pets_db;
```

## Criar tabela
```sql
CREATE TABLE heartrate( pet_chip_id uuid, owner uuid, time timestamp, heart_rate int, PRIMARY KEY (pet_chip_id, time) );
```

## Inserir registros
```sql
INSERT INTO heartrate (pet_chip_id, owner, time, heart_rate) VALUES ( a2a60505-3e17-4ad4-8e1a-f11139caa1cc, 642adfee-6ad9-4ca5-aa32-a72e506b8ad8, '2021-05-01 01:00 +0000', 100 );

INSERT INTO heartrate (pet_chip_id, owner, time, heart_rate) VALUES ( a2a60505-3e17-4ad4-8e1a-f11139caa1cc, 642adfee-6ad9-4ca5-aa32-a72e506b8ad8, '2021-05-01 01:01 +0000', 101 );
```

## Select
```sql
SELECT * FROM heartrate
  WHERE pet_chip_id = a2a60505-3e17-4ad4-8e1a-f11139caa1cc;
```

## Update
```sql
UPDATE heartrate
  SET heart_rate = 105
  WHERE pet_chip_id = a2a60505-3e17-4ad4-8e1a-f11139caa1cc
    AND time = '2021-05-01 01:00 +0000';
```

## Alter Table
# add coluna
```sql
ALTER TABLE heartrate ADD location text;
```

# remove coluna
```sql
ALTER TABLE heartrate DROP owner;
```

## Delete
# excluir linha
```sql
DELETE FROM heartrate WHERE pet_chip_id = a2a60505-3e17-4ad4-8e1a-f11139caa1cc AND time = '2021-05-01 01:01 +0000';
```

#  excluir colunas
```sql
DELETE FROM heartrate WHERE pet_chip_id = a2a60505-3e17-4ad4-8e1a-f11139caa1cc;
```

# excluir tabela
```sql
DROP TABLE heartrate;
```