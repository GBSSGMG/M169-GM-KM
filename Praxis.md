# Docker Dossier

![Docker Logo](https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png)

<br>

## Inhaltsverzeichnis

1. [Was ist Docker](#Was-ist-Docker)
2. [Dockerimage builden](#Dockerimage-builden)
3. [Run-Check-Stop-Remove-sheet](#Run-Check-Stop-Remove-sheet)
4. [Volumes](#Volumes)
5. [Netzwerke](#Netzwerke)

<br>

## Was-ist-Docker
Docker ist eine Plattform zur Containerisierung von Anwendungen. Container sind isolierte Umgebungen, die eine Anwendung mit all ihren Abhängigkeiten einschliessen, damit sie auf jedem System ausgeführt werden kann, unabhängig von der zugrunde liegenden Infrastruktur. Docker macht es einfach, Anwendungen in Containern zu erstellen, zu verteilen und auszuführen, wodurch die Komplexität der Bereitstellung von Anwendungen in unterschiedlichen Umgebungen reduziert wird.

<br>

## Dockerimage-builden

### Build Ordner erstellen und eingehen
```txt
mkdir bsp-apache-php
```
```txt
cd bsp-apache-php
```

### Dockerfile erstellen und schreiben
```dockerfile
# Datei: bsp-apache-php/Dockerfile
FROM php:8-apache
COPY index.php /var/www/html
```

### Entsprechende Datei erstellen z.B index.php
```html
<!DOCTYPE html >
<!-- Datei index.php -->
<html >
<head >
<title >Beispiel</title >
<meta charset ="utf-8" />
</head >
<body >
<h1>Beispiel apache/php</h1>
Serverzeit : <?php echo date("j. F Y, H:i:s, e "); ?>
</body >
</html >
```

### Image builden
```txt
docker build -t bsp-apache-php .
```

<br>

## Run-Check-Stop-Remove-sheet

### Container Run
```txt
docker run -d --name bsp-apache-php-container -p 8080:80 bsp-apache-php
```
#### Optionen & Erklärung
- -d: gibt an, dass der Container im Hintergrund läuft. (daemon)
- --name: gibt en Namen des Containers an, dieser kann anders lauten als das Image.
- -p: Verknüpft den Port 80 innerhalb des Containers mit dem Port 8080 des Hosts.
- bsp-apache-php: der Name des Image aus dem der Container gestartet wird.

### Container Checken
```txt
docker ps
```

### Container Managing
Sie können den Container mit stop, start oder restart anhalten und neu starten:

```txt
docker start bsp-apache-php-container
```
```txt
docker stop bsp-apache-php-container
```
```txt
docker restart bsp-apache-php-container
```
Der Container kann gelöscht werden mit

```txt
docker rm bsp-apache-php-container
```

### Images Managing
Lokal vorhandene Images anzeigen lassen
```txt
docker images
```

Image löschen
```txt
docker rmi bsp-apache-php
```
<br>

## Volumes
Hier geht es darum, wo ein Container seine Daten speichert. Daten die in einem laufenden Container gespeichert sind, bleiben erhalten, wenn der Container gestoppt und wieder gestartet wird, nicht jedoch wenn ein Container gelöscht und wieder neu erzeugt wird.

### Unbenannte Volumes
Schauen wir dazu nochmals das Beispiel des mariadb-Servers an. Einen Image können Sie mit dem folgenden Kommando herunterladen und einen Container daraus starten
```txt
docker run -d --name mariadb-test -e MYSQL_ROOT_PASSWORD=geheim mariadb
```
Um herauszufinden wo nun die Daten aus /var/lib/mysql gelandet sind können Sie das Kommando
```txt
docker inspect -f '{{.Mounts}}' mariadb-test
```
ergibt:
```txt
vmadmin@ubuntu:~/bsp-apache-php$ docker inspect -f '{{.Mounts}}' mariadb-test
[{volume 752507751a42f0c781b96adacb4a3d73bdbbf2184ead3bd4874b4b5f065ee4eb /var/lib/docker/volumes/752507751a42f0c781b96adacb4a3d73bdbbf2184ead3bd4874b4b5f065ee4eb/_data /var/lib/mysql local  true }]
vmadmin@ubuntu:~/bsp-apache-php$
```
Sollte z.B ein Volume gelöscht werden, müsste der vollständige Verzeichnisname angegeben werden:
```txt
docker volume rm 7525077...
```

### Benannte Volumes

Eine bessere Variante ist es deshalb Volumes beim Erstellen eines Containers zu benennen:

```txt
docker run -d --name mariadb-test2 -v myvolume:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=geheim mariadb
```
```txt
vmadmin@ubuntu:~/bsp-apache-php$ docker run -d --name mariadb-test2 -v myvolume:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=geheim mariadb
2ccb55f675a5867efeefaa8bfd02e896cf0e0e1b66fe098465d6d7cc3e6a9bc6
vmadmin@ubuntu:~/bsp-apache-php$ docker inspect -f '{{.Mounts}}' mariadb-test2
[{volume myvolume /var/lib/docker/volumes/myvolume/_data /var/lib/mysql local z true }]
```
Wie Sie sehen, wird nun der gewählte Name für das Unterverzeichnis verwendet. Die Syntax lautet somit:
```txt
-v volumename:containerverzeichnis
```

### Volumes in eigenen Verzeichnissen
Anstelle eines Namens für das Hostvolume kann auch ein Verzeichnis angegeben werden:
```txt
-v hostverzeichnis:containerverzeichnis
```
Damit wird das Volume ganz aus der Dockerumgebung herausgelöst und kann an einer beliebigen Stelle platziert werden:
```txt
mkdir /home/vmadmin/databases
docker run -d --name mariadb-test3 -v /home/vmadmin/databases:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=geheim mariadb
```

<br>

## Netzwerke

Hier geht es darum wie mehrere Dockercontainer untereinander kommunizieren können. Beispielsweise muss ein Web-Container mit einem Datenbank-Container kommunizieren können und an seine Daten zu kommen.

Der Befehl
```txt
docker network ls
```
zeigt die vorhandenen Netzwerke an.
```txt
vmadmin@ubuntu:~$ docker network ls
NETWORK ID     NAME                                 DRIVER    SCOPE
65593a9ebb3b   bridge                               bridge    local
364521a9eaa2   host                                 host      local
c69c18f0a974   none                                 null      local
```

### Standardnetzwerk
Das Netzwerk mit dem Namen bridge ist das Standardnetzwerk und wird verwendet wenn nichts anderes angegeben wird. Die Netzwerkarchitektur lässt sich wie folgt darstellen:

![Netzwerkschema](https://gbssg.gitlab.io/m169/img/kap1/7-1.PNG)

```txt
docker run  -it --name ubuntu_1 ubuntu:latest
```
Hier erkennt man die Definition des Klasse B Netzwerkes 172.17.0.0/16 und die IP-Adresse des Containers

```txt
docker network inspect bridge
```

### Eigene Netzwerke
Alle Container landen standardmässig im selben Netzwerk, dem bridge-Netzwerk. Dies ist aus sicherheitstechnischen Gründen nciht ideal, wenn unterschiedliche Anwendungen voneinander isoliert sein sollen. Es lassen sich deshalb eigene Netzwerke definieren und diese den Containern zuordnen.
```txt
docker network create \
--driver=bridge \
--subnet=10.10.10.0/24 \
--gateway=10.10.10.1 \
my_net
```

Ein Container kann nun beim Start diesem Netzwerk zugeordnet werden:
```txt
docker run -it --name ubuntu_2 --network=my_net ubuntu:latest
```
und
```txt
docker network inspect my_net
```

Die IP-Adresse für den Container wird dabei von docker via DHCP aus dem definierten Netzwerk vergeben. Alternativ kann eine fixe IP-Adresse beim Start des Containers angegeben werden.

```txt
docker run -it --name ubuntu_2 --ip="10.10.10.10" --network=my_net ubuntu:latest
```

Netzwerk entfernen
```txt
docker network disconnect bridge ubuntu_1
```
```txt
docker network connect my_net ubuntu_1
docker start -i ubuntu_1
```

Ping Software
```txt
apt update
apt install iputils-ping
```

Nachdem alle Container, die zu einem Netzwerk hinzugefügt wurden, gestoppt oder getrennt wurden, können Sie das Netzwerk mit folgendem Befehl löschen:
```txt
docker network rm my_net
```