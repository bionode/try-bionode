# try-bionode

Try bionode using docker

## Installation

```
docker pull bionode/try-bionode
```

## Usage

Simply run the image

```
docker run -it bionode/try-bionode
```

## Use with docker-browser-server

You can also use this image with [adventure-time](https://github.com/maxogden/adventure-time)

```
npm install -g docker-browser-server
docker-browser-server bionode/try-bionode # and then set adventure-time to point to localhost:8080
```

## How does http://try.bionode.io works?
The [try.bionode.io](http://try.bionode.io) website is a ```gh-pages``` hosted at [bionode/get-bionode](https://github.com/bionode/get-bionode).
It contains a tutorial written in [Markdown](https://github.com/bionode/get-bionode/tree/master/markdown) and uses ```WebSockets``` to connect to the instance (so it might have some issues on some networks due to firewalls).
The instance that provides the online command line interface, editor and filesystem is a ```Docker container``` generated per-user each time they connect (i.e., they go to [try.bionode.io](http://try.bionode.io)).
These ```Docker containers``` come from a ```VM``` hosted on ```AWS```.
It's a basic ```Ubuntu VM``` with ```Docker``` and the following ```init script```.

```bash
# located at /etc/init/bionode.conf
start on filesystem
exec docker-browser-server bionode/try-bionode --port 80 --persist
```

So ```docker-browser-server``` from the [maxogden/adventure-time](https://github.com/maxogden/adventure-time) project is a server that listens for connections (from the ```gh-pages```) and will create a ```Docker container``` per user by using the ```Docker image``` [bionode/try-bionode](https://github.com/bionode/try-bionode) which is published on the [Docker hub](https://hub.docker.com/r/bionode/try-bionode/). The [Dockerfile](https://github.com/bionode/try-bionode/blob/master/Dockerfile) in that repo is the one that needs to be modified in order to include everything needed for the tutorial.


## License

MIT
