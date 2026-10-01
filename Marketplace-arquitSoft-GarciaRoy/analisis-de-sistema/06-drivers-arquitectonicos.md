# Drivers arquitectónicos

| ID | Driver arquitectónico | Origen | ¿Por qué influye? | Decisión que responde |
|---|---|---|---|---|
| DA01 | Soportar un incremento importante de usuarios en campañas. | AC03 – Escalabilidad | Influye en la estrategia de escalamiento y despliegue. | Monolito modular con escalamiento horizontal |
| DA02 | Mantener tiempos de respuesta adecuados con alta concurrencia. | AC01 – Rendimiento | Influye en comunicación, procesamiento y almacenamiento. | Caché y optimización de consultas |
| DA03 | Proteger datos de usuarios y operaciones de compra. | AC04 – Seguridad | Influye en autenticación, autorización y protección de datos. | Autenticación (JWT) y autorización por rol |
| DA04 | Integrarse con una pasarela de pago externa mediante API. | RC04 – Pasarela de pago | Condiciona la integración con servicios externos. | Interfaces (puertos) y adaptadores |
| DA05 | Usar API REST entre frontend y backend. | RC03 – API REST | Limita las alternativas de comunicación. | Separar interfaz y backend con API REST |
| DA06 | Modificar funcionalidades sin afectar innecesariamente otros módulos. | AC05 – Mantenibilidad | Influye en separación de responsabilidades, modularidad y dependencias internas. | Modularidad + Clean Architecture |
