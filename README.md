# Creación de un contenedor con python | Sergio De La Iglesia Lorenzo

1. Creación del script

El script que se necesita usar para esta práctica es uno de python en el que se va a recoger información sobre un vídeo específico que se debe pasar a través de un enlace. El código es el siguiente:

```
from pytube import YouTube

#link = input("Enter the link: ")
yt = YouTube("https://www.youtube.com/watch?v=aFqTjk3kcEw&ab_channel=Garajedeideas")

#Title of video
print("Title: ",yt.title)
#Number of views of video
print("Number of views: ",yt.views)
#Length of the video
print("Length of video: ",yt.length,"seconds")
#Description of video
print("Description: ",yt.description)
#Rating
print("Ratings: ",yt.rating)

```

2. Creación del Dockerfile

El archivo "Dockerfile" es importante para crear la imagen personalizada. Esto se hace con el comando "docker build ." De esta forma usa el archivo en la carpeta del terminal en la que nos encontramos para montar la imagen. El contenido de este fichero es el siguiente:

```
FROM python:3

WORKDIR /usr/src/app

COPY requirements.txt ./

RUN pip install --no-cache-dir -r requirements.txt

```
3. Creación de docker-compose

El docker-compose.yml es el fichero que debe crearse también dentro de la misma carpeta desde la que estamos trabajando para que se forme correctamente el contenedor. El fichero debe incluir la imagen que ya se ha creado anteriormente, con las siguientes opciones extra para que se ejecute.
```
services:
  python:
    image: youtubeimage:chromecast
    volumes:
      - ./app:/usr/src/app
    stdin_open: true
    tty: true
    working_dir: /usr/src/app
    command: python3
```
4. Imagen creada personalizada subida (enlace)

https://hub.docker.com/layers/sergio10326/youtubeimage/latest/images/sha256-9c7f454c74408d05b722d325a9b24c8c81ecabf99b690bbba2cc0814c3f0583a?tab=layers

