
```bash
git clone https://github.com/vfarcic/go-demo.git

docker-compose up -d

docker-compose ps

docker container inspect go-demo_app_1

docker container inspect go-demo_app_1 | jq '.'

# Get the matching port and put it in a variable

PORT=$(docker container inspect go-demo_app_1 | jq -r '.[0].NetworkSettings.Ports."8080/tcp"[0].HostPort')

```

#

docker container run -it --rm -v $PWD:/tmp -w /tmp golang:1.6 sh -c "go get -d -v -t && go build -v -o go-demo"


# Set up a local registry

docker container run -d --name registry -p 5000:5000 registry:2

docker image tag go-demo localhost:5000/go-demo

docker image push localhost:5000/go-demo

docker image tag go-demo localhost:5000/go-demo:1.1

docker image push localhost:5000/go-demo:1.1

# Stop Container

docker container rm -f registry
