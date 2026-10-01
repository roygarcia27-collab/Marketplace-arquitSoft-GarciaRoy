# Decisiones arquitectónicas (ADR)

| ID | Decisión | Driver | Justificación | Resultado |
|---|---|---|---|---|
| ADR-001 | Monolito modular | DA01, DA06 | Funcionalidades en módulos independientes dentro de una misma aplicación desplegable. | Módulos Usuarios, Sellers, Catálogo, Carrito, Pedidos |
| ADR-002 | Clean Architecture | DA06 | Separar reglas de negocio de detalles tecnológicos. | Capas Dominio, Aplicación, Infraestructura y Presentación |
| ADR-003 | Estrategia de caché | DA02 | Reducir consultas repetitivas a la base de datos. | Caché para consultas frecuentes (catálogo) |
| ADR-004 | Integración de pagos mediante interfaces y adaptadores | DA04 | Desacoplar los casos de uso del proveedor de pagos. | Puerto `ProcesadorPagos` + adaptador de la pasarela |
| ADR-005 | API REST entre frontend y backend | DA05 | Separar interfaz y backend con un contrato estándar. | API `/api/v1/*` en JSON sobre HTTPS |

---

## ADR-001: Monolito modular
- **Estado:** Aceptada
- **Contexto:** Se esperan picos de usuarios en campañas (DA01) y se requiere cambiar módulos sin afectar a otros (DA06). El equipo es pequeño y el alcance es académico.
- **Decisión:** Una sola aplicación desplegable organizada en módulos con límites claros (`src/modules/<modulo>`). Un módulo solo accede a otro a través de su servicio/caso de uso, nunca a sus tablas.
- **Alternativas:** Microservicios (descartada: complejidad operativa, red y despliegue innecesarios para el alcance); monolito sin módulos (descartada: alto acoplamiento).
- **Consecuencias:** (+) despliegue simple, escalamiento horizontal con varias instancias tras un balanceador, evolución a servicios posible. (−) un fallo no controlado puede afectar a toda la aplicación; exige disciplina para respetar los límites.

## ADR-002: Clean Architecture
- **Estado:** Aceptada
- **Contexto:** Las reglas del negocio (pedido, carrito, stock) no deben depender de Express, PostgreSQL ni de la pasarela de pago (DA06).
- **Decisión:** Cada módulo se organiza en Dominio, Aplicación, Presentación e Infraestructura; las dependencias de código apuntan solo hacia el dominio.
- **Alternativas:** Arquitectura en capas clásica (descartada: la capa de negocio queda acoplada a la persistencia); Hexagonal/Onion (equivalentes en intención, se elige Clean por ser el enfoque del curso).
- **Consecuencias:** (+) pruebas unitarias del dominio sin infraestructura, tecnologías intercambiables. (−) más archivos e interfaces; mapeos entre capas.

## ADR-003: Estrategia de caché
- **Estado:** Aceptada
- **Contexto:** Alta concurrencia en lectura de catálogo durante campañas (DA02).
- **Decisión:** Caché (p. ej., Redis) para información de consulta frecuente (listados y detalle de productos), con expiración e invalidación al actualizar un producto o recibir stock del ERP. La caché se usa detrás de un puerto del repositorio, no desde el dominio.
- **Alternativas:** Solo índices en BD (insuficiente en picos); CDN para API (no cubre datos dinámicos).
- **Consecuencias:** (+) menor latencia y carga en PostgreSQL. (−) posible dato desactualizado por unos segundos; hay que definir el TTL.

## ADR-004: Integración de pagos mediante interfaces y adaptadores
- **Estado:** Aceptada
- **Contexto:** La pasarela de pago es externa (RC04, DA04) y puede cambiar de proveedor.
- **Decisión:** La capa de Aplicación define el puerto `ProcesadorPagos`; la capa de Infraestructura implementa un adaptador por proveedor (p. ej., `PasarelaPagosAdapter`). El caso de uso `PagarPedido` solo conoce la interfaz.
- **Alternativas:** Llamar al SDK del proveedor desde el servicio (descartada: acoplamiento y dificultad para probar).
- **Consecuencias:** (+) proveedor intercambiable, pruebas con adaptador simulado. (−) una interfaz adicional que mantener. Se aplica el mismo criterio a envío, facturación y ERP.

## ADR-005: API REST entre frontend y backend
- **Estado:** Aceptada
- **Contexto:** El frontend Angular y el backend Node.js son independientes (RC03, DA05).
- **Decisión:** Contrato REST/JSON versionado (`/api/v1`), con autenticación JWT (DA03) y validación de entrada en la capa de presentación.
- **Consecuencias:** (+) frontend y backend evolucionan por separado. (−) hay que mantener el contrato y el manejo de errores.
