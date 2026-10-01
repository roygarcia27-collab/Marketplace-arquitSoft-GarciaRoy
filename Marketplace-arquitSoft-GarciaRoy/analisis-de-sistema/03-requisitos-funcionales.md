# Requisitos funcionales

| ID | Requisito funcional |
|---|---|
| RF01 | El sistema debe permitir buscar productos mediante criterios de búsqueda. |
| RF02 | El sistema debe permitir consultar la información y disponibilidad de los productos. |
| RF03 | El sistema debe permitir registrar y actualizar productos en la plataforma. |
| RF04 | El sistema debe permitir agregar, modificar y eliminar productos del carrito de compra. |
| RF05 | El sistema debe permitir generar un pedido a partir de los productos del carrito. |
| RF06 | El sistema debe permitir consultar los pedidos realizados y su estado. |
| RF07 | El sistema debe permitir registrar, actualizar y desactivar sellers de la plataforma. |
| RF08 | El sistema debe permitir consultar el detalle de un pedido realizado. |
| RF09 | El sistema debe permitir registrar usuarios, iniciar sesión y controlar el acceso según su rol. |
| RF10 | El sistema debe permitir pagar un pedido mediante una pasarela de pago externa. |
| RF11 | El sistema debe permitir consultar el estado de envío de un pedido. |
| RF12 | El sistema debe permitir generar el comprobante de pago de un pedido. |
| RF13 | El sistema debe permitir sincronizar información de productos y stock con el ERP. |

## Relación entre HU y RF
| Historia de usuario | Requisitos funcionales |
|---|---|
| HU01 Buscar y consultar productos | RF01, RF02 |
| HU02 Gestionar productos | RF03, RF13 |
| HU03 Gestionar carrito | RF04 |
| HU04 Realizar pedido | RF05, RF08 |
| HU05 Gestionar sellers | RF07 |
| HU06 Consultar pedidos | RF06, RF08 |
| HU07 Pagar pedido | RF10, RF12 |
| HU08 Registro e inicio de sesión | RF09 |
| HU09 Seguimiento de envío | RF11 |
