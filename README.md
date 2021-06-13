# docker_healthcheck_by_ramm
HEALTHCHECK CMD curl --fail http://localhost:5000/ || exit 1
$ vi Dockerfile
FROM python:3.6-alpine
RUN apk add -update bash
RUN apk add -update curl
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
HEALTHCHECK CMD curl --fail http://localhost:5000/ || exit 1

•	Bash & curl is to run a HEALTHCHECK 
•	exit 1  Including Python, is for exit(0) to indicate success, and exit(1) or any other non-zero value (in the range 1.. 255) to indicate failure.
•	In this case, we are using the default options, which are interval 30s, timeout 30s, start-period 0s, and retries 3. Read the health check instruction reference for more information on the options.
	Through cli   https://docs.docker.com/engine/reference/run/#healthcheck 
See the health status
•	Let's rebuild and run our container.
$ docker build -t docker-flask .
$ docker run --rm --name docker-flask -p 5000:5000 docker-flask
$ docker ps -a
 
Now let's take a look at the health status. Notice we have the --name option to the above command so we can easily inspect the container.
