1- sudo apt install curl
2- curl -fsSL https://get.docker.com -o install-docker.sh
3- sudo sh install-docker.sh
4- sudo apt-get install -y uidmap
5- dockerd-rootless-setuptool.sh install
6- docker compose up
- Explicar como interactuar con HDFS --> docker compose exec -ti namenode hdfs dfs -ls /ecommerce
7- Explicar donde está el conf de flume
8- Explicar cómo ver el log de flume
9 - Crear un topic en kafka
8 - Crear index en elasticsearch --> docker compose exec -ti elasticsearch curl -k -u "elastic:adminatbd2324" -X PUT "https://localhost:9200/ecommerce-data?pretty"
