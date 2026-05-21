# Ejercicio 1
Crear un contene
## Paso 1

Ejecuta un contenedor basado en la imagen:

ubuntu

### Accede a la terminal del contenedor.

### Instala curl:

apt-get update
apt-get install curl

### Comprueba que funciona:

curl --version

### Pregunta
¿Con qué comando podrías guardar los cambios del contenedor como una nueva imagen?

## Paso 2 --- Dockerfile

### Crea un Dockerfile que haga lo mismo automáticamente.

Ejemplo:

FROM ubuntu

RUN apt-get update && apt-get install -y curl

### Construye la imagen y ejecuta un contenedor.

### Comprueba que curl está instalado.
## Pregunta
¿Qué comando permite ver las capas de una imagen Docker?

# Ejercicio 3. Volúmenes persistentes

## Ejecuta un contenedor de:

postgres:17

## Usa un volumen Docker montado en:

/var/lib/postgresql/data

## Si ejecutas una opción de postgres a partir de la 18, usa un volumen Docker montado en:

/var/lib/postgresql

## Crear tabla

## Conéctate a la base de datos.

## Crea la tabla:

CREATE TABLE items (
 id SERIAL PRIMARY KEY,
 name TEXT
);

## Inserta un registro:

INSERT INTO items(name) VALUES ('item1');

## Comprobación

    Para el contenedor
    Elimina el contenedor
    Crea un nuevo contenedor usando el mismo volumen

## Comprueba que los datos siguen existiendo.

# Ejercicio 4. Bind mounts

## Crea un archivo en tu máquina:

index.html

Ejemplo:

<h1>Hola Docker</h1>

## Ejecuta un contenedor nginx:

    mapea el puerto 80
    monta el archivo en:

<!-- -->

/usr/share/nginx/html/index.html

## Abre el navegador.

## Pregunta:
¿Qué ocurre si modificas el archivo index.html en tu máquina?

# Ejercicio 6. Creando redes privadas

## Crea una red llamada:

my-net

## Arranca dos contenedores ubuntu en esa red.

## Instala ping si es necesario.

## Desde un contenedor intenta hacer:

ping otro_contenedor

## Pregunta
¿Los contenedores pueden comunicarse entre sí?

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
