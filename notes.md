docker 
docker image
ec2
ecs

Frontend (npm run build) will create three filesof[html,css,js] copy these files to public folder of backend project. Then, create a Dockerfile in the backend project root directory with the following content:

docker build . -t backend(tag name)
docker run backend-image
docker run -p 4000:3000 backend