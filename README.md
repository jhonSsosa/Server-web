# Proyecto: Framework Web Concurrente

## Descripción
Este proyecto implementa un framework web ligero y concurrente que permite manejar múltiples solicitudes HTTP en paralelo. Incluye una arquitectura basada en un servidor concurrente con `ExecutorService` para manejar múltiples clientes de manera eficiente y un controlador REST básico que responde a peticiones HTTP.

## Arquitectura
El framework sigue una arquitectura basada en sockets:
- **`RestServiceApplication`**: Clase principal que inicia el servidor y maneja múltiples conexiones concurrentes usando un `ThreadPool`.
- **`HelloRestController`**: Controlador que procesa las solicitudes y devuelve respuestas HTTP.

### Diseño de Clases
1. `RestServiceApplication`
    - Inicia un `ServerSocket` en el puerto 5000.
    - Usa un `ThreadPool` de hasta 10 hilos para manejar conexiones concurrentes.
    - Implementa un mecanismo de apagado elegante para cerrar las conexiones activas.
2. `HelloRestController`
    - Maneja solicitudes HTTP en hilos separados.
    - Simula una solicitud lenta de 5 segundos antes de responder.

## Generar la Imagen Docker
Para empaquetar y ejecutar el servicio en un contenedor Docker, sigue estos pasos:

### 1. Construcción de la imagen
```sh
docker build -t jhonssosa/lab04 .
```

### 2. Verificación de la imagen creada
```sh
docker images
```

### 3. Subir la imagen a Docker Hub
```sh
docker login
# Etiquetar la imagen
 docker tag jhonssosa/lab04 jhonssosa/lab04:latest
# Subirla
 docker push jhonssosa/lab04:latest
```

## Despliegue en AWS
### 1. Acceder a la instancia EC2 y configurar Docker
```sh
sudo yum update -y
sudo yum install docker -y
sudo service docker start
sudo usermod -aG docker ec2-user
logout
```
### 2. Descargar y ejecutar la imagen desde Docker Hub
```sh
docker pull jhonssosa/lab04:latest
docker run -d -p 42000:5000 --name restserver jhonssosa/lab04:latest
```

### 3. Verificar el servicio
Abrir en un navegador o usar `curl`:
```sh
curl http://ec2-18-189-178-147.us-east-2.compute.amazonaws.com:42000/greeting
```

## Imágenes del Despliegue
![Ejecución en local](imagenes/local.png)
![Despliegue en AWS](imagenes/aws.png)

