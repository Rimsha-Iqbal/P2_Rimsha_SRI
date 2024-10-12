# Índice

- [Índice](#índice)
- [Práctica 2](#práctica-2)
    - [Autor: Rimsha](#autor-rimsha)
    - [Fecha: 10-10-2024](#fecha-10-10-2024)
  - [Instalación y configuración de un servidor DHCP en Debian](#instalación-y-configuración-de-un-servidor-dhcp-en-debian)
    - [Plan de trabajo](#plan-de-trabajo)
    - [**Configuración de pfSense**](#configuración-de-pfsense)
    - [**Configuración de Debian 12 DHCP Server**](#configuración-de-debian-12-dhcp-server)
    - [**Configuración de Ubuntu**](#configuración-de-ubuntu)
    - [**Configuraciones en Windows 10**](#configuraciones-en-windows-10)
    - [Ejercicio 1. Configuración del servidor DHCP](#ejercicio-1-configuración-del-servidor-dhcp)
    - [Respecto a los tiempos de alquiler:](#respecto-a-los-tiempos-de-alquiler)
    - [Ejercicio 2. Configuración de los clientes DHCP.](#ejercicio-2-configuración-de-los-clientes-dhcp)
    - [Ejercicio 3. Funcionamiento del servicio.](#ejercicio-3-funcionamiento-del-servicio)


# Práctica 2 
### Autor: Rimsha
### Fecha: 10-10-2024 

## Instalación y configuración de un servidor DHCP en Debian   

### Plan de trabajo
En esta práctica vamos a implementar una red de acuerdo con el siguiente diagrama:

![diagrama](img/diagrama.png)  

Vamos a instalar y configurar un **servidor DHCP** en **Debian** con dos clientes, uno **Windows** y otro **Linux**.  

![maquinas](img/maquinas.png)

Las tres máquinas, el **servidor Debian**, el cliente con **Windows** y el **cliente Ubuntu**, estarán en la misma subred privada interna **SRI214**, con dirección de red **10.0.214.0/24**. Las máquinas estarán conectadas a Internet a través de un router **pfSense**.  

1. Configurar las máquinas indicadas en la topología de red que aparece en la imagen superior, asignar manualmente las direcciones IP indicadas a los dispositivos correspondientes, y cambiar los nombres de las computadoras como se indica en el diagrama.  

### **Configuración de pfSense**    
Vamos a la opción 2 para el cambio de IPs.  

![alt text](img/img1.png)  

Seleccionamos opción 2 para hacer cambios de LAN.  

![alt text](img/img2.png)  

Ponemos **n** porque no queremos configuraciones DHCP.  

![alt text](img/img3.png)  

Entramos nuestra IP: **10.0.214.1** para LAN interna.  

![alt text](img/img4.png)    

Elegimos la máscara de red **/24**.  

![alt text](img/img5.png)  

No queremos cambiar nada de WAN, así que pulsamos **ENTER**.  

![alt text](img/img6.png)    

No ponemos nada para IP de versión 6.  

![alt text](img/img7.png)  

No queremos DHCP, así que ponemos **n**.  

![alt text](img/img8.png)   

Ya está nuestra IP de LAN interna configurada.  

![alt text](img/img9.png)  

### **Configuración de Debian 12 DHCP Server**    
Con `nano`, abrimos el fichero de interfaces en el directorio `network`.  

![alt text](img/img10.png)    

Aquí ponemos **IP, Máscara de red, Puerta de enlace, Servidor DNS y nombre de DNS** que queremos poner a nuestro servidor Debian.  

![alt text](img/img12.png)   

Guardamos y reiniciamos los cambios.  

![alt text](img/img13.png)  

Comprobamos si los parámetros están configurados o no.  

![alt text](img/img14.png)    

Cambio de nombre en Debian.  

![alt text](img/img15.png)   

![alt text](img/img16.png)  

Comprobamos con `cat`.  

![alt text](img/img17.png)  

### **Configuración de Ubuntu**  
Iniciamos como admin para no tener que usar `sudo` antes de cada comando.  

![alt text](img/img18.png)  

Abrimos el fichero de configuración con `nano`.  

![alt text](img/img19.png)     

Captura antes de la configuración.  

![alt text](img/img20.png)    

Ponemos 3 líneas: 2 para el adaptador que vamos a usar y una para habilitar DHCP.  

![alt text](img/img21.png)    

Aplicamos los cambios.  

![alt text](img/img22.png)   

Comprobamos si los cambios están bien o no.  

![alt text](img/img23.png)   

Nombre de mi máquina.  

![alt text](img/img24.png)     

### **Configuraciones en Windows 10**   
Cambiamos el nombre de mi equipo.  

![alt text](img/img25.png)     

Y pongo mi nombre.  

![alt text](img/img26.png)  

Habilitamos servicios de DHCP en el cliente Windows.  

![alt text](img/img27.png)  

### Ejercicio 1. Configuración del servidor DHCP    
Instala el servidor DHCP en la máquina correspondiente.  
Actualizamos los paquetes.  

![alt text](img/img29.png)  

Instalamos el paquete del servidor DHCP.  

![alt text](img/img30.png)   

Vamos al directorio de DHCP.  

![alt text](img/img31.png)  

Listamos su contenido.  

![alt text](img/img32.png)  

![alt text](img/img33.png)  

![alt text](img/img34.png)  

Realizamos las configuraciones adicionales necesarias para que funcione el servidor DHCP.  
Vamos a abrir el archivo del servidor.  

![alt text](img/img35.png)  
    
Aquí ponemos nuestra interfaz de red que vamos a usar.  

Antes de cambios:   

![alt text](img/img36.png)  

Después de cambios:  

![alt text](img/img37.png)    

Realizamos las configuraciones necesarias para cumplir los siguientes requisitos:   

Antes de nada, realizamos un backup/copia del archivo original.  

![alt text](img/img38.png)      

Abrimos el fichero de configuración.  

![alt text](img/img39.png)   

Antes de configuración:  

![alt text](img/img40.png)    

El servidor repartirá direcciones IP en el rango **10.0.XX.1 – 10.0.XX.100**.  

![alt text](img/img41.png)  

Utilizamos la máscara por defecto correspondiente a esa subred.   

![alt text](img/img42.png)  

Ponemos como puerta de enlace la que corresponda según el diagrama de red.  

![alt text](img/img43.png)    

Como servidor DNS, ponemos el del instituto.  

![alt text](img/img44.png)  

Ponemos el sufijo DNS `sri214.local`.  
![alt text](img/img45.png)   

Para el cliente Ubuntu, se le reservará la dirección **10.0.214.60**.   

Antes de configuraciones:  
![alt text](img/img46.png)    

MAC de Ubuntu para confirmar que está en el mismo.  

![alt text](img/img47.png)  

Después de configuraciones:  

![alt text](img/img48.png)  

### Respecto a los tiempos de alquiler:  
El tiempo de alquiler por defecto será de **15 días** para todos los equipos. 

![alt text](img/img49.png)   

Nunca será superior a **30 días**.  

![alt text](img/img50.png)   

Nunca será inferior a **1 semana**. 

![alt text](img/img51.png)   

Cambios completos. 

![alt text](img/img52.png)   

Reiniciación del servicio y verificación de que tras el reinicio está activo y en ejecución.   

![alt text](img/img53.png)   

### Ejercicio 2. Configuración de los clientes DHCP. 
Configura los equipos Windows y Linux como clientes DHCP.   
Habilitamos el servicio DHCP.  

![alt text](img/img54.png)   

Vamos a renovar los parámetros. 
     
![alt text](img/img55.png)   

Los parámetros ya están cambiados correctamente.  

![alt text](img/img56.png)  

Observación dentro del archivo adecuado del servidor si las IPs han sido asignadas en Debian.  

![alt text](img/img57.png) 

* Observación dentro de ambos clientes que son correctos todos los parámetros enviados por el servidor.  
   1. IP 
   2. Máscara  
   3. Puerta de enlace   
   4. DNS 
   5. Nombre de dominio
   6. La MAC del equipo que tiene la reserva
  
En Windows:  

![alt text](img/img58.png)  

En Ubuntu:   
IP y Máscara:  
![alt text](img/img59.png)     

Puerta de enlace:  
![alt text](img/img61.png)   

DNS por defecto:    
![alt text](img/img62.png)  

Nombre de dominio:  
![alt text](img/img63.png)  

DNS por defecto:   
![alt text](img/img64.png)   

DNS después de cambiar:  
![alt text](img/img65.png)   

La MAC del equipo que tiene la reserva.  
![alt text](img/img66.png)  

Verificación de que existe conectividad entre los equipos y que además ambos equipos se conectan a Internet.  

![alt text](img/img67.png)  
![alt text](img/img68.png)  
![alt text](img/img69.png) 
![alt text](img/img70.png)   

### Ejercicio 3. Funcionamiento del servicio. 
Para terminar, deberás explicar la actividad generada por el servidor **isc-dhcp-server** que has instalado y configurado y que se ha registrado en los logs del sistema por la herramienta **journalctl**.  

![alt text](img/img71.png)  

* Aplica el tipo de filtro adecuado para que solo se muestre la actividad concreta relativa a la asignación de la configuración de tu cliente en un determinado intervalo de tiempo.  

![alt text](img/img72.png)  
