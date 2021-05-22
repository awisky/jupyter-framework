### Minimalist Jupyter notebook docker setup

This is a minimalist template you can use to start your Jupyter project.



If you have Docker already installed, you only need to clone this repository.



```bash
git clone https://github.com/awisky/jupyter-framework.git
```

The docker-compose file define the jupyter-serving service using the Dockerfile inside the jupyter folder

```yaml
version: '2'

services:
  jupyter-serving:
    build: ./jupyter
    ports:
      - '8888:8888'
    volumes:
      - ./notebooks:/home/jovyan/work/
```



The jupyter-serving Dockerfile:

```yaml
FROM jupyter/minimal-notebook:latest

USER root

# Update aptitude with new repo
RUN apt-get update \
    && apt-get install -y git

COPY ./requirements.txt ./

# Install Wget
RUN apt-get update && apt-get install -y --no-install-recommends wget

# Install Python3 and all the requirements.txt
RUN apt-get update && apt-get install -y --no-install-recommends \
        apt-utils \
        python3-dev \
        python3-wheel \
    && pip3 install --upgrade pip \
    && pip3 install -r requirements.txt
```

As you can see the last instruction executes pip3 install with the requirements.txt argument. 

Use the requirements.txt file to add all the python libraries you want to use in your project.



Enter into de Jupiter-framework folder and run docker-compose up to run the container

```
docker-compose up
```

After a couple of minutes you will see the access to the notebook

```bash
jupyter-serving_1  |     To access the notebook, open this file in a browser:
jupyter-serving_1  |         file:///home/jovyan/.local/share/jupyter/runtime/nbserver-17-open.html
jupyter-serving_1  |     Or copy and paste one of these URLs:
jupyter-serving_1  |         http://d80fdc39fbf9:8888/?token=0e77ff0ee341c2b4f5283d3d58d8365c9b87c54bda834bd7
jupyter-serving_1  |      or http://127.0.0.1:8888/?token=0e77ff0ee341c2b4f5283d3d58d8365c9b87c54bda834bd7
jupyter-serving_1  | [I 07:38:01.620 NotebookApp] 302 GET /?token=0e77ff0ee341c2b4f5283d3d58d8365c9b87c54bda834bd7 (192.168.32.1) 0.770000ms
```

You just need to access to the provided url. i.e

 http://127.0.0.1:8888/?token=0e77ff0ee341c2b4f5283d3d58d8365c9b87c54bda834bd7

Don't forget to copy the entire url including the token.



That's it you are done! Congrats :-)