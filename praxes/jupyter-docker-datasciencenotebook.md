# Guide for using the Jupyter `datascience-notebook` with Docker

(brew must be installed; cask must be installed)
brew cask install docker


## Quick References

- [Guide covers this notebook](https://hub.docker.com/r/jupyter/datascience-notebook/)
    - Use this to determine what capabilities we have
    - THIS WILL BE OUTDATED:
    - Jupyter Notebook 5.2.x
    - Conda Python 3.x environment
    - pandas, matplotlib, scipy, seaborn, scikit-learn, scikit-image, sympy, cython, patsy, statsmodel, cloudpickle, dill, numba, bokeh pre-installed
    - Conda R v3.3.x and channel
    - plyr, devtools, shiny, rmarkdown, forecast, rsqlite, reshape2, nycflights13, caret, rcurl, and randomforest pre-installed 
    - The tidyverse R packages are also installed, including ggplot2, dplyr, tidyr, readr, purrr, tibble, stringr, lubridate, and broom
    - Julia v0.6.x with Gadfly, RDatasets and HDF5 pre-installed
    - Unprivileged user jovyan (uid=1000, configurable, see options) in group users (gid=100) with ownership over /home/jovyan and /opt/conda
    - tini as the container entrypoint and start-notebook.sh as the default command
    - A start-singleuser.sh script useful for running a single-user instance of the Notebook server, as required by JupyterHub
    - A start.sh script useful for running alternative commands in the container (e.g. ipython, jupyter kernelgateway, jupyter lab)
    - Options for a self-signed HTTPS certificate and passwordless sudo
- [Jupyter Notebook Shortcuts](http://maxmelnick.com/2016/04/19/python-beginner-tips-and-tricks.html)


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

#### This is based on the [docker-stacks](https://github.com/jupyter/docker-stacks#visual-overview)

The following is a summary of the linked diagram. The diagram is a superior explanation.

Docker stacks are very interesting:
1. `tensorflow-notebook1`
1. `datascience-notebook`
1. `pyspark-notebook` --> `all-spark-notebook`

All these notebooks are based on the `scipy-notebook`, which is `ubuntu base-notebook` based. (And all descend from `minimal-notebook`).

There is a separate `r-notebook`

### found on this list of notebooks:
- https://hub.docker.com/r/jupyter/notebook/

### i did not review all the docker containers that jupyter manages
- https://hub.docker.com/u/jupyter/

### Planet Labs maintains notebooks too!
- https://github.com/planetlabs/notebooks
