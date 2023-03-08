## Video 1 (Praxis Aufagbe MariaDB): 
Command1: docker run -d --name mariadb-test -e MYSQL_ROOT_PASSWORD=geheim mariadb

Command2: docker inspect mariadb-test


## Video 2 (Portainer): 
Im Browser aufrufbar indem man (solang portainer installiert ist) ein gibt und dann local auswählt: localhost:9443 

## Video 3 (phpmyadmin): 
Command1: docker run -d --name mariadb-test -e MYSQL_ROOT_PASSWORD=geheim mariadb

Command2: docker pull phpmyadmin/phpmyadmin

Command3: docker run --name my-own-phpmyadmin -d --link mariadb-test:db -p 8081:80 phpmyadmin/phpmyadmin

Phpmyadmin ist nun im Broswer unter localhost:8081 aufrufbar: user: rool passwort (vorher deklariert): geheim

## Video 4 (testen ob die daten erhalten bleiben): 
Zu databases wechseln, create database, name = test, create, name = test, create

In Portainer Maria DB löschen und phpmyadmin stoppen

## Video 5(testen ob die daten noch da sind): 
Maria DB neu erstellen und phpmyadmin wieder starten und auf localhost:8081 gehen

Tabelle verschwunden (nicht optimal, daten/tabelle verschwudnen)

## Video 6(Verzeichnis): 
Alle Container und Volumes löschen.

Datenbank extern auf einem anderen Volume hosten.

Command1: docker run -d --name mariadb-test -v myvolume:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=geheim mariadb

Phpmyadmin neue test datenbank erstellen.

Command2: docker stop mariadb-test

Command3: docker rm mariadb-test

Command4(update machen): docker pull mariadb

Command5: docker run -d --name mariadb-test -v myvolume:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=geheim mariadb

Phpmyadmin aufrufen und schauen ob test tabelle nohc vorhanden ist

## Video 7 (Eigenes Verzeichnis):
Command1(eigens Linux Verzeichnis erstellen): mkdir varlibmysql

Command2: docker Command1(Erklärung: alles einfach, neu: "/home...:/varli..." vor dem ":" verzeichnis in linux wo das
volume abgelegt ist, nach dem ":" kommt der ort im container)

run -d --name mariadb-test -e MYSQL_ROOT_PASSWORD=geheim -v /home/vmadmin/varlibmysql/:/var/lib/mysql mariadb

Command3(ins linux verzeichnis vom volume wechseln): cd varlibmysql/

Command3(testen ob das volume vorhanden ist): ls


## Video Netzwerk:
Command(testnet = name): docker network create testnet

Netzwerk kann auf Portainer gesehen werden

## Video Wordpress 1-3:
Benötigte Container:

1.DB = Mariadb

2.Phpmyadmin

3.Wordpress

Für weitere Variablen für Commands die jeweiligen Dokus auf Dockerhub anschauen (nicht notwenig nur ein Tipp)

Command1: docker run -d --name mariadb-test --network testnet -e MYSQL_RANDOM_ROOT_PASSWORD=1 -e MYSQL_DATABASE=wp -e MYSQL_USER=wpuser -e MYSQL_PASSWORD=geheim -v myvolme:/var/lib/mysql mariadb

Command2: docker run -d --name pma --network testnet -p 8080:80 -e PMA_HOST=mariadb-test phpmyadmin/phpmyadmin

Testen ob phpmyadmin läuft mit dem eben erstellten user

Command3: docker run -d --wordpress-test --network testnet -h wordpress-test -v wp-html:/var/www/html/wp-content -p 8081:80 -e WORDPRESS_DB_HOST=mariadb-test -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_NAME=wp -e WORDPRESS_DB_PASSWORD=geheim wordpress

Wordpress ist dann aufrufbar unter localhost:8080

Zur Kontrolle in Portainer nachschauen