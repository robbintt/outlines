# Guide for using the Jupyter `datascience-notebook` with Docker

(brew must be installed; cask must be installed)
brew cask install docker

## Steps

I recommend doing this from your home internet. It is about 2 GB. 

1. `brew cask install docker`
2. run docker (open spotlight search or press CMD+space, and type docker)
  - docker should be running in the top bar of the mac
3. `docker pull jupyter/datascience-notebook` . (2 GB)
  - `docker images` - see what's installed
4. `docker run -p 8888:8888 jupyter/datascience-notebook`

Go to the URL it spits out (in iterm you can command+click the URL to open it in your browser)

### Part II

ssh into your docker container.

1. `docker ps` get the name of your container
2. docker exec -it <container name> /bin/bash
  - use generically: `docker exec -it <container name> <command>
3. that home directory seems to be where notebooks go or something
  - i put a text file in jovyan@e47f8b66eea3:~/work/ and could see it


## Resources

### we decided to try this notebook:
- https://hub.docker.com/r/jupyter/datascience-notebook/

### found on this list of notebooks:
- https://hub.docker.com/r/jupyter/notebook/

### i did not review all the docker containers that jupyter manages
- https://hub.docker.com/u/jupyter/

### Planet Labs maintains notebooks too!
- https://github.com/planetlabs/notebooks
