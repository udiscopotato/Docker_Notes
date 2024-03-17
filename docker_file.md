- Dockerfile is a specific file, written in a specific format that docker can understand and make an image out of it.
- It follows INSTRUCTION ARGUMENT method
Some INSTRUCTION examples are: FROM, RUN, COPY, PORT, etc.
- Each lines of the Instruction builds a separate layer to create a Image.
- All the layers build are cached or saved so that it'll help rebuild the image incase the build failed.
- we can add .dockerignore files which will ge dignored by adding them to .dockerignore.
### FROM
This defines what the base OS should be, for out application. Every Docker image must be based-on of anoter image. All Dockerfile must run from "FROM" instruction.
### WORKDIR
Sets the working directory for subsequent instructions.
### RUN
It instructs Docker to run a perticular command to run on the base image.
### COPY
It copies files from local system to the Docker image.
### ADD
It's same as copy with some additional functionalities like handling URLs and tar files. COPY is more preferable due to it's simplicity.
### EXPOSE
Declares which ports the container will listen on at runtime.
Does not actually publish the port.
### ENV
Sets environment variables in the image.
### CMD
It allows us to run static command during image creation.
### ENTRYPOINT 
It allows us to run a command, that will run when the image is being run as container. It also appends the argument we pass during docker run.
Example:
```javascript
FROM
ENTRYPOINT ["sleep"]
CMD ["5"]
```
in above example the default entry point is "sleep" command and it's value is "5" from CMD. ENTRYPOINT can also append arguments from out run command i.e. if we run the container using command "docker run containername 50" it'll append 50 to entrypoint and it'll run command "sleep 50".

### Example
Dockerfile
```javascript
FROM python:3.9
WORKDIR /app
RUN pip install requests
ENV MY_VAR=my_value
COPY app.py /app/
EXPOSE 5000
CMD ["python", "app.py"]
```

## MULTI-STAGE BUILD
We can use multi stage build to get optimized low sized image 
```javascript
FROM node:14 AS build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 3000
CMD ["nginx","-g", "daemon off"]
```



## Best Practices
- Always use repository update and install command on a single instruction so that it updates the repository according to lattest indexes.
i.e.    "RUN apt update && apt install -y python python3-pip python-dev"
OR
```javascript
RUN apt update && apt install -y \
    python \
    python3-pip \
    python-dev
```
- we can use "--no-cache" to disable the cache during building a docker image.
- Always use persistant volume sollutions like docker volume, redis etc to make container data persistent whenever needed.
- Always try to use low sized image make image size low so that it can start up fast and take less size.
- only install essensial packages.
- Avoid sending unnessesery files to build. use .dockerignore
- Try to use multi-stage build to make the image low size and efficient.

















copy vs add