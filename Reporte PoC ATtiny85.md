# Reporte de Creación de Clúster de base de datos y pruebas con Sysbench
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

