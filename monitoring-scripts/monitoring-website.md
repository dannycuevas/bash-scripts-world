# Creating a Monitoring App Container

- We will use the following shell script to be running on a container

```
#!/bin/bash

#####################
# -The script is using a "while true" loop which means in will run indefinitely
# and will keep running until it is manually stopped.
# 
# "echo" will print the current date and time.
# 
# "curl" use to retrieve the webpage and measures the timeit takes to complete the request, as well as
# the http status code returned by the server and writes to the console.
#
# The "-k" allows "curl" to connect to an SSL website without verifying the certificate.
#
# "sleep" pauses the script for a specific number of seconds, 
# specified by the interval variable, the interval will be defined as an environment variable.
# 
# "done" just completes the loop.
# 
# This script is useful for monitoring the perfomance of a website, by repeatedly sending 
# requests to it, and measuring the response time and HTTP status code.
#
#####################
 
while true; do echo -n "$(date) "; curl -s -o /dev/null -w "%{time_total} %{http_code}\n" $HOST -k; sleep $INTERVAL; done
```

- Make sure that the script will be an executable file
```
chmod +x monitoring-app.sh
```

- And then build the image with Docker
```
docker build -t monitoring-app .
```

- Tag the newly created image to be able to later push it
- Tagging will create an additional image, and not replace an image
```
docker tag monitoring-app <your-registry>/monitoring-app:v1

docker tag monitoring-app danielcuevas/monitoring-app:v1
```

- Push your new image to your repository
```
docker push <your-registry>/monitoring-app:v1

docker push danielcuevas/monitoring-app:v1
```

- Run a new container from the image in your registry
- This command will set the environment variables needed to be pass to the shell script
- You can also stop it running the `docker stop` command if you need
```
docker run -e INTERVAL=5 -e HOST=microsoft.com <your-registry>/my-troubleshooting-app:v1

docker run -e INTERVAL=5 -e HOST=microsoft.com danielcuevas/monitoring-app:v1
```

- You will get an output like this
```
Fri May  9 00:55:42 UTC 2025 9.810770 000
Fri May  9 00:55:57 UTC 2025 9.809692 000
Fri May  9 00:56:12 UTC 2025 7.760862 307
Fri May  9 00:56:25 UTC 2025 3.492250 307
```
