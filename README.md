# post-it

## Local Docker run

This will allow you run your container using the docker run command

- Create a network to connect the backend to the DB

docker network create mongo-network

docker run -d -p 27017:27017 \
—name mongodb \
—network mongo-network \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=password \
mongo

docker run -d -p 8081:8081 \
—name mongo-express \
—network mongo-network \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
-e ME_CONFIG_MONGODB_SERVER=mongodb \
mongo-express

CD into the backend-project

docker build -t backend:v1 .

docker run -d -p 8080:8080 \
—name backend \
—network mongo-network \
backend:v1

## Docker Compose