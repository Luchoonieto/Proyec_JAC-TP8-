# Proyec_JAC-TP8-


-consultas:



- Consulta 1: Listar todos los datos de los clientes registrados.

SELECT * FROM cliente;


- Consulta 2: Listar todos los productos del inventario cuyo precio sea menor a $20000.00.

SELECT ID_producto, Tipo_producto, Nom_pedido, Precio_producto, Lanza_producto 
FROM Producto 
WHERE Precio_producto < 20000.00;

- Consulta 3 : Listar todos los juegos registrados ordenados por su precio de mayor a menor.

SELECT Nom_pedido AS Juego, Precio_producto, Lanza_producto 
FROM Producto 
WHERE Tipo_producto = 'Juego'
ORDER BY Precio_producto DESC;


- Consulta 4: Consultar todos los juegos junto con su desarrollador correspondiente.

SELECT p.Nom_pedido AS Juego, d.Nom_desarrollador, d.Apelli_desarrollador
FROM Producto p
JOIN juego j ON p.ID_producto = j.ID_producto
JOIN juego_desarrollador jd ON j.ID_juego = jd.ID_juego
JOIN desarrollador d ON jd.ID_desarrollador = d.ID_desarrollador;

- Consulta 5 (Con JOIN múltiple): Consultar qué plataformas soporta cada juego registrado.

SELECT p.Nom_pedido AS Juego, pl.Tipo_plataforma AS Plataforma
FROM Producto p
JOIN juego j ON p.ID_producto = j.ID_producto
JOIN juego_plataforma jp ON j.ID_juego = jp.ID_juego
JOIN plataforma pl ON jp.ID_plataforma = pl.ID_plataforma;

- Consulta 6 (Con JOIN múltiple): Consultar todos los pedidos realizados, 
-- mostrando el ID del pedido, la fecha, el cliente y el método de pago.

SELECT ped.ID_pedido, ped.Fecha_pedido, c.Nom_cliente, c.Apelli_cliente, pg.Tipo_pago
FROM pedido ped
JOIN cliente c ON ped.ID_cliente = c.ID_cliente
JOIN pago pg ON ped.ID_pago = pg.ID_pago;

- Consulta 7 (Con JOIN y detalle): Consultar el detalle completo de los juegos comprados en cada pedido (nombre del juego, cantidad y precio).

SELECT ped.ID_pedido, pr.Nom_pedido AS Juego_Comprado, dp.Cantidad_detalleP, dp.PrecioUni_detalleP
FROM pedido ped
JOIN detallepedido dp ON ped.ID_pedido = dp.ID_pedido
JOIN Producto pr ON dp.ID_producto = pr.ID_producto
JOIN juego j ON pr.ID_producto = j.ID_producto;

- Consulta 8 (Con Agrupación - SUM): Calcular la ganancia total generada por todos los pedidos registrados.

SELECT SUM(PrecioT_pedido) AS Ganancia_Total 
FROM pedido;

- Consulta 9 (Con Agrupación - COUNT y GROUP BY): Contar cuántos juegos hay registrados por cada género (Acción, RPG, etc.).

SELECT gj.Nom_generoJ AS Genero, COUNT(jg.ID_juego) AS Cantidad_Juegos
FROM generoJ gj
JOIN juego_generoJ jg ON gj.ID_generoJ = jg.ID_generoJ
GROUP BY gj.Nom_generoJ;

- Consulta 10 (Avanzada con JOIN y funciones): Obtener el listado de clientes con el total de dinero gastado en pedidos de juegos,ordenados de mayor a menor gasto.

SELECT c.ID_cliente, c.Nom_cliente, c.Apelli_cliente, SUM(ped.PrecioT_pedido) AS Total_Gastado
FROM cliente c
JOIN pedido ped ON c.ID_cliente = ped.ID_cliente
GROUP BY c.ID_cliente, c.Nom_cliente, c.Apelli_cliente
ORDER BY Total_Gastado DESC;
