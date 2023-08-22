# Pre test Commands
Firstly boot up the docker environment by executing this command in this folder:
```bash
docker compose up -d
```
Before testing the environment we need to create a table in Apache Kudu via Impala:
```bash
docker exec -it impala impala-shell
```
In the Impala shell, use the following commands to insert a new table called jogos and equipes
```SQL
connect;   -- (run again if not successful)

CREATE TABLE jogos (
  partida STRING,
  mapa STRING,
  equipe1 STRING,
  equipe2 STRING,
  vitorioso STRING, 
  ct STRING,
  tr STRING,
  PRIMARY KEY(partida, mapa)
)
STORED AS KUDU;

CREATE TABLE equipes (
  equipe STRING,
  jogos DECIMAL(8, 5),
  vitorias DECIMAL(8, 5),
  derrotas DECIMAL(8, 5),
  md3 DECIMAL(8, 5),
  md5 DECIMAL(8, 5),
  jmd3 DECIMAL(8, 5),
  jmd5 DECIMAL(8, 5),
  PRIMARY KEY(equipe)
)
STORED AS KUDU;

exit;
```
After creating table you can stop impala:
```bash
docker stop impala
```
Now, check the logs of the pyspark-notebook container to find the link with the token to access the pyspark environment:
```bash
docker logs pyspark-notebook
```
Finally, to execute the tests enter the pyspark environment, upload the connection_test notebook and run all cells.