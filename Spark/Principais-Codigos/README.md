# Comandos utilizados no Spark


## Criar Dataframe

```
data = [("Newton", 1643), ("Eistein", 1879), ("Gauss", 1777)]
df = spark.createDataFrame(data, ["nome", "birth"])
```

## Mostra o conteúdo de um Dataframe

```
df.show()
```

## Carrega arquivo csv no Spark

```
df = spark.read.format("com.databricks.spark.csv").option("header", "true").option("delimiter", "\t").option("inferSchema", "true").load("file.csv")
```

## Verifica o Schema

```
df.printSchema()
```

## Conta a quantidade de linhas do DataFrame

```
df.count()
```

## Seleciona colunas do DataFrame (select)

```
df.select("Nome da Coluna").show()
```

## Seleciona os valores distintos da coluna do DataFrame (distinct)

```
df.select("Nome da Coluna").distinct().show()
```

## Filtra linhas do DataFrame (filter)

```
df.filter(df["Nome da Coluna"] == "Caracteristica").count()
```

## Agrupamento em DataFrame (groupBy)

```
df.groupBy("Nome do campo").count().show()
```

## Agrupamento em DataFrame com ordenação(orderBy)

```
df.groupBy("Nome do campo").count().orderBy("count").show()
```

```
df.groupBy("Nome do campo").count().orderBy("count", ascending=False).show()
```

## Troca caracteres em Spark

```
to_value = lambda v: float(v.replace(",","."))

from pyspark.sql import function as F

udf_to_value = F.udf(to_value, pyspark.sql.types.FloatType())

df2 = df.withColumn("value", udf_to_value(df["Nome do campo"]))
```

## Informações do DataFrame (describe)

```
df2.describe("value").show()
```

## Informações mais otimizadas

```
from pyspark.sql import function as F

df2.groupBy("Nome do campo").agg(F.sum(df2.value), F.max(df2.value), F.count(df2.value)).show()
```


```
df2.groupBy("Nome do campo").agg(F.sum(df2.value), F.max(df2.value), F.count(df2.value), F.avg("value")).orderBy("sum(value)", descending=False).show()
```



























































