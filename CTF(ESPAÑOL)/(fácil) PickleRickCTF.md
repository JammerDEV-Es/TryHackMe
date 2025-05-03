# TryHackMe - **Pickle Rick** CTF Tutorial
## Si estás buscando las respuestas están al final 
Este es un tutorial detallado del CTF **Pickle Rick** de TryHackMe. El objetivo de este CTF es ayudar a Rick a volver a ser humano encontrando tres ingredientes secretos. Este desafío es para principiantes y cubre la explotación web básica, comandos de Linux, y la escalada de privilegios.

---

# Pasos para completar el desafío

## **Paso 1: Reconocimiento Inicial**

1. **Acceder a la máquina:**
   - SSH en la máquina o utilizar el método de acceso proporcionado por TryHackMe.

2. **Escaneo de Puertos:**
   - La primera tarea es realizar un **escaneo de puertos** para descubrir los puertos y servicios abiertos en la máquina. Para ello podemos utilizar **nmap**:

   ```bash
 nmap -sC -sV -o PickleRickCTF -A MACHINE_IP
### Comprobar Servicios Disponibles

Después de ejecutar el escaneo, debería ver un servicio web ejecutándose en puertos como 80 u 8080. Abra su navegador y visite la dirección IP de la máquina:

  ```bash
 http://MACHINE_IP
 ```
Deberías ver una página con algunas pistas iniciales sobre los ingredientes secretos.

## Paso 2: Explorar el Servicio Web

### Inspeccionar el Servicio Web

Inspecciona la página viendo el código fuente. Puedes hacerlo pulsando Ctrl+U o haciendo clic con el botón derecho y seleccionando "Ver código fuente de la página". Busque comentarios o pistas ocultas que puedan apuntar a la ubicación de los ingredientes.

### Directorio Bruteforce (Usando Gobuster)

Haremos clic con el botón derecho del ratón en el espacio en blanco de la página y seleccionaremos «Ver fuente de la página». Una vez hecho esto, aparecerá un comentario en verde en la parte inferior que dice
```bash
 <!--

    Nota, ¡recuerda el nombre de usuario!

    Nombre de usuario: R1ckRul3s

  -->
```
![](https://github.com/JammerDEV-Es/TryHackMe/blob/main/CTF/Images/recorteusername.png)
Si no encuentras más información relevante directamente en la página, puedes usar Gobuster, es un poco lento de escanear pero ayuda a encontrar directorios y archivos ocultos.

pondrás esto en la consola
```bash
gobuster dir -u http://MACHINE-IP -w /usr/share/wordlists/dirb/common.txt
```
-u es para especificar el directorio y -w es para poner la lista de palabras

common.txt tiene 4615 palabras, estos son los directorios de la página: 
/.hta 
/.htaccess 
/.htpasswd 
/assets 
/index.html 
/robots.txt 
/server-status

![](https://github.com/JammerDEV-Es/TryHackMe/blob/main/CTF/Images/recortegobusteer.png)

Después de eso vamos a poner el robots.txt así http://MACHINE-IP/robots.txt y vamos a ver un texto simple en la pantalla que dice: Wubbalubbadubdub

Esta será la contraseña. Luego ponemos este https://MACHINE-IP/login.php y pondremos el nombre de usuario **R1ckRul3s** y la Contraseña **Wubbalubbadubdub**

## Paso 3 (Localizar el Primer Ingrediente) - Primera Pregunta: ¿Cuál es el primer ingrediente que Rick necesita?

Después de poner el nombre de usuario y la contraseña, usted debe encontrar el primer ingrediente en el en un archivo llamado `Sup3rS3cretPickl3Ingred.txt`. No puedes `cat` el archivo txt porque no eres capaz de hacer esto
entonces vas a poner `menos` es básicamente la misma función.
![](https://github.com/JammerDEV-Es/TryHackMe/blob/main/CTF/Images/recortelogin.png)

### Y EL PRIMER INGREDIENTE SERA: `mr. meeseek hair`
---
## Paso 4 (Localizar el Segundo Ingrediente) - Segunda Pregunta: ¿Cuál es el segundo ingrediente de la poción de Rick?


Haciendo `ls /home/` veremos una carpeta llamada `rick` así que ponemos lo mismo pero con rick `ls /home/rick`
![](https://github.com/JammerDEV-Es/TryHackMe/blob/main/CTF/Images/recortecommand.png)
Y aquí está el segundo ingrediente `menos /home/rick/"second ingredients`

### SEGUNDO INGREDIENTE ES: `1 jerry tear`
---
## Paso 5 (Localizar el tercer ingrediente) - Tercera pregunta: ¿Cuál es el último y definitivo ingrediente?

En este shell de comandos tenemos permiso `sudo`, así que vamos a poner 
```bash
sudo ls /root/
```
En `/root/` hay un .txt llamado `3rd.txt` así que vamos a poner esto en el shell de comandos `sudo less /root/3rd.txt`
![](https://github.com/JammerDEV-Es/TryHackMe/blob/main/CTF/Images/recorte3rd.png)
### Y EL TERCER INGREDIENTE ES: `fleeb juice`. 
---
![](https://github.com/JammerDEV-Es/TryHackMe/blob/main/CTF/Images/recortepicklerickallflag.png)

