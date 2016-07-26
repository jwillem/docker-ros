# docker-ros

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
- `ssh root@192.168.0.142 -X -p 1337` um sich mit dem heatmap-container zu verbinden.
- Dort kann man bspw. `rviz` starten. -- Das X-Forwarding über das Netzwerk kann zum Teil inperformant sein.
- Note: Es befindet sich im Moment nur auf dem Heatmap-Container ein Desktop-System und die nötige ssh-config & das ssh-environment.
