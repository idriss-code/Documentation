# DOCKER

```bash
docker --help | less
# liste des container runing
docker -ps
# liste de tous les contenaire
docker -ps -a

docker inspect myContainer | less

docker run -dit my_image

docker run -dit --restart always --name my_container_name my_image

docker exec -ti my_container_name bash

docker top my_container_name

docker run --rm my_image

docker logs -tf my_container_name

docker stop my_container_name

docker kill my_container_name

docker pull my_image

docker image ls
docker images

docker image prune
docker rmi my_image:mytag

docker system prune -a
docker system df

docker build -t my_image
docker history my_image

docker run --name mon_nginx -d -p 8080:80 nginx
#ro = read only
docker run --name autre_nginx -d -p 8080:80 -v ${PWD}/pagesweb:/usr/share/nginx/html:ro nginx

```
