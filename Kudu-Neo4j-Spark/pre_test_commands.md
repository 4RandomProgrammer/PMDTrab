Before testing we need to create a table in Apache Kudu via Impala:
```bash
docker exec -it impala impala-shell
```
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
Test by accessing the notebook on the pyspark container, uploading the connection_test notebook and running it.