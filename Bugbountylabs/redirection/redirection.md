Máquina: [Redirection](https://bugbountylabs.com/)

Autor: El Pinguino de Mario & Curiosidades De Hackers

Dificultad: Principiante

![image](images/Redirection.PNG)

## Despliegue

Nos descargamos el archivo .zip que contiene el auto_deploy, lo descomprimimos y ejecutamos el .py como **sudo**

![image](images/despliegue.PNG)


## Reconocimiento

Cuando la tengamos desplegada podemos ver la conectividad con ```ping -c 1 172.17.0.2``` 
<br>
con el parámetro `-c` hacemos que el ping solo se haga una vez<br>
<br>


Una vez que tengamos conectividad con la máquina usamos nmap ```nmap -p- --open -sS -sC -sV --min-rate 3000 -n -vvv -Pn 172.17.0.2``` <br>
`-p-` ⮞ comprueba todos los puertos <br>
`--open` ⮞ analiza en profundidad solo a los que esten abiertos <br>
`-sS` ⮞ para descubrir puertos de manera silenciosa y rápida <br> 
`-sC` ⮞ ejecuta los scripts de reconocimiento básico, los más comunes <br> 
`-sV` ⮞ para conocer la versión del servicio que corre por el puerto
`--min-rate 3000` ⮞ para enviar paquetes más rápido <br> 
`-n` ⮞ no aplica la resolución DNS (tarda mucho en el caso de que no pongamos dicho parámetro)<br> 
`-vvv` ⮞ cuando descubre un puerto nos lo muestra por pantalla <br> 
`-Pn` ⮞ ignora si esta activa o no la IP<br> 
<br>

Al aplicar el escaneo, vemos que el puerto 80 está abierto
<br>

![image](images/nmap.PNG)
<br>

## Apache (Puerto 80)

Al ser una máquina enfocada al bug bounty, lo normal es solo encontrar el puerto 80 que corresponde al servidor web. Al buscar 172.17.0.2 nos encontramos con esto

![image](images/inicio.PNG)


Aquí podemos observar tres laboratorios para practicar open-redirect, para el que no sepa lo que es un open-redirect, este es una vulnerabilidad en una web que permite redirigir a los usuarios a una página externa modificando la url.


## Laboratorio 1

En este laboratorio podemos observar un botón que si lo presionamos nos redirige a google

![image](images/laboratorio1.PNG)

Si miramos el código fuente de la página nos encontramos con esta parte que maneja la redirección

![image](images/enlace1.PNG)


Viendo esto, podemos probar a cambiar la url a la que nos redirige el botón a por ejemplo `dockerlabs.es`. Con lo cual nos quedaría así ![image](images/url1.PNG)

Tendiendo esta url, al presionar ENTER podemos comprobar que si que funciona, redirigiéndonos a `dockerlabs.es`

![image](images/dockerlabs.PNG)


## Laboratorio 2

En este laboratorio también podemos observar un botón que si lo presionamos nos redirige a google

![image](images/laboratorio2.PNG)

Si miramos el código fuente el código de redirección es el mismo, pero si probamos el mismo método vemos que no funcionará

![image](images/error1.PNG)
