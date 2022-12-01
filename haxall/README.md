# Haxall on Docker
Source: https://github.com/haxall/haxall

This folder contains docker files to create a new container with Ubuntu:latest and the most current version of Haxall


To start the container:
1. Clone this repo and navigate to the /haxall folder

    ```git clone https://github.com/LBNL-ETA/haxall-based-fault-correction.git```

2. Ideally, use docker-compose to build and run the container

    `docker-compose build`

3. Start the container in disconnected (background) mode

   `docker-compose up -d`

4. At this point you should be able to connect to `http://localhost:8080` and login to a blank Haxall project with default credentials `admin/pass`  

5. The project files will be mounted under `haxall/demo` on the host machine under the github repository. These files will persist between docker sessions.  

---

If you don't have docker-compose installed, you should. But if you don't, you can use the following commands:

`docker build -t haxall .`

`docker run -it -p 8080 haxall 'bash'`

Then from the shell within the container:

`cd /haxall/bin`

`fan hx init demo`

`fan hx run demo`

At this point you should have a blank project active and available at `http://localhost:8080`, however the project files will not persist between docker sessions. To do this, get *docker-compose*.
