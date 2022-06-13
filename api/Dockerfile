##Each line below adds a new layer
##Dockerfile is to build image, which means we want to build an isolated working enviroment different from the current work environment

# FROM node:17-alpine   
#get version 17 and alpine distribution of Linux, instead of the default distribution
#Can be helpful since we don't want to mess up everything when the default 
#distribution change(default distribution is always the latest version) 

# WORKDIR /app
##Specify all the installations are under /app folder

# COPY . .
#copy all the files in root directory to /app folder. 
#Since we have specified the workdir as /app, then the second "." means the /app directory

# RUN npm install
#to install all the depentency in package.json in /app folder

# EXPOSE 4000
# it is not necassary, only required for docker desktop port mapping

## don't write "RUN node app.js" since it is only the bulletpoint of the images.
## "RUN node app.js" should be run in container,但这里是镜像，就是instruction，而不是具体执行的地方
## Instead，用下面这句去指导接下来的container需要去 RUN node app.js
# CMD ["node", "app.js"]


##Layer Caching
##如果修改了app.js的内容会影响COPY这一步，而copy之前的部分会从cache中获取，
##这样会节省时间，所以为了节省时间，我们可以把COPY往下移，这样COPY之前的都可以
##从Cache中获取，优化的方式如下：

FROM node:17-alpine   

RUN npm install -g nodemon

WORKDIR /app

COPY package.json .
# ##需要先copy这个，因为只有基于这个文件，才能run npm install

RUN npm install

RUN npm install express

COPY . .

EXPOSE 4000

# CMD ["node", "app.js"]

CMD ["npm", "run","dev"]

