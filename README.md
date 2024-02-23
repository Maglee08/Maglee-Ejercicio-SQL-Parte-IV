# Maglee Ejercicio SQL Parte IV
 
/*Ejercicio 4
Nivel de dificultad: Experto

1. Crea una tabla llamada "Pedidos" con las columnas: "id" (entero, clave
primaria), "id_usuario" (entero, clave foránea de la tabla "Usuarios") y
"id_producto" (entero, clave foránea de la tabla "Productos").*/


CREATE TABLE IF NOT EXISTS public. pedidos 
( id INT PRIMARY KEY, producto VARCHAR(50), 
usuario_id INT NOT NULL,
CONSTRAINT FK_usuario_id FOREIGN KEY (usuario_id) References usuarios(id)
 )

 /* ó */

 CREATE TABLE Pedidos (
    id SERIAL PRIMARY KEY,
    id_usuario INT REFERENCES Usuarios(id),
    id_producto INT REFERENCES Productos(id)
);

/* 2. Inserta al menos tres registros en la tabla "Pedidos" que relacionen usuarios con
productos.*/

INSERT INTO Pedidos (id_usuario, id_producto) VALUES (1, 1);
INSERT INTO Pedidos (id_usuario, id_producto) VALUES (2, 2);
INSERT INTO Pedidos (id_usuario, id_producto) VALUES (3, 3);

/* 3. Realiza una consulta que muestre los nombres de los usuarios y los nombres de
los productos que han comprado, incluidos aquellos que no han realizado
ningún pedido (utiliza LEFT JOIN y COALESCE).
*/

SELECT usuarios.nombre AS nombre, pedidos.producto AS producto
FROM  public.pedidos
LEFT JOIN public.usuarios
ON public.pedidos.id = public.pedidos.usuario_id;

/*4.Realiza una consulta que muestre los nombres de los usuarios que han
realizado un pedido, pero también los que no han realizado ningún pedido
(utiliza LEFT JOIN).*/


SELECT *
FROM  public.pedidos
LEFT JOIN public.usuarios
ON public.pedidos.id = public.pedidos.usuario_id
WHERE public.pedidos.cantidad = 1 

SELECT *
FROM  public.pedidos
LEFT JOIN public.usuarios
ON public.pedidos.id = public.pedidos.usuario_id
WHERE public.pedidos.cantidad = 0

/*Agrega una nueva columna llamada "cantidad" a la tabla "Pedidos" y actualiza
los registros existentes con un valor (utiliza ALTER TABLE y UPDATE)*/

/*Para agregar la columna cantidad*/

ALTER TABLE public.pedidos
ADD COLUMN cantidad INT

/* Usar UPDATE pata quitar la condición nula de columna cantidad*/

UPDATE public.pedidos
SET cantidad = '' 
WHERE cantidad IS NULL


ALTER TABLE public.pedidos
ALTER COLUMN cantidad SET NOT NULL


INSERT INTO public.pedidos ( id,producto, usuario_id,cantidad)
VALUES (1,'zapatos',1, 48);