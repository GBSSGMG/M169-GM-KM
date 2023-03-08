# Docker Dossier

![Docker Logo](https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png)

<br>

## Inhaltsverzeichnis

1. [Begriffe](#Sie kennen den Begriff von "Container" und können Begriffe wie Docker Image, Dockerfile, Docker-Container und Docker-Registry erklären.)
2. [Dockerimage builden](#Dockerimage-builden)
3. [Run-Check-Stop-Remove-sheet](#Run-Check-Stop-Remove-sheet)
4. [Volumes](#Volumes)
5. [Netzwerke](#Netzwerke)

<br>

## Sie kennen den Begriff von "Container" und können Begriffe wie Docker Image, Dockerfile, Docker-Container und Docker-Registry erklären.

Container: kein Guest-OS, Kernel vom Host-OS, Docker Engine

VM: Guest-OS, eigener virtueller Kernel, Hypervisor

Docker Image: Enthält alle benötigten Komponenten, inkl. Bibliotheken, Hilfsprogramme und sonstige Dateien für den Betrieb. Bei VMs wären dies die ISO Files, Docker Images sind jedoch häufig nur einige Kilo bis Megabyte gross. 

Dockerfile: Instruktionen, um ein Docker-Image zu erzeugen

Docker-Container: Laufende Docker Instanz basiert auf einem dazugehörigen Image

Docker-Registry: Bibliothek für Docker-Images, es gibt Public Registrys wie von Docker selbst (Docker Hub) oder Amazon, kann auch selbst gehostet werden (gibt dafür auf Dockerhub ein Image)

![Container vs VM](https://www.criticalcase.com/wp-content/uploads/2021/02/SCHEMA-CONTAINER-VS-VM.png)

<br>

## Sie können die Begriffe Virtualisierung und Cloud voneinander trennen.

Virtualisierung ist eine Technologie, die es einem ermöglicht Physische Hardware Virtuell auf mehrere Systeme zu verteilen. In der Cloud werden sehr viele Physische Ressourcen auf viele Systeme verteile, wobei der User selbst Skalieren kann.
