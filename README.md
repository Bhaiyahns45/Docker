
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
## Dockerfile example for python as base image (Streamlit)

    # Use the Python 3.9-slim base image
    FROM python:3.9-slim
    
    # Define the present working directory
    WORKDIR /app
    
    # Copy the contents into the working dir
    COPY . /app
    
    # Install GLPK and other dependencies
    RUN apt-get update && apt-get install -y glpk-utils && \
        pip install pyomo && \
        pip install -r requirements.txt
    
    # Expose the port
    EXPOSE 8501
    
    # Set the working directory again (optional, in case you want to specify it)
    WORKDIR /app
    
    # Define the entry point command to run your Streamlit app
    ENTRYPOINT ["streamlit", "run", "main.py", "--server.port=8501", "--server.address=0.0.0.0"]


---------------------------
## Dockerfile example for python as base image (Fastapi & GLPK)

    # Use the Python 3.10 base image
    FROM python:3.10
    
    # Define the present working directory
    WORKDIR /app
    
    # Copy the contents into the working dir
    COPY . /app
    
    # Install GLPK and other dependencies
    RUN apt-get update && apt-get install -y glpk-utils && \
        pip install pyomo && \
        pip install -r requirements.txt
    
    
    # Set the working directory again (optional, in case you want to specify it)
    WORKDIR /app
    
    # Expose port 8000 to the outside world
    EXPOSE 8000
    
    # Command to run the FastAPI application
    CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]




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
    docker stop $(docker ps -aq)
    
#### 4. Delete container
    docker rm container_name
    
#### 5. Delete all stopped container
    docker rm $(docker ps -aq)
    
#### 6. Go inside container
    docker attach container_name
    docker exec -it container_id bash
    
#### 7. List all containers
    docker ps -a
    
#### 8. List all running containers
    docker ps 
    
#### 9. general
    docker stats
    docker info

#### 10. Make container from docker image and run it
    docker run -it --name container_name image_name ( make and run it )
    
    OR
  
    docker run -td --name container_name -p 5000:5000 image_name (port mapping)
    
    OR
   
    docker run -p 5000:5000 -d image_name

#### 11. Stop and remove the existing containers, then recreate them with the updated configuration:
    
    docker-compose down
    docker-compose up -d
    
---------------------------
---------------------------

Error :-

  WARNING: Retrying (Retry(total=3, connect=None, read=None, redirect=None, status=None)) after connection broken by
 => => #  'NewConnectionError('<pip._vendor.urllib3.connection.HTTPSConnection object at 0x7fbdeedbc460>: Failed to establi
 
Steps:
Open /etc/resolv.conf with a text editor: You need superuser (root) privileges to edit this file, so use a text editor like nano or vi:

bash
Copy code
sudo nano /etc/resolv.conf
or

bash
Copy code
sudo vi /etc/resolv.conf
Add the DNS server to the file: Once the file is open, add the following line to use Google's public DNS server:

bash
Copy code
nameserver 8.8.8.8
You can also add another Google DNS server for redundancy:

bash
Copy code
nameserver 8.8.4.4
Save and close the file:

If using nano, press Ctrl + O to save and Ctrl + X to exit.
If using vi, press Esc, type :wq, and hit Enter to save and exit

 
 

