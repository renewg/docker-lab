# Ejercicio 1
Crear un contene
## Paso 1

### Ejecuta un contenedor basado en la imagen: ubuntu
Se ejecuta un docker run -dit ubuntu
La opción -d es para que no se quede ligada a la terminal y -it para que sea interactiva, ya que de lo contrario, finalizaría directamente.
<img width="1845" height="458" alt="Ejercicio1b" src="https://github.com/user-attachments/assets/20ef0989-836f-49d6-a44a-1c1ae1873ca9" />

### Accede a la terminal del contenedor.
Nos conectamos al contenedor ejecutando interactivamente bash.
 
### Instala curl:

apt-get update
apt-get install curl
<img width="1415" height="600" alt="Ejercicio1c" src="https://github.com/user-attachments/assets/7bf0ddeb-315b-4b07-8a28-285d2093938f" />

### Comprueba que funciona:

curl --version
<img width="1488" height="171" alt="Ejercicio1d" src="https://github.com/user-attachments/assets/30b7ac2f-b261-423a-a44b-2e8c4a871121" />


### Pregunta
¿Con qué comando podrías guardar los cambios del contenedor como una nueva imagen?
docker commit <dockerid> <nuevoNombreImagen>

## Paso 2 --- Dockerfile

### Crea un Dockerfile que haga lo mismo automáticamente.

Ejemplo:
FROM ubuntu

RUN apt-get update && apt-get install -y curl

### Construye la imagen y ejecuta un contenedor.
Construímos la imagen ejecutando el docker build indicando que busque el fichero Dockerfile en el directorio actual.
<img width="1848" height="729" alt="Ejercicio2a" src="https://github.com/user-attachments/assets/8837e0f7-9af3-420e-8bcb-1b6e0393e00e" />

### Comprueba que curl está instalado.
Nos conectamos para ejecutar directamente un curl --version
<img width="1506" height="185" alt="Ejercicio2b" src="https://github.com/user-attachments/assets/d19290b4-6c65-484f-8a30-c9eef99e7847" />

## Pregunta
¿Qué comando permite ver las capas de una imagen Docker?
docker history

# Ejercicio 3. Volúmenes persistentes

## Ejecuta un contenedor de:

postgres:17

## Usa un volumen Docker montado en:

/var/lib/postgresql/data

## Si ejecutas una opción de postgres a partir de la 18, usa un volumen Docker montado en:

/var/lib/postgresql

## Crear volumen
Se ejecuta un docker volume create
<img width="1369" height="116" alt="Ejercicio3a" src="https://github.com/user-attachments/assets/2ca30d98-53a1-449c-8ab5-f8e2141e5669" />


## Conéctate a la base de datos.
Nos conectamos a la base de datos con docker exec -it ejercicio3 psql -U admin -d ejercicio3_db
para acceder al CLI de posgresql

## Crea la tabla:

CREATE TABLE items (
 id SERIAL PRIMARY KEY,
 name TEXT
);

## Inserta un registro
INSERT INTO items(name) VALUES ('item1');

Tras ejecutar esas consultas se puede comprobar que los datos se encuentran insertados.
<img width="1296" height="409" alt="Ejercicio3b" src="https://github.com/user-attachments/assets/8eb0ecdb-bc76-4db6-b07c-a94728185f67" />

## Comprobación

    Para el contenedor: docker stop ejercicio3
    Elimina el contenedor: docker rm ejercicio3
    Crea un nuevo contenedor usando el mismo volumen
    

## Comprueba que los datos siguen existiendo.
Tras volver a crearlo se puede apreciar que los datos siguen existiendo.
<img width="1373" height="507" alt="Ejercicio3c" src="https://github.com/user-attachments/assets/e63333bd-904e-4d28-affd-efabd1cffdb7" />


# Ejercicio 4. Bind mounts

## Crea un archivo en tu máquina:

index.html

Ejemplo:

<h1>Hola Docker</h1>

## Ejecuta un contenedor nginx:

    mapea el puerto 80
    monta el archivo en:/usr/share/nginx/html/index.html
    
Para ello durante la creación usamos el comando docker run con las opciones:
 -p 8000:80  para mapear el puerto del anfitrión 8000 en el puerto 80 del contenedor
 --mount type=bind,source=./Ejercicio4/index.html,target=/usr/share/nginx/html/index.html para exponer el fichero al contenedor
<img width="1678" height="454" alt="Ejercicio4a" src="https://github.com/user-attachments/assets/eb716199-e54f-4592-a8b1-402a6a493401" />

## Abre el navegador.
<img width="1387" height="250" alt="Ejercicio4b" src="https://github.com/user-attachments/assets/3eae12d8-e851-46a1-b46c-83517e812a45" />

## Pregunta:
¿Qué ocurre si modificas el archivo index.html en tu máquina?
Que al estar montado, se ve actualizado directamente.
<img width="1237" height="228" alt="Ejercicio4c" src="https://github.com/user-attachments/assets/058800e4-e1bf-4479-9968-adc407800f71" />


# Ejercicio 6. Creando redes privadas

## Crea una red llamada:

my-net
Creamos la red con el comando docker network create
<img width="868" height="133" alt="Ejercicio6a" src="https://github.com/user-attachments/assets/4c2dc790-d4cc-43d5-8085-e302cb5700a0" />

## Arranca dos contenedores ubuntu en esa red.
Para ello usamos la opción --network my-net en la creación
<img width="1257" height="184" alt="Ejercicio6b" src="https://github.com/user-attachments/assets/8b44d51e-28ba-49a7-99ed-ae5001a5cac8" />

## Instala ping si es necesario.
Ejecutamos un bash en uno de los contendores e instalamos el paquete iputils-ping
<img width="930" height="637" alt="Ejercicio6c" src="https://github.com/user-attachments/assets/abdfb923-69b9-4211-9044-e3fc87620853" />

## Desde un contenedor intenta hacer:

ping otro_contenedor
Para ello necesitamos conocer la ip de cada contenedor. Lo obtenemos con el comando
docker network instpect my-net
<img width="944" height="634" alt="Ejercicio6d" src="https://github.com/user-attachments/assets/a33d3b4c-67c9-433d-9e9f-7306addf22ac" />
Vemos que el contenedor ejercicio4a tiene la ip 172.20.0.2 y que el otro tiene la 172.20.0.3 y al hacer ping funciona.
<img width="871" height="285" alt="Ejercicio6e" src="https://github.com/user-attachments/assets/b10e7c76-7b76-4f0c-a1fe-1750ae6a545a" />


## Pregunta
¿Los contenedores pueden comunicarse entre sí?
Sí, si se les configura una misma red para ello.

# Ejercicio 9. Docker Compose --- Compartiendo volúmenes

## Crea un fichero:

docker-compose.yml

Con dos servicios.
writer

Debe:

    montar un volumen en /app/logs
    escribir un timestamp cada 30 segundos

reader

Debe:

    montar el volumen en modo solo lectura
    mostrar el contenido en consola
Al Ponerlo en marcha, nos falla la 1ª vez ya que el fichero a leer no existe aún. Pero al volver a ejecutarlo y ya existir el fichero, funciona.
<img width="1102" height="837" alt="Ejercicio9b" src="https://github.com/user-attachments/assets/ec21d0c0-a1b6-4a9f-84ba-a12ec315b2fd" />



