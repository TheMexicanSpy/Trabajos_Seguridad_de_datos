# Reporte: Ejercicios de inyección de SQL

## ¿Qué son las inyecciones de SQL?

Se tratan de vulnerabilidades web que permiten a un atacante interferir con las consultas 
que alguna aplicación realize a una base de datos. La razón por la que son tan peligrosos es que a partir
de estas consultas se pueden obtener:
* Contraseñas
* Detalles de tarjetas de credito
* Información de usuarios
Estos simples ataques son capaces de desmantelar sistemas robustos y pueden causar mala reputación
y reparación de daños. <sub>Sin embargo vamos a ver como se hacen.....</sub>

## SQLi en cláusula WHERE para obtener datos ocultos
Imaginen que tenemos una página web de compras y queremos saber que productos existen en ella que no esten
en existencia, ya que asi podremos saber todos los productos que hay en la tienda. Cada vez que se busque en una categoría de productos
la página web realiza una consulta sql y esta se puede cambiar desde la url.

Primero usemos el caractér `'` para revisar si hay vulnerabilidad en la consulta. Al apretar `Enter` obtenemos lo siguiente.

![1 sqli](https://github.com/user-attachments/assets/d0d57356-9e75-4ceb-8081-df869286895e)

Como se observa la página nos arroja un error, por lo que podemos probar el siguiente paso de la inyección.

La instrucción a insertar a continuación es `+or+1=1--`.
* La parte `+or+1=1` es una condición concatenada que literalmente permitirá seleccionar todos los elementos donde la operación matemática sea verdad(prácticamente en todos los artículos).
* La parte `--` que es la instrucción para crear un comentario, por lo que las demás instrucciones serán ignoradas y la inyección será aplicada hasta antes de `--`.

Por lo tanto al insertar la instrucción completa y presonar enter en la url obtenemos lo siguiente:

![2 sqli](https://github.com/user-attachments/assets/61ea200e-75bf-42dc-b11d-61288ee9841e)

La consulta nos devuelve todos los productos disponibles y no disponibles registrados en la base de datos. Como se dijo antes, estos tipos de ataques parecen inofensivos, pero si el sistema es lo suficientemente vulnerable, estos datos de productos pueden ser datos bancarios o información gubernamental secreta....<sub>No antojen...</sub>

## Vulnerabilidad para saltar proceso de login
Si se quiere hacer login es necesario tener usuario y contraseña y la aplicación realizaría alguna consulta SQL tal como:
`SELECT firstname FROM users WHERE username='admin' and password='admin'`

Obvio si ponemos estas credenciales nos indica que son incorrectas.Sin embargo podemos insertar los caracteres `'` y `--` (comentario) para que se realize una consulta así:
`SELECT firstname FROM users WHERE username='administrator'--' and password='admin'`
Por lo que la consulta ignora la parte de la contraseña y solo ocuparemos el nombre de usuario para realizar el inicio de sesión.

![image](https://github.com/user-attachments/assets/7f5e0eb9-8015-4475-bff0-795dcdc92c2f)

![image](https://github.com/user-attachments/assets/e32b100a-0bed-4dc9-932d-e2bb7f59711c)
