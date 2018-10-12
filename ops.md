# ops
## docker
Stop and remove all containers
```
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```

Create a network
```
docker network create <network-name>
```

Clean all docker stuffffff 🔥🔥🔥
```
docker system prune
```
