# Node Docker Image

This image is for a development environment with node.

## Build

Generate a new test image in development environment with:

```sh
bin/build-local.sh
```

A new image will be generated locally with the name
`lets/docker-node-local:latest`. Test the changes you want with this image and
make sure they are all good.

If you push an updated master branch, the automated build will generate a "latest" image in dockerhub.

You should however always tag your release and push a tagged release:

```
git tag 0.0.x
git push origin 0.0.x
```

## Usage

Your project must contain a Node application and an appropriate configuration
(example with docker-compose):

```yml
version: '3.6'
services:
  front:
    image: lets/docker-node:latest
    container_name: some-name
    command: npm run dev
    env_file:
      - .env
    volumes:
      - .:/app
    ports:
      - 3000:8000
    networks:
      - net
    tty: true
    stdin_open: true
```

Note that it requires app code mounted at `/app`.
