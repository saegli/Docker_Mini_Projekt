Installieren Sie Docker, falls noch nicht geschehen: https://docs.docker.com/get-docker/

Erstellen Sie einen neuen Ordner für das Projekt und navigieren Sie in das Verzeichnis:


mkdir mein-webserver
cd mein-webserver

Erstellen Sie eine einfache index.html-Datei im Projektordner:


echo '<h1>Willkommen auf meiner Webseite!</h1>' > index.html

Erstellen Sie ein Dockerfile im Projektordner:


touch Dockerfile

Öffnen Sie das Dockerfile in einem Texteditor und fügen Sie den folgenden Inhalt hinzu:


FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]

Erstellen Sie das Docker-Image:

docker build -t mein-webserver .

Erstellen Sie lokale Verzeichnisse für die Webseite und die Logdateien:

mkdir logs
mkdir html
cp index.html html/

Starten Sie den Container:

docker run --name mein-webserver -p 8080:80 -v $(pwd)/html:/usr/share/nginx/html -v $(pwd)/logs:/var/log/nginx -d mein-webserver

Öffnen Sie einen Webbrowser und navigieren Sie zu http://localhost:8080.
