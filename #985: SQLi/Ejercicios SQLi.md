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

Primero usemos el caractér ´'´ para revisar si hay vulnerabilidad en la consulta. Al apretar ´Enter´ obtenemos lo siguiente.
