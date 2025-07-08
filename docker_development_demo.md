# Demo Project: Using Docker for Local Development

## Environment:
- Host: Local Machine
- Linux Ubuntu 24.10 x64

## Steps to Use Docker for Local Development:

1. **I cloned the example git project on my local machine:**

```bash
git clone git@gitlab.com:twn-devops-bootcamp/latest/07-docker/js-app.git
```

![image](https://github.com/user-attachments/assets/3a3df343-4561-40a0-a871-89a3dce00130)

2. **I then pulled the MongoDB image from Docker Hub onto my local machine in the project directory:**

```bash
cd /js-app/app
docker pull mongo
```

![image](https://github.com/user-attachments/assets/2240e1be-2901-4612-9640-edab54943c35)

3. **I pulled the Mongo-express image from Docker Hub onto my local machine in the project directory:**

```bash
docker pull mongo-express
```

![image](https://github.com/user-attachments/assets/fa7bcf62-a2e9-4e27-99e4-67d8bf690f87)

**To see the locally running images

```bash
docker images | grep mongo
```

![image](https://github.com/user-attachments/assets/5b273db9-c9bc-46be-80d9-493428229eed)

4. **I then ran the Mongo and Mongo-express containers to make the MongoDB database available for our application, and also to connect Mongo-express with the MongoDB container. To do this, I created a new Docker network for MongoDB and Mongo-express and checked it out:**

```bash
docker network create mongo-network
docker network ls
```

![image](https://github.com/user-attachments/assets/8c87b430-0be8-4a19-a362-43c2ae6eabf0)

**To make the MongoDB container and the Mongo-express container run in this Mongo Network,I then provided that network option when I ran the container, in the docker run command**

```bash
docker run -d \
-p 27017:27017 \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=password \
--name mongodb \
--net mongo-network \
mongo
```

**To see whether it was successful I then executed the following

```bash
docker logs <containerID>
```

**To make Mongo-express connect to the running MongoDB container on startup, I executed the following command, including the Docker server env variable and mongo network, which would then allow MongoDB to connect to the Mongo-express container on startup**

```bash
docker run -d \
-p 8081:8081 \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
-e ME_CONFIG_BASICAUTH_USERNAME=user \
-e ME_CONFIG_BASICAUTH_PASSWORD=pass \
--net mongo-network \
--name mongo-express \
-e ME_CONFIG_MONGODB_SERVER=mongodb \
-e ME_CONFIG_MONGODB_URL=mongodb://mongodb:<portnumberIused>
mongo-express
```

**To see whether it was successful I then executed the following

```bash
docker logs <containerID>
```

5. **Finally, I created a new database via MongoExpress UI, configured the Nodejs application code to connect with the Mongo database, then ran the node .js app:**

```bash
cd app
npm install 
node server.js
```
