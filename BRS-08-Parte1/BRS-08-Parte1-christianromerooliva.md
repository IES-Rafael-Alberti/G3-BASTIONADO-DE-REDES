# Hardening de Router Asus RT-AX88U
## Índice

- [Introducción](#introducción)
- [WPS](#wps)
- [Credenciales por defecto](#credenciales-por-defecto)
- [Red para invitados](#red-para-invitados)
- [Filtro WiFi por dirección MAC](#filtro-wifi-por-dirección-mac)
- [Método de autenticación WPA3 y contraseña WiFi robusta](#método-de-autenticación-wpa3-y-contraseña-wifi-robusta)
- [Ocultar SSID](#ocultar-ssid)
- [Establecer configuraciones de sistema](#establecer-configuraciones-de-sistema)
  - [Comprobar actualizaciones](#comprobar-actualizaciones)
- [Firewall](#firewall)
- [Ajustes adicionales de WiFi](#ajustes-adicionales-de-wifi)
- [Desactivar UPnP](#desactivar-upnp)
- [Realizar backup de la configuración](#realizar-backup-de-la-configuración)
- [DDNS](#ddns)
- [DNS](#dns)
- [Aplicación Android del Router](#aplicación-android-del-router)

### Introducción

En este documento vamos a definir una guía de hardening para el router Asus RT-AX88U. La guía consistirá en una serie de configuraciones de seguridad y medidas a tener en cuenta que pueden ayudar a fortalecer la seguridad del router Asus RT-AX88U y proteger la red doméstica o empresarial contra posibles amenazas cibernéticas. 

Estas medidas incluirán recomendaciones sobre la configuración de contraseñas sólidas y únicas, la configuración adecuada del firewall integrado para controlar el tráfico entrante y saliente, la desactivación de servicios y funciones innecesarias que puedan representar riesgos de seguridad, la habilitación del filtrado de direcciones MAC para limitar los dispositivos que pueden conectarse al router, entre otras prácticas recomendadas. 

La implementación de estas medidas de endurecimiento ayudará a mitigar los riesgos de seguridad y a mantener la integridad y confidencialidad de la red y los datos transmitidos a través del router Asus RT-AX88U.

### WPS

Por defecto la configuración WPS de este router viene activada, por lo que vamos a desactivarla. Para ello:
1. Nos vamos a **Advanced Settings** **(Configuración avanzada)** > **Wireless (Inalámbrico)** > ficha WPS
2. En el campo **Enable WPS** (Habilitar WPS), mueve el control deslizante a **OFF** (ACTIVAR).

![Pasted image 20240402010350.png](./img/Pasted%20image%2020240402010350.png)

### Credenciales por defecto

Deberemos de cambiar la contraseña por defecto al router, para ello nos vamos a 

1. **Advanced Settings (Configuración avanzada)** > **Administration (Administración)** > ficha **System (Sistema)**
2.  Aquí modificaremos la contraseña y usuario de inicio de sesión del router por unas credenciales personalizadas mucho más seguras:
![Pasted image 20240402010947.png](./img/Pasted%20image%2020240402010947.png)

### Red para invitados

A veces podemos tener invitados en casa o momentos en los que ceder nuestra red WiFi por algún motivo, para ello, mejor que dar acceso a nuestra red privada, utilizar una red de invitados. Podemos crearla de la siguiente manera:

Para crear una red para invitados:
1. En el panel de navegación, vaya a **General** > **Guest Network**
(Red para invitados).
2. En la pantalla Guest Network (Red para invitados), seleccione
la banda de frecuencia **2.4 GHz** o **5 GHz** para la red de invitados
que desee crear.
3. Haga clic en **Enable** (Habilitar).

![Pasted image 20240402104506.png](./img/Pasted%20image%2020240402104506.png)

### Filtro WiFi por dirección MAC

Podremos realizar una configuración para que únicamente ciertos dispositivos de nuestro hogar (ciertos portátiles, móviles personales...etc) sean capaz de conectarse a nuestra red WiFi. Para ello debemos habilitar un filtro MAC en la configuración de red inalámbrica.

Podemos seguir los siguientes pasos para activarla:

1. En el panel de navegación, vaya a **Advanced Settings** (Configuración avanzada) > **Wireless** (Inalámbrico) > ficha **Wireless MAC Filter** (Filtro MAC inalámbrico).
2. Seleccione Yes (Sí) en el campo Enable Mac Filter (Habilitar filtro Mac).
3. En la lista desplegable **MAC Filter Mode** (Modo de filtro MAC), seleccione **Accept** (Aceptar).
4. Seleccione **Accept** (Aceptar) para permitir que los dispositivos de la lista de filtros MAC accedan a la red inalámbrica.
5. En la lista de filtros MAC, haga clic en el botón **Add** (Agregar) y escriba la dirección MAC del dispositivo inalámbrico.
6. Haga clic en **Apply** (Aplicar).

![Pasted image 20240402012623.png](./img/Pasted%20image%2020240402012623.png)

### Método de autenticación WPA3 y contraseña WiFi robusta

Es interesante cambiar el método de autenticación de WPA2 a la última versión (reciente, de 2023) WPA3, el problema es que algunos dispositivos no podrán conectarse si la configuración es esta.

Una de las opciones que tenemos en este router, frente a no poder crear dos SSIDs distintas, es aprovechar que existen ajustes para la banda de 2.4GHz y 5GHz-1, y luego aparte de esos un ajuste que permite configurar una banda 5GHz-2 adicional en el que podremos utilizar WPA3 para probar si tenemos demasiados problemas con los dipositivos de nuestra casa. 
![Pasted image 20240402132229.png](./img/Pasted%20image%2020240402132229.png)
![Pasted image 20240402132237.png](./img/Pasted%20image%2020240402132237.png)

![Pasted image 20240402122720.png](./img/Pasted%20image%2020240402122720.png)

Establecemos también en esta sección también una contraseña robusta (recomendado mayor de 16 caracteres).

En cuanto a los ajustes de la red de 2.4GHz y 5GHz-1 utilizaremos WPA2-Enterprise, debido a que no es un decremento **tan inmenso** en seguridad y maximiza las opciones de compatibilidad. Además la versión *Enterprise* asegura que cada usuario tenga **su propio userid y contraseña**. Sin embargo, esta opción requiere de un servidor RADIUS que tendremos que configurar. Por suerte este modelo de router también trae una opción de configuración para añadirlo en la sección de configuración de WiFi:

![Pasted image 20240402133114.png](./img/Pasted%20image%2020240402133114.png)

![Pasted image 20240402133145.png](./img/Pasted%20image%2020240402133145.png)

### Ocultar SSID

El SSID es el identificador de la red, cada vez que un dispositivo haga un escaneo WiFi nuestra red aparecerá disponible si no está oculto. Por ello vamos a ocultarlo para que solo podamos conectarnos únicamente conociendo el SSID. Para ello:

1.  Vamos a **Advanced Settings** (Configuración avanzada) > **Wireless** (Inalámbrico)
2. Seleccionamos lo siguiente: ![Pasted image 20240402105812.png](./img/Pasted%20image%2020240402105812.png)

### Establecer configuraciones de sistema

En la sección **Advanced Settings** (Configuración avanzada) > **Administration** (Administración) > pestaña **System** (Sistema) y realizamos las siguientes configuraciones:

- Desactivar pantalla de alerta cuando se trata de acceder a la WAN. Esta pantalla podría dar información interesante para un atacante (si sale, es que está en el camino correcto).
- *AutoLogout* establecido en 30 minutos. Cuanto más tarde en desloguearse, más seguro será.
- Desactivar Telnet, protocolo obsoleto, inseguro y en desuso.
- Desactivar SSH
- Configurar el método de autenticación a HTTPS
- Cambiar el puerto TCP/IP a uno que solo nosotros conozcamos
- Desactivar acceso WAN, es decir restringir el acceso a LAN.
- Activar un Captcha en el Login
- Restringir el acceso a la WebUI a un único equipo que tengamos controlado.
  ![Pasted image 20240402120007.png](./img/Pasted%20image%2020240402120007.png)

![Pasted image 20240402115631.png](./img/Pasted%20image%2020240402115631.png)

#### Comprobar actualizaciones

En esta sección de sistema, podemos comprobar y actualizar la versión del Firmware:
![Pasted image 20240402120141.png](./img/Pasted%20image%2020240402120141.png)

Sin embargo, se desconoce como se descarga el firmware, si se realiza a través de SFTP HTTPs, FTPS u otro, y ASUS no provee información alguna sobre como se actualiza en sus sitios de soporte oficiales. Una de las pocas soluciones posibles para tener una respuesta a esto es analizar directamente el tráfico y conexiones e investigar si se trata de un servidor oficial de ASUS o socio oficial etc.

Según el mensaje de comprobación al menos, se indica que se comprueba el "ASUS Server", pero nada más:

![Pasted image 20240402124340.png](./img/Pasted%20image%2020240402124340.png)

Tampoco existe manera de comprobar si el firmware descargado se valida de alguna manera antes de instalarse, y comprobar esto requeriría de un proceso de investigación bastante amplio sobre como opera el propio router a nivel estructural.

En la [página oficial de soporte del modelo](https://www.asus.com/us/supportonly/rt-ax88u/helpdesk_download?model2Name=RT-AX88U) podremos encontrar drivers de restauración por si el proceso de actualización fuera mal, pero poca información más. 

Ante tantas dudas incluso puede resultar más seguro buscar información sobre la versión actual de firmware y conocerla antes que descargar una nueva.

### Firewall

Si existe algún **puerto WAN** permitido en el firewall, no debería haberlo si no es absolutamente necesario. Podremos realizar algunos ajustes adicionales en la sección de Firewall de este router:

- Desactivar respuesta ICMP a ping a través de la WAN
- Activar protección de DoS. No se especifica en la información que medidas se tomarán pero probablemente se realizarán alguna de las siguientes medidas:
	- Filtrado de paquetes
	- Reglas especiales
	- Monitorización de comportamiento anómalo
- Activar firewall para ipv6

![Pasted image 20240402121556.png](./img/Pasted%20image%2020240402121556.png)

### Ajustes adicionales de WiFi

Este modelo de router posee un botón para apagar el WiFi manualmente, se recomienda desactivarlo si no se está usando o en momentos puntuales como por ejemplo cuando nos vayamos de casa o por las noches incluso.

![Pasted image 20240402122033.png](./img/Pasted%20image%2020240402122033.png)
El botón **número 11** corresponde al interruptor de apagado/encendido WiFi.



### Desactivar UPnP

UPnP ( Universal Plug and Play ) nos permite en una red local descubrir y comunicarse entre sí de manera automática sin necesidad de intervención manual del usuario. UPnP puede abrir puertos en el router automáticamente para permitir el acceso remoto a ciertos servicios o dispositivos.

Esto supone un peligro en cuanto a términos de seguridad, por lo que simplemente lo desactivaremos y para ello:
1. Nos vamos a **Advanced Settings** (Configuración avanzada) > **WAN** y desactivamos la opción activar UPnP:
   ![Pasted image 20240402123450.png](./img/Pasted%20image%2020240402123450.png)

### Realizar backup de la configuración

El router nos permite en la sección  **Advanced Settings** (Configuración avanzada) > pestaña **Restore/Save/Upload Setting** encontraremos la siguiente opción para guardar la configuración del router actual.

![Pasted image 20240402124802.png](./img/Pasted%20image%2020240402124802.png)

### DDNS

A no ser que sea estrictamente necesario, el DDNS debería de estar desactivado. 

Si es necesario, el router proporciona sus propios servidores DDNS para configurarlo, además provee una opción de utilizar un certificado SSL gratuito por parte de *Let's Encrypt*, es ideal utilizar si optamos por activar esta opción:

![Pasted image 20240402125526.png](./img/Pasted%20image%2020240402125526.png)

### DNS

Este router no da información sobre que versión de DNS seguro posee, ni DoH (DNS over HTTPS) ni DoT (DNS over TLS). 

La única configuración que podemos establecer para IPv4 e IPv6 es no permitir que se conecte a los servidores DNS automáticamente, si no que configuremos manualmente los servidores DNS que tengamos fe en que sean seguros:

![Pasted image 20240402130012.png](./img/Pasted%20image%2020240402130012.png)

### Aplicación Android del Router

Este router posee una aplicación adicional para controlar el Router:

![Pasted image 20240402130705.png](./img/Pasted%20image%2020240402130705.png)

En cuanto a seguridad, lo mejor es quizá no utilizarla. Si se va a instalar, existen algunos permisos como el de ubicación que por algún motivo solicita al instalarse, no deberían de suministrarse en un principio. Parece conectarse únicamente a través de WiFi al router, no hay evidencia de otro tipo de conexión como bluetooth, HTTP o HTTPS. Lo ideal por supuesto, si se ha instalado, es mantenerse logueado únicamente cuando se vaya a utilizar, de lo contrario tendríamos un vector directo de acceso al router a través de nuestro dispositivo móvil.