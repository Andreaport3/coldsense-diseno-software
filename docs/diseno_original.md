# Diseño original de ColdSense

## 1. Descripción general

ColdSense es una propuesta de sistema IoT que permite supervisar las condiciones ambientales de espacios de almacenamiento de productos sensibles a la temperatura, como medicamentos y alimentos. El sistema recibe información de sensores, registra las lecturas y genera alertas cuando las condiciones se encuentran fuera de los rangos establecidos.

Para este análisis se plantea un diseño inicial hipotético en el que la mayoría de las funciones se concentran en un solo componente.

## 2. Responsabilidades del diseño inicial

Se propone una clase principal llamada `ColdSenseSystem`, encargada de realizar las siguientes actividades:

- Recibir las lecturas de los sensores.
- Validar los datos recibidos.
- Comprobar los valores de temperatura y humedad.
- Guardar las lecturas en la base de datos.
- Evaluar los umbrales configurados.
- Generar y enviar alertas.
- Consultar el historial de mediciones.
- Generar reportes.
- Administrar dispositivos y usuarios.

## 3. Problemas de diseño identificados

### Alta concentración de responsabilidades

Una sola clase realiza demasiadas tareas diferentes, lo que dificulta comprender y modificar el sistema.

### Bajo nivel de modularidad

Las funciones no están suficientemente separadas. Un cambio en las notificaciones podría afectar otras partes del sistema.

### Dificultad para realizar pruebas

Probar una función puede requerir interactuar con la base de datos, los sensores y el sistema de alertas al mismo tiempo.

### Dependencia entre componentes

Si la lógica de negocio depende directamente de una tecnología específica de almacenamiento o notificaciones, cambiarla puede requerir modificaciones en distintas partes del programa.

### Dificultad para incorporar nuevas funciones

Agregar nuevos tipos de sensores, notificaciones o reportes puede aumentar la complejidad de la clase principal.

## 4. Consecuencias

Estos problemas pueden aumentar el tiempo de mantenimiento, dificultar la reutilización del código y elevar el riesgo de errores cuando se agregan nuevas funcionalidades.

Por estas razones, se propone reorganizar el diseño mediante componentes con responsabilidades específicas.
