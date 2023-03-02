# Docker Dossier

![Docker Logo](https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png)

<br>

## Inhaltsverzeichnis

1. [Was ist Docker](#Was-ist-Docker)
2. [Dockerimage builden](#Dockerimage-builden)
3. [Run-Check-Stop-Remove-sheet](#Run-Check-Stop-Remove-sheet)
4. [Volumes](#Volumes)


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

### Entsprechende Dateie erstellen z.B index.php
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

## Volumes
