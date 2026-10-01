# Arquitectura inicial del sistema (Guía 02)

Primera propuesta en tres capas. Las integraciones con sistemas externos las realiza la capa de lógica de negocio.

```mermaid
flowchart TD
    subgraph ACTORES["ACTORES"]
        Cliente["Cliente"]
        Seller["Seller"]
        Admin["Administrador"]
    end

    subgraph PRESENTACION["PRESENTACIÓN"]
        Web["Aplicación Web → API REST"]
    end

    subgraph NEGOCIO["LÓGICA DE NEGOCIO"]
        Usuarios["Usuarios"]
        Sellers["Sellers"]
        Catalogo["Catálogo"]
        Carrito["Carrito"]
        Pedidos["Pedidos"]
    end

    subgraph DATOS["DATOS"]
        BD[("PostgreSQL")]
    end

    subgraph EXTERNOS["SISTEMAS EXTERNOS"]
        Pago["Pasarela de pago"]
        ERP["ERP"]
        Envio["Servicio de envío"]
        Fact["Facturación"]
    end

    ACTORES --> PRESENTACION
    PRESENTACION --> NEGOCIO
    NEGOCIO --> DATOS
    NEGOCIO -->|"integraciones"| EXTERNOS
```

## Descripción
- **Presentación:** interacción de los usuarios mediante la aplicación web y la API REST.
- **Lógica de negocio:** módulos de usuarios, sellers, catálogo, carrito y pedidos.
- **Datos:** almacenamiento y consulta en PostgreSQL.
- Los módulos de **Pedidos** y **Catálogo** se integran con la pasarela de pago, el servicio de envío, la facturación y el ERP.
