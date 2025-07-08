# Demo Project: Using Docker for Local Development

## Environment:
- Host: Local Machine
- Linux Ubuntu 24.10 x64

## Steps to Use Docker for Local Development:

1. **I cloned the example git project on my local machine:**

'''bash
git clone git@gitlab.com:twn-devops-bootcamp/latest/07-docker/js-app.git
'''

![image](https://github.com/user-attachments/assets/3a3df343-4561-40a0-a871-89a3dce00130)

2. **I then pulled the MongoDB image from Docker Hub onto my local machine in the project directory:**

'''bash
cd /js-app/app
docker pull mongo
'''

![image](https://github.com/user-attachments/assets/2240e1be-2901-4612-9640-edab54943c35)

3. **I pulled the Mongo-express image from Docker Hub onto my local machine in the project directory:**

'''bash
docker pull mongo-express
'''

![image](https://github.com/user-attachments/assets/fa7bcf62-a2e9-4e27-99e4-67d8bf690f87)

**To see the locally running images

'''bash
docker images | grep mongo
'''

![image](https://github.com/user-attachments/assets/5b273db9-c9bc-46be-80d9-493428229eed)

4. **I then ran the Mongo and Mongo-express containers to make the MongoDB database available for our application, and also to connect Mongo-express with the MongoDB container. To do this, I created a new Docker network for MongoDB and Mongo-express and checked it out:**

'''bash
docker network create mongo-network
docker network ls
'''

![image](https://github.com/user-attachments/assets/8c87b430-0be8-4a19-a362-43c2ae6eabf0)

**To make the MongoDB container and the Mongo-express container run in this Mongo Network,I then provided that network option when I ran the container, in the docker run command**

'''bash






