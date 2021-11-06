#Exercises of part 1

##1.1 Getting started
Start 3 containers from image that does not automatically exit, such as nginx, detached.
Stop 2 of the containers leaving 1 up.
Submit the output for docker ps -a which shows 2 stopped containers and one running.

##1.2 Cleanup
We’ve left containers and a image that won’t be used anymore and are taking space, as docker ps -as and docker images will reveal.
Clean the docker daemon from all images and containers.
Submit the output for docker ps -a and docker images

##1.3 Secret message
Now that we’ve warmed up it’s time to get inside a container while it’s running!
Image devopsdockeruh/simple-web-service:ubuntu will start a container that outputs logs into a file. Go inside the container and use tail -f ./text.log to follow the logs. Every 10 seconds the clock will send you a “secret message”.
Submit the secret message and command(s) given as your answer

##1.4: Missing dependencies
Start a ubuntu image with the process sh -c 'echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
You will notice that a few things required for proper execution are missing. Be sure to remind yourself which flags to use so that the read actually waits for input.
Note also that curl is NOT installed in the container yet. You will have to install it from inside of the container.
Test inputting helsinki.fi into the application. It should respond with something like
```<html>

<head>
  <title>301 Moved Permanently</title>
</head>

<body>
  <h1>Moved Permanently</h1>
  <p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>
</body>

</html> ```

##1.5 Sizes of images
In a previous exercise we used devopsdockeruh/simple-web-service:ubuntu.
Here is the same application but instead of ubuntu is using alpine: devopsdockeruh/simple-web-service:alpine.
Pull both images and compare the image sizes. Go inside the alpine container and make sure the secret message functionality is the same. Alpine version doesn’t have bash but it has sh.

##1.6 Hello Docker Hub
Run docker run -it devopsdockeruh/pull_exercise.
It will wait for your input. Navigate through docker hub to find the docs and Dockerfile that was used to create the image.
Read the Dockerfile and/or docs to learn what input will get the application to answer a “secret message”.
Submit the secret message and command(s) given to get it as your answer.

## 1.7: Two line Dockerfile
By default our devopsdockeruh/simple-web-service:alpine doesn’t have a CMD. It instead uses ENTRYPOINT to declare which application is run.
We’ll talk more about ENTRYPOINT in the next section, but you already know that the last argument in docker run can be used to give command.
As you might’ve noticed it doesn’t start the web service even though the name is “simple-web-service”. A command is needed to start the server!
Try docker run devopsdockeruh/simple-web-service:alpine hello. The application reads the argument but will inform that hello isn’t accepted.
In this exercise create a Dockerfile and use FROM and CMD to create a brand new image that automatically runs the server. Tag the new image as “web-server”
Return the Dockerfile and the command you used to run the container.
Running the built “web-server” image should look like this:

$ docker run web-server
[GIN-debug] [WARNING] Creating an Engine instance with the Logger and Recovery middleware already attached.

[GIN-debug] [WARNING] Running in "debug" mode. Switch to "release" mode in production.
 - using env:   export GIN_MODE=release
 - using code:  gin.SetMode(gin.ReleaseMode)

[GIN-debug] GET    /*path                    --> server.Start.func1 (3 handlers)
[GIN-debug] Listening and serving HTTP on :8080
