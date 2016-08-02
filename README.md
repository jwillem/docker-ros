# docker-ros
- This repository holds the current version of a dockerized ROS-Environment for use with a Pioneer 2/3DX robot present at the University of Applied Sciences Mannheim. 
- For further explanation of the fundamentals consider to read the documenation:
- [Docker-Ros_Dokumentation.pdf](Docker-Ros_Dokumentation.pdf) (german)

## Container-Overview
![container-overview](/container-overview.png?raw=true)

## Initiale Schritte auf dem Host
- Zur Installation soll ein Linux-Derivat, z.B. ein aktuelles Ubuntu, auf dem Roboter installiert werden. Dort brauchen wir die Pakete `joystick` und `docker`. 
- Um auf die Hardware lesend, wie auch schreibend zugreifen zu können, müssen einige Rechte an den Device-Files vorgenommen werden.
- Folgende Devices brauchen die Rechte 777:

```
/dev/ttyS0
/dev/ttyUSB0
/dev/input/js0
```

- Dies ist mit dem Linux-Tool `chmod` zu bewerkstelligen. (bspw. `chmod 777 /dev/input/js0`)
- Um dies nicht bei jedem Starten des Systems wiederholen zu müssen, bietet sich ein init.d-Skript an. (Weitere Erklärung folgt noch)
- Anschließend soll das docker-ros Repository mit Git geklont werden.

## Starten des ganzen Systems
- `docker-compose up`
- oder `docker-compose up pioneer` um bspw. nur den Pioneer-Container + dessen Abhängigkeit (Master) zu starten

## Neubau der Images nach Änderung an Dockerfile
- `docker-compose stop && docker-compose build`
- manchmal kann auch ein `docker-compose remove` sinnvoll sein.

## Einloggen in Docker-Container
- `docker exec -it [container-name] bash`
- Es können beliebige Änderungen vorgenommen werden.
- Allerdings gehen diese nach einem Beenden des Containers verlohren.
- Deswegen bietet sich diese Möglichkeit nur für Tests am System an, Änderungen müssen ins jeweilige Dockerfile übernommen werden. -> Implizite Doku!

## Ausführen von grafischen Ros-Tools
- Um die grafischen Tools von Ros nutzen zu können, kann zunächst der Heatmap-Container als Basis dienen. Dieser enthält eine Ros-Desktop-Full Installation. Dazu muss man sich per SSH auf diesen Verbinden und das X-Server-Forwarding nutzen.
- Voraussetzung ist allerdings ein Linux-System mit einem X-Server.
- `ssh root@192.168.0.142 -X -p 1337` um sich mit dem heatmap-container zu verbinden.
- Das Passwort lautet `p`.
- Dort kann man bspw. `rviz` starten.
- Note:
  - Das X-Forwarding über das Netzwerk kann zum Teil inperformant sein.
  - Die Verbindung wird zum Host aufgebaut, jedoch den Port 1337 genutzt, welcher auf den Port 22 des Heatmap-Containers weitergeleitet wird. (Siehe docker-compose.yml)
  - Es befindet sich im Moment nur auf dem Heatmap-Container ein Desktop-System und die nötige ssh-config & das ssh-environment.
