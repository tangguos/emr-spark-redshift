###  spark-redshift
#### 加入了s3_endpoint参数,防止china region解析endpoint错误. 使用方式如下
```shell
# 默认s3_endpoint设定为：s3.cn-north-1.amazonaws.com.cn，因此北京region可以不加s3_endpoint参数
# 北京region使用方式
df.write
.format("io.github.spark_redshift_community.spark.redshift")
.option("url", jdbc_url)
.option("dbtable", sink_dbtable)
.option("tempdir", tmp_s3_path)
.option("aws_iam_role",iam_role).mode("append").save()

val rdf = spark.read
.format("io.github.spark_redshift_community.spark.redshift")
.option("url", jdbc_url)
.option("query", query)
.option("tempdir",tmp_s3_path)
.option("aws_iam_role",iam_role)
rdf.load().show()
# 其他regions使用方式，区别是要添加option("s3_endpoint","xxxxxx")参数
df.write
.format("io.github.spark_redshift_community.spark.redshift")
.option("url", jdbc_url)
.option("dbtable", sink_dbtable)
.option("tempdir", tmp_s3_path)
.option("s3_endpoint","xxxxxx")
.option("aws_iam_role",iam_role).mode("append").save()

val rdf = spark.read
.format("io.github.spark_redshift_community.spark.redshift")
.option("url", jdbc_url)
.option("query", query)
.option("tempdir",tmp_s3_path)
.option("s3_endpoint","xxxxxx")
.option("aws_iam_role",iam_role)
rdf.load().show()

```
#### 编译
```shell
# aws社区：https://github.com/spark-redshift-community/spark-redshift 使用sbt构建项目
# 这里是maven构建
mvn clean package -Dscope.type=provided     

# 默认使用spark2构建，也可以调整为spark3
```
