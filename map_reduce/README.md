# Map reduce homework
К сожалению, разобрался только с простой частью задания :c

# Запуск локально:
```shell
   cat sample.txt | python map.py | sort -k1,1 | python reduce.py > output.txt
```
# Запуск в докере hadoop:

Имя докера: quirky_leakey
```shell
   sudo docker ps -a
```

Копирование фаилов:
```shell
   sudo docker cp ./map.py quirky_leakey:map.py
   sudo docker cp ./reduce.py quirky_leakey:reduce.py
   sudo docker cp ./sample.txt quirky_leakey:sample.txt
```
запуск докера:

```shell
   sudo docker run -it sequenceiq/hadoop-docker:2.7.1 /etc/bootstrap.sh -bash
```

В докере:
```shell
   cd $HADOOP_PREFIX
   bin/hdfs dfs -mkdir sample
   bin/hdfs dfs -put /sample.csv ./sample
```

```shell
    bin/hadoop jar share/hadoop/tools/lib/hadoop-streaming-2.7.1.jar \
    -input sample/ \
    -output ./output \
    -mapper map.py \
    -reducer reduce.py \
    -file /map.py \
    -file /reduce.py
```
