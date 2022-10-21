
1- Pull the image from docker hub using command ( docker pull username/image_name )

2- now check the image using command ( docker images )

3- if image exists make the container  and port mapping form that image and run it using command ( docker run -td --name flaskapp_container -p 5000:5000 image_name )
or 
docker run -p 5000:5000 -d image_name

4- app run at http://localhost:5000/



Other commands:-
docker build -t my_image .

docker run -it --name my_container my_images

docker search username

first give an tag and then push to hub

docker tag my_image  username/new_image

docker push  username/new_image

docker pull username/new_image:latest
