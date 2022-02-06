# Linux/MacOS

## Installation



### Download

You need to have [Docker](https://docs.docker.com/get-docker/) installed.

Furthermore, OCR4all expects a specific folder structure. Change into the directory where you want to manage your OCR4all projects.

Then create the following structure:

```
.
└── ocr4all
    ├── data
    └── models
```

This structure can be created with the following command:

```bash
mkdir -p ocr4all/{models,data}
```

Go to the directory where you want to put your 

Open your terminal and type:

```bash
docker pull uniwuezpd/ocr4all
```

If you want to install other docker images, you can find a list of available tags and the respective pull commands [here](https://hub.docker.com/r/uniwuezpd/ocr4all/tags).

The download of the docker image takes a while (6.5 GB).

### Configuration

Make sure you are in the the `ocr4all` directory:

```bash
cd ocr4all
```

Build the docker container:

```bash
sudo docker run -p 1476:8080 -u `id -u root`:`id -g $USER` --name ocr4all \
-v $PWD/data:/var/ocr4all/data \
-v $PWD/models:/var/ocr4all/models/custom \
-it uniwuezpd/ocr4all
```

Now the OCR4all container is up and running.

If you type 

```bash
docker ps -a
```

you will see the somethin like

```
CONTAINER ID   IMAGE               COMMAND             CREATED         STATUS                    PORTS                                       NAMES
5fccf7d2280d   uniwuezpd/ocr4all   "catalina.sh run"   3 minutes ago   Up 3 minutes              0.0.0.0:1476->8080/tcp, :::1476->8080/tcp   ocr4all
```

Now go to [`http://localhost:1476/ocr4all/`](http://localhost:1476/ocr4all/) in your web browser an you will see the OCR4all window.

![OCR4all Project Overview](./img/OCR4all_Project_Overview.png)


### Stop the container

It is not strictly necessary to stop the container when you are done with your work.
If you want, you can stop it by typing

```bash
docker stop ocr4all
```

### Update

If you want to update OCR4all to the latest release, remove the docker container and pull the docker image:

```bash
docker remove ocr4all

docker pull uniwuezpd/ocr4all
```

Then rebuild the docker container as explained above.