I made it all on local VM and create a ssh tunnel to connect to the server and check results:

ssh -o ExitOnForwardFailure=yes -fN -L 8080:localhost:80 -p 2222 root@127.0.0.1

start a docker swarm:
cd /to/directory/with/docker-compose.yml/
docker swarm init
docker stack deploy -c docker-compose.yml <test_name>

check logs:
service logs <test_name>_nginx