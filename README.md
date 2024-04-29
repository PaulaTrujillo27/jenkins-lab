# Paso a paso Jenkins Lab

Para comenzar, es necesario asegurarse tener docker compose instalado en nuestras máquinas. Una vez hecho lo anterior, se debe asegurar que nuestro docker-compose.yml cuente con la siguiente estructura:

```
version: '3.7'

services:
  jenkins:
    image: jenkins/jenkins:lts
    ports:
      - "8080:8080"
      - "3000:3000"
    volumes:
      - jenkins_patm:/var/jenkins_home

volumes:
  jenkins_patm:
    name: jenkins_patm
```
## Ejecutar Docker Compose

Luego, para ejecutar nuestro docker-compose.yml se utiliza el siguiente comando, en la ubicación donde se encuentra nuestro archivo:

```
docker-compose up -d
```
![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/279108c5-6564-4a9a-a72d-a60ff8dd6dd2)

Se verifica el estado del contenedor usando el comando:

```
docker ps
```
![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/3be5cd53-dfbb-4b39-99e3-ba3a431c8b65)

Por otro lado, en nuestro Docker Desktop podemos ver el volúmen ya creado:

![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/bf70f3f7-9f46-4be4-b670-b14e90154eb5)

## Extraer las password

Se ejecuta el siguiente comando:

```
docker exec id_container cat /var/jenkins_home/secrets/initialAdminPassword
```
Y con este conseguimos la contaseña:

![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/f578335f-9f53-416a-9de3-0f176fbed09c)

## Iniciar Jenkins

Luego de haber conseguido nuestra contraseña, ingresamos al `localhost:8080` como administrador e ingresamos la contraseña obtenida anteriormente:

![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/ac37f57c-e7cc-48dd-86ff-fa01d090cc12)

Después, elegimos el tipo de instalación de Jenkins, seleccionamos el onboarding para seleccionar los plugins o extensiones a instalar.


![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/d155b43a-d0ed-4d83-97c0-3ddafff42cdb)

Ahora, se selecciona Node.js en la lista de plugins a instalar, luego se iniciará la descarga de los plugins y sus dependencias:

![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/c74eb670-77ae-4a40-8301-5e133afff6c0)

![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/3b90bf00-148f-4043-ba65-8bb7814ec967)

Posterior a ello, crearemos el usuario administrador de Jenkins:

![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/9a0d42eb-6c7c-4c11-a1c6-100d2a1550dd)

Finalmente, nos encontramos con el panel de control de Jenkins. Aquí administraremos los proyectos de integración continua a desarrollar:

![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/548a9218-4265-4962-aad5-c61939e3e2d1)

## Configuraciones en Jenkins

En este punto, realizaremos las configuraciones de Jenkins necesarias:

1. Ingresar a Administrar Jenkins
2. Tools
3. Bajamos hasta las instalaciones de NodeJS
4. Nombramos la nueva instalación y elegimos nuestra versión de Node JS:

![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/c5b0a54e-90ff-4334-b3e8-ed970ae1fc17)

## Crear nuestra primera tarea

Para crear nuestro primero Pipeline debemos hacer lo siguiente:

1. Nueva tarea
2. Nombramos nuestro Pipeline
3. Creamos un proyecto de: Estilo Libre

Después de lo anterior, se debe configurar la conexión con el repositorio en GitHub, el ambiente de ejecución del Jenkins y los pasos del pipeline. Para esto, realizamos unas configuraciones que se verán en las siguientes imágenes:

### Conexión con Git

![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/9484972c-1762-4e7f-bf9f-8f02628d3073)

### Configurar nuestro ambiente de ejecución

![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/45cdf684-cd36-48f2-b021-6e59b263e7c4)

### Pasos de compilación

Se agrega un nuevo Paso de Compilación y en el menu desplegable se selecciona:Ejecutar Script de Shell y se agregan los siguientes comandos para su ejecución:

![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/1c54a05f-5e72-47ab-90f4-01f5f4752687)

## Ejecución del Pipeline

Para finalizar con nuestro proceso, correremos el pipeline. Para esto, damos click en el botón de ejecutar. Para revisar el status de la ejecución, damos click en el apartado de "Estado del ejecutor de construcciones". Aquí podemos tener una visualización del estado:


![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/abf922d8-fd68-4658-9151-3bde56d381d8)

Para abrir la app en el navegador, accedemos a Console Output y accesamos a la URL que nos da:

![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/b2d4cc8a-e677-40c3-a882-fb025b21ded4)

Al accesar a la IP del Servidor podemos ver la aplicación corriendo satisfactoriamente:

![image](https://github.com/PaulaTrujillo27/jenkins-lab/assets/71205932/3d984e90-a8ab-4bb9-b0e3-95fe5a65eefd)


























