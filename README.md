# MongoDB-Docker-Basic
![MongoDB-DockerImage](https://media.licdn.com/dms/image/C5612AQENOC_bFx1Scg/article-cover_image-shrink_600_2000/0/1599320945318?e=2147483647&v=beta&t=Hj5K3tLMhvguYziWrDZ-ckB-zceTHkBSxLNBKr1LqaY)

En este repositorio te vamos a enseñar cómo instalar MongoDB en un contenedor de Docker con una configuración básica.
El documento docker-compose.yml crea contenedores. Tiene comandos para crear como 3 contenedores. Toma imagenes para crear esos contenedores. Las imagenes las saca de dockerHub

## Instalación

#### Paso 1: Crear documento de docker-compose. Para crear el archivo docker-compose.yml, tienes dos opciones:

- Opción 1: Utilizar Docker Compose en Visual Studio Code instalando la extensión de Docker.

- Opción 2: En la línea de comando, ejecutar:
  ```
  touch docker-compose.yml
  cat > docker-compose.yml
  ```
#### Paso 2: Ahora, editaremos el archivo docker-compose.yml para configurar nuestro servicio de MongoDB. Asegúrate de reemplazar "user" y "pass" con el usuario y la contraseña deseados,al terminar de copiar aprtete un enter y ctr + d para grabar y continuar.
```
version: '2.2'
services:

  mongo:
    image: mongo:4.0.4
    restart: always
    container_name: monguito
    environment:
      - MONGODB_USER="user"
      - MONGODB_PASS="pass"	
      
    volumes:
      - ./monguitodata:/data/db
      - ./monguitodata/log:/var/log/mongodb/
    ports:
      - "27017:27017"
```
Explicación de cada línea
- version del docker compose
- el servico que queremos configurar en este caso mongo
- nombre del servicio
- indica que estamos utilizando la imagen oficial de MongoDB versión 4.0.4
- asegura que el contenedor se reinicie automáticamente si se detiene
- nombre del cointainer
- entorno, se configura el nombre y contraseña para el usuario raiz
- me permite mapear el almacenamiento del contenedor en este caso los dos que contiene
- puerto que permite acceder a la base de datos MongoDB desde fuera del contenedor.
En resumen todo este comando crea el contenedor con usuario y contraseña, monta los volumenes locales para los datos y los registros y expone en puerto 27017 para acceder a la base de datos.


#### Paso 4: Presiona CTRL+D

#### Paso 5: Crea un archivo para ejecutar comandos en la terminal 
```
touch mongo.sh
```

#### Paso 6: Completa el archivo 'mongo.sh' con los siguientes comandos:
```
cat > mongo.sh

# Crear carpeta para volumen de mongo:
mkdir monguitodata && cd monguitodata; cd monguitodata || mkdir log

cd ~

# Iniciar el contenedor:
sudo docker-compose up -d

# Mostrar mensaje:
echo "Monguito está iniciandose ......."

# Entrar en el contenedor
sudo docker exec -it monguito bash
```

#### Paso 7: Presiona CTRL+D

#### Paso 8: Asigna permisos de ejecución y ejecuta 'mongo.sh':
```
chmod u+x mongo.sh
./mongo.sh
```

## ¡Listo! Ya has instalado MongoDB con éxito. 

### Continuemos con algunos comandos básicos:

**Mostrar Bases de datos:**
```
> show dbs
```

**Crear o ubicarse en una base de datos:**
```
> use databasename
```

**Saber qué base de datos estamos usando:**
```
> db
```

**Crear colección:**
```
> db.createCollection('nameCollection')
{"Clave": "Valor"}
```

**Mostrar el contenido de una colección:**
```
> showCollections
```
