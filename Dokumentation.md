# Docker Dossier

![Docker Logo](https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png)

<br>

## Inhaltsverzeichnis

1. [Was ist Docker](#Was-ist-Docker)
2. [Dockerimage builden](#Dockerimage-builden)
3. [Run-Stop-Remove-sheet](#Run-Stop-Remove-sheet)


<br>

## Was-ist-Docker
Docker ist eine Plattform zur Containerisierung von Anwendungen. Container sind isolierte Umgebungen, die eine Anwendung mit all ihren Abhängigkeiten einschliessen, damit sie auf jedem System ausgeführt werden kann, unabhängig von der zugrunde liegenden Infrastruktur. Docker macht es einfach, Anwendungen in Containern zu erstellen, zu verteilen und auszuführen, wodurch die Komplexität der Bereitstellung von Anwendungen in unterschiedlichen Umgebungen reduziert wird.

<br>

## Dockerimage-builden

### Build Ordner erstellen und eingehen
```txt
mkdir bsp-apache-php
cd bsp-apache-php
```txt

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

## Run-Stop-Remove-sheet

