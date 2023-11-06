# atdb-docker

En este repositorio se encuentran los pasos para lanzar en la máquina virtual local de Ubuntu el entorno para implementar la primera práctica de la asignatura ATBD.

# Instalación de Docker

En una terminal, ejecutar los siguientes pasos:

```
sudo apt install curl
curl -fsSL https://get.docker.com -o install-docker.sh
sudo sh install-docker.sh
sudo apt-get install -y uidmap
dockerd-rootless-setuptool.sh install
```

# Configurar el entorno

Descargar este repositorio y acceder a él:

```
git clone https://github.com/memaldi/atbd-docker
cd atbd-docker/
```

Desde este directorio, descargar y descomprimir Hadoop:
```
wget https://dlcdn.apache.org/hadoop/common/hadoop-3.3.6/hadoop-3.3.6.tar.gz
unzip hadoop-3.3.6.tar.gz
```

# Iniciar el entorno

Desde dentro del directorio del repositorio, ejecutamos

```
docker compose up
```

# Interacción con las herramientas

Para interactuar con las diferentes herramientas, tenemos que abrir una terminal dentro del repositorio.

## HDFS

Para interactuar con HDFS, podemos lanzar el siguiente comando. Por ejemplo, para ver el contenido de la carpeta /ecommerce:

```
docker compose exec -ti namenode hdfs dfs -ls /ecommerce
```

## Flume

En este entorno se incluye una instancia de Flume, en el caso de que queráis utilizarla. Para configurarla, tenéis que editar el fichero `flume/flume.conf` y reiniciar Flume:

```
docker compose restart flume
```

## Kafka

Existen dos instancias de kafka en el entorno. Se puede acceder a ellas en las URIs `kafka:9092` y `kafka-ecommerce:9092`. La primera, la podéis utilizar para realizar la práctica, si lo necesitaseis. La segunda, es en la que se depositan los mensajes de ecommerce que tenéis que procesar.

No es necesario ejecutar ningún comando para crear los topics, se crean automáticamente cuando alguien envía un mensaje.

## Elasticsearch

La instancia de elasticsearch se puede acceder desde otras herramientas (p. ej., NiFi), desde la URI http://elasticsearch:9200. El usuario es elastic y la contraseña adminatbd2324. En este caso, sí hace falta crear el índice antes de escribir datos. Podemos hacerlo así:

```
docker compose exec -ti elasticsearch curl -k -u "elastic:adminatbd2324" -X PUT "http://localhost:9200/ecommerce-data?pretty"
```

Para consultar los documentos que tenemos en el índice, podemos hacerlo así:

```
docker compose exec -ti elasticsearch curl -k -u "elastic:adminatbd2324" -X GET "http://localhost:9200/ecommerce-data/_search?q=*&pretty"
```

## NiFi

NiFi está accesible en la url https://localhost:8443. El usuario es admin y la contraseña adminatbd2324. En el repositorio se puede encontrar el fichero `NiFi_configuration_example.json`, en el que podéis ver cómo se accede a servicios como Kafka, HDFS o Elasticsearch desde NiFi.


