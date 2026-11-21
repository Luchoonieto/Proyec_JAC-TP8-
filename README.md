# Proyec_JAC-TP8-


Descripcion del documento

1 - Introduccion:

-proposito: Este documento especifica los requisitos que seran necesarios del sistema "Gestor de Pedidos", una aplicacion diseñada y pensada para la gestion de pedidos de una tienda. El documento esta dirigido para al equipo que controla los resgistros del pedido.

-alcance: El sistema permite registrar, eliminar y editar los registros confirmados, incluyendo

-valor: El beneficio de este sistema para el negocio, es poder registrar los pedidos ya confirmados de una forma mas ordenada y rapida

2 - Descripcion General:
-persperctiva: Es un sistema nuevo y no se integraria con otros sistemas, es decir, es independiente, 

-usuario: El rol que cumpliria el usuario para este "Gestor de Pedidos" es la administrasion de pedidos

-funciones principales: Las funciones principales de este sistema de gestor de pedidos, ademas de registrar los pedidos, se puede editar y eliminar pedidos en caso de que sean necesarios

-restrincciones: para este sistema hay un plazo de 4 meses para desarrollarlo y el presupuesto es de 200USD, si hay normativa de seguridad para proteger los datos de este sistema

3 - requisitos especificos

• -requisitos de interfaces externas: ​​El sistema dispondrá de una interfaz gráfica (web o de escritorio) clara para que el personal autorizado pueda registrar, consultar y administrar las compras de productos. Tambien, ​La base de datos estará alojada en un Sistema Gestor de Bases de Datos Relacional, el sistema operará en equipos de escritorio o servidores estándar, compatibles con dispositivos de entrada convencionales

• Requisitos funcionales: las funciones que tendrian serian las siguientes: Registro de Compras de Productos: El sistema debe permitir registrar una nueva compra de productos (pudiendo asociar juegos, canciones o álbumes), especificando la fecha, las cantidades adquiridas y el costo unitario/total. debera permitir buscar y filtrar el historial de compras por fecha, tipo de producto, mostrando el detalle completo de cada transacción registrada.

• Requisitos no funcionales: Rendimiento y Tiempos de Respuesta: Las consultas sobre el historial de compras y los reportes de productos adquiridos deben completarse en un tiempo menor a 2 segundos bajo condiciones normales. Tambien, al registro y modificación de las compras estará restringido mediante autenticación de usuarios, permitiendo modificar registros únicamente a roles con permisos autorizados.


-consultas:



- Consulta 1: Listar los precios mayores a 35000

SELECT ID_producto, Tipo_producto, Nom_pedido, Precio_producto, Lanza_producto 
FROM Producto 
WHERE Precio_producto < 35000.00
ORDER BY Precio_producto ASC;

- consulta 2: lista de todos los pedidos

SELECT ID_pedido, ID_pago, ID_cliente, Fecha_pedido, PrecioT_pedido 
FROM pedido;

- Consulta 3: listar los pedidos de juegos conexion "online"

SELECT p.ID_producto, p.Nom_pedido AS Juego, c.Tipo_conexion
FROM Producto p
INNER JOIN juego j ON p.ID_producto = j.ID_producto
INNER JOIN juego_conexion jc ON j.ID_juego = jc.ID_juego
INNER JOIN conexion c ON jc.ID_conexion = c.ID_conexion
WHERE c.Tipo_conexion = 'Online';

- consulta 4: listar los pedidos de juegos del desarrollador John loke

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

- Consulta 6: Listar todos los productos con precio menor a 35000

SELECT ID_producto, Tipo_producto, Nom_pedido, Precio_producto, Lanza_producto
FROM Producto
WHERE Precio_producto < 35000.00;


- consulta 7: Listar todas las canciones de artistas asociados al género 'Pop'

SELECT DISTINCT p.ID_producto, 
                p.Nom_pedido AS Nombre_Cancion, 
                c.Duracion_cancion, 
                p.Precio_producto, 
                a.Nom_artista, 
                a.Apelli_artista, 
                g.Nom_generoA AS Genero
FROM Producto p
INNER JOIN cancion c ON p.ID_producto = c.ID_producto
INNER JOIN artista_cancion ac ON c.ID_cancion = ac.ID_cancion
INNER JOIN artista a ON ac.ID_artista = a.ID_artista
INNER JOIN artista_generoA ag ON a.ID_artista = ag.ID_artista
INNER JOIN generoA g ON ag.ID_generoA = g.ID_generoA
WHERE g.Nom_generoA = 'Pop';

- Consulta 8: Listar todas las canciones registradas

SELECT p.ID_producto, 
       c.ID_cancion, 
       p.Nom_pedido AS Nombre_Cancion, 
       c.Duracion_cancion, 
       p.Precio_producto, 
       p.Lanza_producto
FROM Producto p
INNER JOIN cancion c ON p.ID_producto = c.ID_producto;

- consulta 9: Listar todos los pedidos pagados en efectivo

SELECT pe.ID_pedido, 
       pe.Fecha_pedido, 
       pe.PrecioT_pedido, 
       pa.Tipo_pago, 
       c.Nom_cliente, 
       c.Apelli_cliente
FROM pedido pe
INNER JOIN pago pa ON pe.ID_pago = pa.ID_pago
INNER JOIN cliente c ON pe.ID_cliente = c.ID_cliente
WHERE pa.Tipo_pago = 'Efectivo';

- Consulta 10: Listar todos los pedidos realizados el 2026-11-21

SELECT pe.ID_pedido, 
       pe.Fecha_pedido, 
       pe.PrecioT_pedido, 
       pa.Tipo_pago, 
       c.Nom_cliente, 
       c.Apelli_cliente
FROM pedido pe
INNER JOIN pago pa ON pe.ID_pago = pa.ID_pago
INNER JOIN cliente c ON pe.ID_cliente = c.ID_cliente
WHERE DATE(pe.Fecha_pedido) = '2026-11-21';



