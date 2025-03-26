# Tarea #974 Realizar una PoC de un elemento del OWASP TopTen - Misconfiguration PoC
### *Integrantes:*
<p>Ángel Briceño Córtez                 210300518
<p>Emmanuel García Peñaloza             200300595

## *Introducción*
Este reporte realiza un análisis de seguridad realizado sobre el firmware __IoTGoat-x86.img__, una imagen diseñada para pruebas de seguridad en dispositivos IoT. El objetivo principal es demostrar un flujo de trabajo común en la evaluación de la seguridad de firmware, que incluye la extracción del sistema de archivos, el análisis de archivos de configuración de usuarios y la realización de un ataque de fuerza bruta para obtener credenciales de acceso.

## *Procedimiento*

1. *Extracción del Sistema de Archivos*

El primer paso en el análisis de un sistema de este tipo es acceder a los archivos del sistema operativo contenidos dentro de la imagen del firmware. Para lograr esto, utilizamos herramientas que permiten descomprimir o extraer el contenido de la imagen del firmware. En este caso, se emplea la herramienta binwalk, que facilita la extracción del sistema de archivos comprimido dentro de la imagen del firmware. Al ejecutar la extracción, podemos explorar y analizar los archivos internos que componen el sistema.

*

    binwalk -e IoTGoat-x86.img

![1](https://github.com/user-attachments/assets/b7ad9dd0-3ecf-46f0-8c54-220a39b2885d) 

![2](https://github.com/user-attachments/assets/9fa1bca0-2c5e-4614-918d-fb9205b4d9d0)


El comando de extracción se ejecuta en el archivo de imagen IoTGoat-x86.img, lo que genera un directorio que contiene los datos descomprimidos llamado _IoTGoat-x86.img.extracted. Este paso es fundamental para poder manipular y observar los archivos relevantes del sistema operativo, como la configuración de los usuarios y contraseñas. Dentro de este directorio, se encuentra el sistema de archivos raíz, identificado como sasquashfs-root.
*
2. *Exploración del directorio extraído*

Una vez que la extracción ha finalizado, accedemos al directorio que contiene los archivos del sistema operativo descomprimido. En este punto, podemos inspeccionar archivos clave que almacenan información sobre los usuarios del sistema, como los archivos passwd y shadow.
El archivo passwd se encuentra en la ruta /etc/passwd dentro del sistema de archivos extraído. Este archivo contiene una lista de usuarios y el shell asignado a cada uno. Es importante señalar que los usuarios cuyo shell es /bin/ash son aquellos que tienen acceso a un entorno de comandos al iniciar sesión en el sistema. Para este análisis, nos enfocamos en el usuario llamado ‘iotgoatuser’, que es uno de los usuarios con un shell asignado.

*


    cat _IoTGoat-x86.img.extracted/squashfs-root/etc/passwd
                                             
![3](https://github.com/user-attachments/assets/d5cf004c-5d57-43a9-83c8-e2c150b8f945)


Por otro lado, el archivo shadow, ubicado en la ruta /etc/shadow, almacena las contraseñas de los usuarios en formato hasheado. El formato es generalmente ‘usuario:contraseña hasheada’, y en este caso obtenemos lo siguiente:

    iotgoatuser:9bz0K8z$Ii6Q/if83F1QodGmkb4Ah.

![4](https://github.com/user-attachments/assets/bf791aa9-bfde-4124-88cf-0ca111b77abc)

Estos carácteres parece que no dicen nada ya que se encuentran cifrados. Descifrarlos podría tomar mucho tiempo, el cuál no tenemos. 
*
3. *Proceso de descifrado del hash*

Para obtener la contraseña en texto claro, es necesario intentar descifrar el hash. Este proceso puede ser laborioso y demandar mucho tiempo, especialmente si el hash fue generado usando algoritmos de cifrado fuertes. Sin embargo, existen métodos y herramientas que permiten acelerar el proceso, como el uso de listas de contraseñas comunes que son probadas de manera automatizada.
En este escenario, se hace uso de una lista de contraseñas populares asociadas con la botnet Mirai con el archivo mirai-botnet_passwords.txt, que contiene combinaciones de contraseñas que han sido frecuentemente empleadas en ataques a dispositivos IoT.

*

    cat mirai-botnet-passwords.txt
![5](https://github.com/user-attachments/assets/cffc6d67-6e9e-4079-93d4-fb0d404af06b)



Con esto podremos usar alguna herramienta de fuerza bruta y por medio de esta lista probar todas las contraseñas con el usuario ‘iotgoatuser’.

*

4. *Fuerza bruta*

Una vez que tenemos la lista de contraseñas, utilizamos una herramienta de fuerza bruta para probar múltiples combinaciones de manera automática. En este caso, se emplea Medusa, una herramienta que permite probar contraseñas con diversos protocolos de acceso, como SSH. Medusa probará todas las contraseñas de la lista mirai-botnet_passwords.txt asociándolas con el usuario iotgoatuser en un servidor específico, que está accesible a través del protocolo SSH en el puerto 2222 de la dirección IP 172.18.0.2.
*
    medusa -u iotgoatuser -P mirai-botnet_passwords.txt -h 172.18.0.2 -M ssh -n 2222

![6](https://github.com/user-attachments/assets/f111b0d7-9d16-4d53-8f44-6dcabc379adc)



El proceso de fuerza bruta consiste en probar cada contraseña hasta encontrar una combinación válida. Finalmente, Medusa indica que la combinación exitosa para el usuario iotgoatuser es la contraseña ‘7ujMko0vizxv’.
*

5. *Prueba*

El último paso que queda es probar que la contraseña obtenida mediante fuerza bruta es la correcta. 

![7](https://github.com/user-attachments/assets/4886efac-c466-45ad-a38b-fb9ed2fa4c08)


Se ha completado la PoC y ahora tenemos acceso al sistema.

## *Conclusión*

Este proceso ilustra cómo es posible acceder a sistemas a través de la extracción de archivos del firmware, seguido de la exploración de los archivos clave que contienen información de usuarios y contraseñas. Mediante el uso de herramientas de descifrado y fuerza bruta, logramos obtener una contraseña en texto claro que nos permite acceder al sistema. Este enfoque resalta la importancia de proteger adecuadamente las contraseñas y adoptar mecanismos de seguridad robustos en dispositivos IoT, ya que muchos de ellos presentan vulnerabilidades fácilmente explotables mediante estos métodos. Por ejemplo la doble autenticación es un buen método para proteger nuestros sistemas evitando penetraciones no deseadas.
