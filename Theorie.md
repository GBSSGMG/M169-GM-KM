# Docker Dossier

![Docker Logo](https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png)

<br>

## Inhaltsverzeichnis

1. [Begriffe](#Sie-kennen-den-Begriff-von-"Container"-und-können-Begriffe-wie-Docker-Image,-Dockerfile,-Docker-Container-und-Docker-Registry-erklären.)
2. [Virtualisierung | Cloud](#Sie-können-die-Begriffe-Virtualisierung-und-Cloud-voneinander-trennen.)
3. [Container ausführen und benutzen](#Sie-können-einen-Docker-Container-ausführen-und-interaktiv-verwenden.)
4. [Portweiterleitung](#Sie-erkennen,-warum-Portweiterleitungen-wichtig-sind,-und-können-eine-solche-in-Betrieb-nehmen.)
5. [Volumes](#Sie-können-mit-Docker-Volumes-umgehen.)
6. [Volumes Praxis](#Sie-können-Volumes-benennen-und-in-einem-definierten-Verzeichnis-speichern.)
7. [Netzwerke](#Sie-verstehen-den-Standardaufbau-eines-Netzwerks-mit-Docker.)
8. [Netzwerke Praxis](#Sie-können-eigene-Netzwerkdefinitionen-mit-Docker-umsetzen.)
9. [Befehle](#Sie-kennen-die-wichtigsten-Befehle-um-Docker-zu-administrieren,-dazu-zählen-Platzbedarf-von-Images-und-Containern-ermitteln,-Container-und-Images-löschen,-Volumes-verwalten,-Gesamtüberblick-erhalten-und-Ungenutzten-Speicher-freigeben.)

<br>

## Sie-kennen-den-Begriff-von-"Container"-und-können-Begriffe-wie-Docker-Image,-Dockerfile,-Docker-Container-und-Docker-Registry-erklären.

Container: kein Guest-OS, Kernel vom Host-OS, Docker Engine

VM: Guest-OS, eigener virtueller Kernel, Hypervisor

Docker Image: Enthält alle benötigten Komponenten, inkl. Bibliotheken, Hilfsprogramme und sonstige Dateien für den Betrieb. Bei VMs wären dies die ISO Files, Docker Images sind jedoch häufig nur einige Kilo bis Megabyte gross. 

Dockerfile: Instruktionen, um ein Docker-Image zu erzeugen

Docker-Container: Laufende Docker Instanz basiert auf einem dazugehörigen Image

Docker-Registry: Bibliothek für Docker-Images, es gibt Public Registrys wie von Docker selbst (Docker Hub) oder Amazon, kann auch selbst gehostet werden (gibt dafür auf Dockerhub ein Image)

![Container vs VM](https://www.criticalcase.com/wp-content/uploads/2021/02/SCHEMA-CONTAINER-VS-VM.png)

<br>

## Sie-können-die-Begriffe-Virtualisierung-und-Cloud-voneinander-trennen.

Virtualisierung ist eine Technologie, die es einem ermöglicht Physische Hardware Virtuell auf mehrere Systeme zu verteilen. In der Cloud werden sehr viele Physische Ressourcen auf viele Systeme verteile, wobei der User selbst Skalieren kann.

<br>

## Sie-können-einen-Docker-Container-ausführen-und-interaktiv-verwenden.

[Schau die Praxisbezogene Doku an](https://github.com/GBSSGMG/M169-GM-KM/blob/main/Praxis.md)

<br>

## Sie-erkennen,-warum-Portweiterleitungen-wichtig-sind,-und-können-eine-solche-in-Betrieb-nehmen.

Falls ein Port beim Host-OS besetzt ist kann dieser ganz einfach auf einen beliebigen weitergeleitet werden.

<br>

## Sie-können-mit-Docker-Volumes-umgehen.

Volumes sind die Speicher der Container, welche weiter bestehen können wenn der dazu gehörige Container gelöscht wird oder kaputt geht. 

<br>

## Sie-können-Volumes-benennen-und-in-einem-definierten-Verzeichnis-speichern.

[Schau die Praxisbezogene Doku an](https://github.com/GBSSGMG/M169-GM-KM/blob/main/Praxis.md)

<br>

## Sie-verstehen-den-Standardaufbau-eines-Netzwerks-mit-Docker.

![Docker Netzwerk](https://gbssg.gitlab.io/m169/img/kap1/7-1.PNG)

<br>

## Sie-können-eigene-Netzwerkdefinitionen-mit-Docker-umsetzen.

[Schau die Praxisbezogene Doku an](https://github.com/GBSSGMG/M169-GM-KM/blob/main/Praxis.md)

<br>

## Sie-kennen-die-wichtigsten-Befehle-um-Docker-zu-administrieren,-dazu-zählen-Platzbedarf-von-Images-und-Containern-ermitteln,-Container-und-Images-löschen,-Volumes-verwalten,-Gesamtüberblick-erhalten-und-Ungenutzten-Speicher-freigeben.

[Schau die Praxisbezogene Doku an](https://github.com/GBSSGMG/M169-GM-KM/blob/main/Praxis.md)


## Joel Zusammenfassung

Erklärung Netzwerk
⦁	Bridge-Netzwerk: Standardmäßig werden Docker-Container in einem Bridge-Netzwerk erstellt, das es den Containern ermöglicht, miteinander zu kommunizieren, ohne dass sie öffentlich zugänglich sind. Der Host-System wird auch in dieses Netzwerk einbezogen. Jeder Container erhält eine IP-Adresse im Bridge-Netzwerk und kann auf andere Container im Netzwerk zugreifen, indem er die IP-Adresse oder den Container-Namen verwendet.

⦁	Host-Netzwerk: Docker bietet auch die Option, Container direkt an das Host-Netzwerk anzuschließen, wodurch sie dieselbe Netzwerkumgebung wie das Host-System haben. Container, die dem Host-Netzwerk angeschlossen sind, haben Zugriff auf alle Netzwerkressourcen, die auf dem Host verfügbar sind.

⦁	Overlay-Netzwerk: Overlay-Netzwerke ermöglichen es Containern, über mehrere Hosts hinweg miteinander zu kommunizieren. Dies ist nützlich für Anwendungen, die auf mehrere Hosts verteilt sind und die Interaktion zwischen Containern erfordern.

⦁	Custom-Netzwerk: Docker ermöglicht es auch, benutzerdefinierte Netzwerke zu erstellen, die spezifisch für eine Anwendung oder Gruppe von Anwendungen sind. Diese Netzwerke können so konfiguriert werden, dass sie nur den erforderlichen Datenverkehr zulassen und die Sicherheit erhöhen.


Wichtigste Befehle

Platzbedarf von Images und Containern ermitteln:
"docker images -a" zeigt eine Liste aller Images an, die auf dem Host-System gespeichert sind, zusammen mit ihrer Größe.
"docker ps -a" zeigt eine Liste aller Container an, die auf dem Host-System ausgeführt werden, zusammen mit ihrem Status und ihrer Größe.

Container und Images löschen:
"docker rm" löscht einen oder mehrere Container von dem Host-System. Zum Beispiel: "docker rm container_name".
"docker rmi" löscht ein oder mehrere Images von dem Host-System. Zum Beispiel: "docker rmi image_name".

Volumes verwalten:
"docker volume ls" zeigt eine Liste aller Volumes an, die auf dem Host-System erstellt wurden.
"docker volume create" erstellt ein neues Volume.
"docker volume rm" löscht ein oder mehrere Volumes. Zum Beispiel: "docker volume rm volume_name".

Gesamtüberblick erhalten:
"docker stats" zeigt Echtzeitinformationen zu CPU, Speicher und Netzwerkverbrauch von allen laufenden Containern an.
"docker system df" zeigt Informationen zu allen Images, Containern und Volumes an, die auf dem Host-System gespeichert sind.

Ungenutzten Speicher freigeben:
"docker system prune" entfernt alle nicht verwendeten Images, Container und Volumes von dem Host-System.
"docker image prune" entfernt alle nicht verwendeten Images von dem Host-System.
"docker container prune" entfernt alle nicht verwendeten Container von dem Host-System.
"docker volume prune" entfernt alle nicht verwendeten Volumes von dem Host-System.
