# Plex sobre Docker en Raspberry o cualquier SV cloud

## Step by Step

1. Tener instalado docker & docker compose
     (Solo si estas armandolo fuera de tu red local)
     a. Ir a [Plex claim](https://www.plex.tv/claim/) y obtener tu claim token
     b. Modificar el docker-compose.yml con tu claim token
3. Hacer un `docker-compose up -d` o `docker compose up -d`
4. Hacer `docker container logs qbittorrent` para obtener la contraseña temporal
5. Ir a qBittorrent `http://<server_ip>:8080` y cambiar la contraseña
6. Ir a jackett `http://<server_ip>:9117` cambiar la contraseña y configurar indexers (con agregar 1337x deberia alcanzar)
7. Ir a radarr `http://<server_ip>:7878`
     a. Configurar una contraseña
     b. Agregar qBittorrent como cliente (el hostname es qBittorrent porque todos los servicios están en la misma red de docker)
     c. Agregar jackett como indexador (el hostname es jackett). Te recomiendo usar el modo torznab
     d. En Media Management, configurar el renombrado de archivos para que plex los detecte correctamente (tenes que tickear la opcion y darle a guardar nomas)
     e. Configurar la libreria de películas (/movies). Si esto te da error de permisos solo tenes que hacer `sudo chown -R 1000:1000 /mnt/storage/media` (o donde hayas configurado la env variable ${MEDIA})
8. Ir a sonarr `http://<server_ip>:8989`
     a. Hacer todo lo mismo que en radarr, aca la libreria de series esta en /tv.
9. Ir a plex `http://<server_ip>:32400/manage` y configurar tu biblioteca de series y películas (/media)
10. (opcional) Si lo estas montando en un SV cloud tenes que encender el acceso directo porque sino por default hace un tunnel por un proxy de plex que es muy lento. Te vas a dar cuenta porque no ves el contenido en la calidad que deberias.
