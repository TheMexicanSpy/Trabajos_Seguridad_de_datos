# Hardening de CentOS7 con Wazuh
***
## Preparación del entorno
Tenemos una CentOS 7 en máquina virtual, así como una máquina virtual de Amazon Linux preconfigurada
con un Wazuh-Manager, que nos permite acceder al Dashboard desde un navegador Web.

![image](https://github.com/user-attachments/assets/62b2872b-c2c6-4264-b816-6cd54252c196)

![image](https://github.com/user-attachments/assets/02f3438e-18f2-414a-ba5b-a52ea6369991)

Hay que mencionar que CentOS 7 ya ha sido descontinuado y que, muchas de las 
funciones del instalador de paquetes `yum` y sus mirrors ya no sirven, lo cuál hacen el hardening más complicado de lo que es.
***
## Verificando configuración del sistema
En un entorno recién instalado, junto con su configuración básica del CentOS 7, el 
compliance abarcaba el 20% aproximadamente.  

En este momento después de varios scripts encontrados por varias fuentes, el sistema se encuentra con una calificación del 46%

![image](https://github.com/user-attachments/assets/976c67dd-ccfc-4ace-8c14-1376dcc62477)

