# **Spark Style Guide**

Spark is an amazingly powerful big data engine that's written in Scala.

This document draws on the Spark source code, the [Spark examples](http://spark.apache.org/examples.html), and popular open source Spark libraries  to outline coding conventions and best practices.


## <a name='TOC'>Table of Contents</a>

1. [Scala Style Guides](#scala-style-guides)
1. [Spark RDD](#rdd)
1. [Spark SQL](#spark-sql)
1. [Variables](#variables)
1. [Methods](#methods)
1. [Chained Method Calls](#chained-method-calls)
1. [Pyspark Dataframes](#pyspark-dataframes)
1. [Writing Functions](#writing-functions)
    * [Custom SQL Functions](#custom-sql-functions)
    * [User Defined Functions](#user-defined-functions)
    * [Pandas User Defined Functions](#pandas-udf-functions)
1. [Open Source](#open-source)

## <a name='scala-style-guides'>Scala Style Guides</a>

* [Official Scala style guide](http://docs.scala-lang.org/style/) 
* [Databricks Scala style guide](https://github.com/databricks/scala-style-guide)  

## <a name='rdd'>RDD</a>
[RDD Programming Guide](http://spark.apache.org/docs/latest/rdd-programming-guide.html)
The backbone of a Dataframe is an RDD [Row](https://spark.apache.org/docs/2.3.4/api/python/pyspark.sql.html?highlight=row#pyspark.sql.Row), a Spark type that behaves very similar to a Python dictionary. 
[Programming Guide to RDD](https://towardsdatascience.com/a-modern-guide-to-spark-rdds-725cd7c14059)

* Dataframe to RDD
```python
   spark \
     .read \
     .csv('CSV data path') \
     .rdd \
     .map(lambda r: r.asDict())
```
* RDD to Dataframe
```python
   from pyspark.sql import Row

   dict_rdd = sc \
     .parallelize([
       {'col1': 'val_A', 'col2': 'val_B'},
       {'col1': 'val_C', 'col2': 'val_D'}])

   dict_rdd \
     .map(lambda d: Row(
       col1 = d['col1'], 
       col2 = d['col2'])) \ 
     .toDF()

   dict_rdd \
     .map(lambda d: Row(**d)) \ 
     .toDF()
```
Or
```
   sc \
     .parallelize([
       ('val_A', 'val_B'), 
       ('val_C', 'val_D')]) \
     .toDF(['col1','col2'])
```
### RDD Best Practices:
* #### Don’t call collect() on large RDDs
By calling collect() on any RDD, you drag data back into your applications from the nodes. Each RDD element will be copy onto the single driver program, which will run out of memory and crash.
* #### Reduce Your RDD Before Joining
One of the most basic rules that you can apply when you’re revising the chain of operations that you have written down is to make sure that you filter or reduce your data before joining it. This way, you avoid sending too much data over the network that you’ll throw away after the join.
* #### Avoid groupByKey() on large RDDs
When you use groupByKey(), all key-value pairs are shuffled around in the cluster. A lot of unnecessary data is being transferred over the network. On big data sets, you’re better off making use of other functions, such as reduceByKey(), combineByKey() or foldByKey().
* #### Broadcast Variables
By broadcasting variables, you can reduce the cost of launching a job over the cluster.
* #### Avoid flatmap(), join() and groupBy() Pattern
When you have two datasets that are grouped by key and you want to join them, but still keep them grouped, use cogroup() instead of the above pattern.
* #### Use coalesce to repartition in decrease number of partition
Use coalesce function if you decrease the number of partition of the RDD instead of repartition. Coalesce is useful because it avoids a full shuffle, It uses existing partitions to minimize the amount of data that is shuffled.
* ####  Joining a large and a small RDD
If the small RDD is small enough to fit into the memory of each worker we can turn it into a broadcast variable and turn the entire operation into a so called map side join for the larger RDD and this way, the larger RDD does not need to be shuffled at all. This can easily happen if the smaller RDD is a dimension table.
* #### Joining a large and a medium size RDD
Filter before joining to reduce memory overload if the medium size rdd does not fit in memory.


## <a name='spark-sql'>Spark SQL</a>

Use multiline strings to write properly indented SQL code:

```scala
coolDF = spark.sql("""
select
  `first_name`,
  `last_name`,
  `hair_color`
from people
""")
```
## <a name='variables'>Variables</a>

Variables should use same naming conventions as python PEP-8. Variables that point to DataFrames, Datasets, and RDDs should be suffixed to make your code readable:

* Variables pointing to DataFrames should be suffixed with `df` (following conventions in the [Spark Programming Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html))

```python
people_df.createOrReplaceTempView("people")
```

* Variables pointing to Datasets should be suffixed with `ds`

* Variables pointing to RDDs should be suffixed with `rdd`
e.g.
```python
people_rdd = spark.sparkContext.textFile("examples/src/main/resources/people.txt")
```

## <a name='methods'>Methods</a>
Same naming convention as Python PEP-8 for custom methods:
```python
def with_stuff1(arg1, arg2, df):
    return df.withColumn("stuff1", lit(f"{arg1} {arg2}"))
```

## <a name='chained-method-calls'>Chained Method Calls</a>

Spark methods are often deeply chained and should be broken up on multiple lines.

```python
actual_df = (source_df
     .transform(with_greeting)
     .transform(with_funny("haha")))
```

Here's an example of a well formatted extract:

```scala
extractDF = spark.read.parquet("someS3Path")
  .select(
    "name",
    "Date of Birth"
  )
  .transform(someCustomTransformation())
  .withColumnRenamed("Date of Birth", "date_of_birth")
  .filter(
    col("date_of_birth") > "1999-01-02"
  )
```

## <a name='pyspark-dataframes'>Pyspark DataFrames</a>

* Follow the [Official Documentation](http://spark.apache.org/docs/latest/api/python/pyspark.sql.html#pyspark.sql.DataFrame) for the exhaustive list of methods and examples for Pyspark DataFrames.
* Avoid doing `toPandas()` while working with PySpark Dataframes.

## <a name='writing-functions'>Writing functions</a>

### <a name='custom-sql-functions'>Custom SQL Functions</a>

Here's an example of a custom SQL function that returns `child` when the age is less than 13, `teenager` when the age is between 13 and 18, and `adult` when the age is above 18.

```scala
import org.apache.spark.sql.Column

def lifeStage(col):
{
  when(col < 13, "child")
    .when(col >= 13 && col <= 18, "teenager")
    .when(col > 18, "adult")
}
```

The `lifeStage()` function will return `null` when `col` is `null`.  All built-in Spark functions gracefully handle the `null` case, so we don't need to write explicit `null` logic in the `lifeStage()` function.

Custom SQL functions can also be optimized by the Spark compiler, so this is a good way to write code.  Read [this blog post](https://www.mungingdata.com/apache-spark/spark-sql-functions) for a full discussion on custom SQL functions.

### <a name='user-defined-functions'>User Defined Functions</a>

You can write User Defined Functions (UDFs) when you need to write code that leverages advanced Scala/Pyspark programming features or Java libraries.

Here's an example of a UDF that forecasts future value for DF column values:

```python
from pyspark.sql.functions import  udf
def getFutureForecast(model, numFuturePredictions=1):
   '''
   returns future forecast using model
   '''
   forecast, confidence = model.forecast(steps=numFuturePredictions)
   return forecast.tolist(), confidence.tolist()

forecast, confidence = getFutureForecast(trainedModel)
udfForecast = udf(lambda x: forecast[x],returnType=FloatType())
testDF = testDF.withColumn('forecast', udfForecast("id"))
```

UDFs [are a black box](https://jaceklaskowski.gitbooks.io/mastering-spark-sql/spark-sql-udfs-blackbox.html) from the Spark compiler's perspective and should be avoided whenever possible.

Most logic can be coded as a custom SQL function. Only revert to UDFs when the native Spark API isn't sufficient.


### <a name='pandas-udf-functions'>Pandas User Defined Functions</a>
A pandas user-defined function (UDF)—also known as vectorized UDF—is a user-defined function that uses Apache Arrow to transfer data and pandas to work with the data. You define a pandas UDF using the keyword pandas_udf as a decorator or to wrap the function; no additional configuration is required.

Refer [here](https://docs.databricks.com/spark/latest/spark-sql/udf-python-pandas.html) for more detail.

```python
import pandas as pd

from pyspark.sql.functions import col, pandas_udf
from pyspark.sql.types import LongType

# Declare the function and create the UDF
def multiply_func(a, b):
    return a * b

multiply = pandas_udf(multiply_func, returnType=LongType())
# The function for a pandas_udf should be able to execute with local pandas data
x = pd.Series([1, 2, 3])
print(multiply_func(x, x))
# 0    1
# 1    4
# 2    9
# dtype: int64
```


## <a name='open-source'>Open Source</a>

You should write generic open source code whenever possible.  Open source code is easily reusable (especially when it's uploaded to Maven) and forces you to design code without business logic.

The [`org.apache.spark.sql.functions`](https://spark.apache.org/docs/2.1.0/api/java/org/apache/spark/sql/functions.html) class provides some great examples of open source functions.

The [`Dataset`](https://spark.apache.org/docs/2.1.0/api/java/org/apache/spark/sql/Dataset.html) and [`Column`](https://spark.apache.org/docs/2.1.0/api/java/org/apache/spark/sql/Column.html) classes provide great examples of code that facilitates DataFrame transformations.
