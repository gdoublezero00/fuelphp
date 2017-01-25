# Cloning Source
git clone <URL> application
# docker up
docker-compose up


# Tips
## docker up
docker-compose up

## docker up with build
docker-compose up --build

## bash
docker exec -it <Container ID> bash

## Remove all images 
docker rmi -f $(docker images -q)
