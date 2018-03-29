# Docker-Galera-Mysql
Docker整合Galera Mysql

rpm site   
download galera3
http://releases.galeracluster.com/galera-3/centos/7/x86_64/galera-3-25.3.23-2.el7.x86_64.rpm
download mysql-wsrep-5.7.21-25.14
http://releases.galeracluster.com/mysql-wsrep-5.7.21-25.14/centos/7/x86_64/

commad:
first: docker volume create mysql_galera
second: docker volume create mysql_log

master
docker run --env MYSQL_ROOT_PASSWORD=123 -p3339:3306 -v mysql_galera:/var/lib/mysql -v mysql_log:/var/logs/  -p 4567:4567 -p 4444:4444 -p 4568:4568 -d mysqlgalera5.7:5.7 --wsrep-cluster-address=gcomm:// --wsrep-node-address=192.168.0.116

child node1:
docker run --env MYSQL_ROOT_PASSWORD=123 -p3339:3306   -v mysql_galera:/var/lib/mysql -v mysql_log:/var/logs/  -p 4567:4567 -p 4444:4444 -p 4568:4568  -d mysqlgalera5.7:5.7 --wsrep-cluster-address=gcomm://192.168.0.116:4567 --wsrep-node-address=192.168.0.165

child node2:
docker run --env MYSQL_ROOT_PASSWORD=123 -p3339:3306   -v mysql_galera:/var/lib/mysql -v mysql_log:/var/logs/  -p 4567:4567 -p 4444:4444 -p 4568:4568  -d mysqlgalera5.7:5.7 --wsrep-cluster-address=gcomm://192.168.0.116:4567 --wsrep-node-address=192.168.0.115
