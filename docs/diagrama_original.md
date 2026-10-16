# Diagrama del diseño original de ColdSense

El diseño inicial propuesto concentra las responsabilidades principales en una sola clase. Esto genera una dependencia elevada entre las funciones.

```mermaid
flowchart TD
    A[Dispositivos y sensores IoT] --> B[ColdSenseSystem]
    B --> C[Recepción de lecturas]
    B --> D[Validación de datos]
    B --> E[Evaluación de temperatura y humedad]
    B --> F[Almacenamiento de lecturas]
    B --> G[Generación y envío de alertas]
    B --> H[Consulta de historial]
    B --> I[Generación de reportes]
    B --> J[Gestión de dispositivos y usuarios]
    F --> K[(Base de datos)]
    H --> K
```

## Observación

La clase principal concentra demasiadas funciones. Si cambia la base de datos, la forma de enviar alertas o la generación de reportes, puede ser necesario modificar el mismo componente.
