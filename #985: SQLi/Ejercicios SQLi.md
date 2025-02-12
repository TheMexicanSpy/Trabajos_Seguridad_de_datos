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
