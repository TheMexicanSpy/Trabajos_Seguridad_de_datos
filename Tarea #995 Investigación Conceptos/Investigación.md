# Reporte: Conceptos básicos de Seguridad de Datos
En este reporte sa abarcarán algunos de los conceptos fundamentales dentro de la seguridad de datos.

## ¿Qué es la triada CIA?
Se trata de *Confidentiality*, *Integrity* y *Availability*, que es un modelo fundamental que define los pilares de la protección de la información:

* La **confidencialidad** garantiza que la información solo sea accesible para aquellos con autorización.
* La **integridad** se refiere a que los datos no sean alterados de maneras inesperadas.
* Y la **disponibilidad** garantiza que los datos y los recursos sean siempre accesibles cuando se necesiten.

![image](https://github.com/user-attachments/assets/93def860-238f-43ce-8dbc-a439d33c1a7a)

Con esto se tiene un sistema completo e integral en el cual empresas u personas puedan confiar sus preciados recursos y su dinero.
***
## El triangulo de Usabilidad
Para obtener un sistema seguro es necesario tener en cuenta 3 cosas clave:

1. **Seguridad**: Aquella capacidad para proteger los datos
2. **Usabilidad**: Es la facilidad con la que los usuarios pueden usar el sistema
3. **Funcionalidad**: Son las características y funcionalidades del sistema.

![image](https://github.com/user-attachments/assets/c02d9242-e884-4277-a800-29e04007b41c)

A diferencia de la triada CIA, el triángulo de usabilidad es un enfoque donde se debe equilibrar el uso de estos 3 elemntos; enfocarse demasiado en seguridad solo complica de más la experiencia de los usuarios, o si tienes un sistema con capcaidades extraordinarias pero poca seguridad, corres el riesgo de que te roben tus ideas y tus datos.
***
## El Riesgo

Bajo el contexto de seguridad de datos, el **riesgo** se refiere a la posibilidad de que una amenaza pueda aprovecharse de una vulnerabilidad, y así causar algún impacto negativo. Existen varias formas de calcular riesgos, pero la más simple puede verse tal que así:

$Riesgo = Amenaza × Vulnerabilidad × Impacto$

### Las amenazas
Se trata de aquél evento o acción que tiene el potencial de causar daños a un sistema o a la información que este contenga. Estas amenazas pueden ser:

* **Intencionales**
* **No intencionales**

### Las vulnerabilidades
Estas son debilidades o fallos que se encuentren en un sistema y que pueden ser explotadas por una amenaza para causar daño. Estos errores pueden ser:

* **Errores de software**
* **Malas configuraciones**
* **Falta de actualizaciones o mantenimiento**

### El Impacto
Se le puede decir impacto a todo efecto negativo que resulte en la ponderación de un riesgo. Estos efectos pueden tambien considerarse como las consecuancias de que una vulnerabilidad sea explotada dentro de tu sistema, tales como:

* **Pérdida de clientes**
* **Multas gubernamentales**
* **La reputación de una organización**
***
## ¿De qué se trata el MFA?
Del inglés *Multi Factor Authentication*, se trata de un método de seguridad en el que se requiere que un usuario proporcione 2 o más factores de autenticación pra acceder a un sistema. Se trata de un método que muchas empresas y aplicaciones an implementado recientemente, pues acceder a tu *Facebook* con tu contraseña era muy fácil, ahora para iniciar sesión debes estar en las mismas coordenadas donde se haga el inicio de sesión, por ejemplo.

![image](https://github.com/user-attachments/assets/299be069-be19-42c9-984c-e34a56106371)

Algunos de los factores para pasar la prueba MFA pueden ser:

* **Algo que tu sepas**: Una contraseña o un *PIN*.
* **Algo que tengas**: Un token móvil o un código que la aplicación envie a tu dispositivo personal.
* **Algo que tu seas**: Una huella digital, un escanéo facial, entre otros.
***
## Referencias bibliográficas

*Team, S. (2024, December 13). What is the CIA triad in cyber security? StationX. https://www.stationx.net/what-is-the-cia-triad/*

*Cercado, C. (2015, July 31). La funcionalidad, la usabilidad y la seguridad en el desarrollo de Software. Cultura Informatica. https://culturatics.wordpress.com/2015/07/26/la-funcionalidad-la-usabilidad-y-la-seguridad-en-el-desarrollo-de-software/*

*Initialize, N. (2024, April 16). Cálculos de Análisis de Riesgos: 7 Formas de Determinar Puntuaciones de Riesgo de Ciberseguridad. Secureframe. https://secureframe.com/es-es/blog/risk-analysis-calculation*

*Mehta, J. (2024, April 5). What is a Multi-Factor Authentication (MFA)? Difference between 2FA & MFA. EncryptedFence by Certera - Web & Cyber Security Blog. https://certera.com/blog/what-is-multi-factor-authentication-difference-between-2fa-mfa/*
