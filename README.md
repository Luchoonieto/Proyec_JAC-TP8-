# Proyec_JAC-TP8-


-consultas:



- Consulta 1: Listar los precios mayores a 35000

SELECT ID_producto, Tipo_producto, Nom_pedido, Precio_producto, Lanza_producto 
FROM Producto 
WHERE Precio_producto < 35000.00
ORDER BY Precio_producto ASC;

- consulta 2: lista de todos los pedidos

SELECT ID_pedido, ID_pago, ID_cliente, Fecha_pedido, PrecioT_pedido 
FROM pedido;

- Consulta 3: listar los pedidos de conexion de "online"

SELECT p.ID_producto, p.Nom_pedido AS Juego, c.Tipo_conexion
FROM Producto p
INNER JOIN juego j ON p.ID_producto = j.ID_producto
INNER JOIN juego_conexion jc ON j.ID_juego = jc.ID_juego
INNER JOIN conexion c ON jc.ID_conexion = c.ID_conexion
WHERE c.Tipo_conexion = 'Online';

- consulta 4: listar los pedidos del desarrollador John loke

SELECT p.ID_producto, p.Nom_pedido AS Juego, d.Nom_desarrollador, d.Apelli_desarrollador
FROM Producto p
INNER JOIN juego j ON p.ID_producto = j.ID_producto
INNER JOIN juego_desarrollador jd ON j.ID_juego = jd.ID_juego
INNER JOIN desarrollador d ON jd.ID_desarrollador = d.ID_desarrollador
WHERE d.Nom_desarrollador = 'John' AND d.Apelli_desarrollador = 'Locke';


- Consulta 5: Listar las canciones de la artista Billie Eilish
SELECT p.ID_producto, 
       p.Nom_pedido AS Nombre_Cancion, 
       c.Duracion_cancion, 
       p.Precio_producto, 
       p.Lanza_producto,
       a.Nom_artista, 
       a.Apelli_artista
FROM Producto p
INNER JOIN cancion c ON p.ID_producto = c.ID_producto
INNER JOIN artista_cancion ac ON c.ID_cancion = ac.ID_cancion
INNER JOIN artista a ON ac.ID_artista = a.ID_artista
WHERE a.Nom_artista = 'Billie' AND a.Apelli_artista = 'Eilish';
