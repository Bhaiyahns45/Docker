
![download (1)](https://user-images.githubusercontent.com/72096831/200459883-2ff14cb5-9378-4e5a-bbae-c8d423fb9220.png)



## Dockerfile example for python as base image

    # for a base image from python
    FROM python:3.8
    
    # define the present working directory
    WORKDIR /folder_name
    
    # copy the contents into the working dir
    COPY . /folder_name
    
    # run pip to install the dependencies of the app
    RUN pip install -r requirements.txt
    
    #expose the port
    EXPOSE 5000
    
    # define the command to start 
    CMD ["python","run.py"]


---------------------------
---------------------------

## Image

#### 1. Pull the image from docker hub
    docker pull username/image_name

#### 2. Push image to docker hub
    docker tag new_image username/image_name
    
    docker push  username/new_image

#### 3. List all docker images
    docker images
    
#### 4. Delete image
    docker rmi image_name
    
#### 5. Delete all image
    docker rmi -f $(docker images -q)
    
#### 6. List all docker images in your docker hub
    docker search username

#### 7. Build docker image from dockerfile
    docker build -t image_name .

#### 8. Save docker image in tar file
    docker save image_name > file_name.tar
    
#### 9. Load docker image from tar file
    docker load < file_name.tar (window)
    
    docker load -i file_name.tar (linux)

---------------------------
---------------------------

## Container

#### 1. Start container
    docker start container_name

#### 2. Stop container
    docker stop container_name
    
#### 3. Stop all running container
    docker stop $(dokcer ps -a -q)
    
#### 4. Delete container
    docker rm container_name
    
#### 5. Delete all stopped container
    docker rm $(dokcer ps -a -q)
    
#### 6. Go inside container
    docker attach container_name
    
#### 7. List all containers
    docker ps -a
    
#### 8. List all running containers
    docker ps 

#### 9. Make container from docker image and run it
    docker run -it --name container_name image_name
  
    docker run -td --name container_name -p 5000:5000 image_name (port mapping)
    
    OR
   
    docker run -p 5000:5000 -d image_name
    
---------------------------
---------------------------
 
 
 
 

