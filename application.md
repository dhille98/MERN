## deploying mern application in 3-tier applications 

`git clone https://github.com/dhille98/MERN.git`
* three tier aplications arctitechture  
  - **presentations (UI/Frontend)**
  - **Bussiness logic (server/backend)**
  - **Data(db)**
* i have working on MERN based application 

* this application **MERN** based application 
  - **M:** Mongodb
  - **E:** Express
  - **R:** React.js 
  - **N:** node js 

* depending's our application in  on language 

- **JAVA --> WE Want to `pom.xml` file**
- **PYTHON --> WE Want to `requried.txt` file**
- **NODE.js --> WE Want to `package.json` file**
- **GO-LAng --> WE Want to `go.mod` file**
  
deploying the MERN stack Application 
=====================================

* deploying our 3 tier applications in Docker best pritice purpose using **docker Network** 
* `docker network create <name> ` creating network 
* create docker file `docker image build -t <name-of-image> <path>`
* run the container `docker container run -d -P --net <network-name> --name <container-name> image:version `
* create the container checking the docker logs `docker logs <name_image>`
* create data base `docker run  --net mern --name mongodb -d -p 27017:27017 -v ~/opt/data:/data/db mongo:latest` 


**explane in interview docker compose**

interview if you explain that there is one **Services block** there is a **network block** and there

is a **volume block** where in the services you will Define different container conf configuration that 
 
you have how to start the container where is the docker file what is theportbinding right
 
if you can explain thats imilarly for the back end and for the DB you know how to write a
  
Docker-compost-file so I will start with services like I said in the services

**docker compose**

* writing a docker compose file basic flow
  
```yaml
service:
    fronted:
        ---
        ---
        ---
    backend: 
        ---
        ---
        ---
        depends on db
    db:
        ---
        ---
        ---
    network:
        ---
        ---
    volume:
        --- name of the drive
        ---
```

**docker compose usecase**
```yaml
services:
  backend:
    build: ./mern/backend  # docker file locations
    ports:
      - "5050:5050" 
    networks:
      - mern_network
    environment:
      MONGO_URI: mongodb://mongo:27017/mydatabase  
    depends_on:
      - mongodb

  frontend:
    build: ./mern/frontend  # docker file locations
    ports:
      - "5173:5173"  
    networks:
      - mern_network
 

  mongodb:
    image: mongo:latest  
    ports:
      - "27017:27017"  
    networks:
      - mern_network
    volumes:
      - mongo-data:/data/db  

networks:
  mern_network:
    driver: bridge 

volumes:
  mongo-data:
    driver: local  # Persist MongoDB data locally
```