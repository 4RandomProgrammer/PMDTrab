# Pre test Commands
Firstly boot up the docker environment by executing this command in this folder:
```bash
docker compose up -d
```
Before testing the environment we need to create a table in Apache Kudu via Impala:
```bash
docker exec -it impala impala-shell
```
In the Impala shell, use the following commands to insert a new table called testA
```SQL
connect;   -- (run again if not successful)

CREATE TABLE testA (
  literal STRING,
  nota DECIMAL(8, 5),
  dados DECIMAL(8, 5),
  idade INT,
  lorem INT,
  ipsum STRING,
  PRIMARY KEY(literal, nota, dados)
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