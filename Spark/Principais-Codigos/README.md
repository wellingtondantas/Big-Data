# Comandos utilizados no Spark


## Criar Dataframe

```
data = [("Newton", 1643), ("Eistein", 1879), ("Gauss", 1777)]
df = spark.createDataFrame(data, ["nome", "birth"])

```