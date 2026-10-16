# Diseño mejorado de ColdSense

## 1. Objetivo de la mejora

La propuesta consiste en dividir las responsabilidades del sistema en componentes independientes. Cada componente tendrá una función específica y se comunicará con los demás mediante interfaces definidas.

## 2. Componentes propuestos

### ReceptorIoT

Recibe los datos enviados por los dispositivos y convierte la información al formato que utiliza el sistema.

### ValidadorLecturas

Comprueba que los datos tengan el formato correcto y que los campos obligatorios estén presentes. Las mediciones válidas que se encuentren fuera de los rangos permitidos no se descartan, porque pueden representar una situación de riesgo.

### GestorUmbrales

Consulta y administra los límites configurados de temperatura y humedad para cada tipo de almacenamiento.

### GestorAlertas

Compara las mediciones válidas con los umbrales y determina si es necesario generar una alerta, así como su nivel de severidad.

### ServicioNotificaciones

Se encarga de enviar las alertas por los medios configurados. De esta forma, las reglas de detección no dependen directamente del mecanismo de envío.

### RepositorioLecturas

Guarda las mediciones y permite consultar el historial. Su separación facilita cambiar la tecnología de almacenamiento sin modificar la lógica principal.

### GeneradorReportes

Obtiene las lecturas necesarias y genera reportes para consultar el comportamiento de las condiciones ambientales.

### GestorDispositivos

Administra el registro y la información de los dispositivos conectados.

## 3. Flujo general de funcionamiento

1. El dispositivo IoT envía una medición.
2. ReceptorIoT recibe y transforma los datos.
3. ValidadorLecturas comprueba su estructura y consistencia.
4. RepositorioLecturas guarda la medición válida.
5. GestorUmbrales proporciona los límites configurados.
6. GestorAlertas evalúa si existe una condición de riesgo.
7. ServicioNotificaciones envía la alerta cuando corresponde.
8. GeneradorReportes consulta el historial para elaborar informes.

## 4. Beneficios del diseño mejorado

### Mantenimiento

Los cambios pueden realizarse en el componente responsable sin modificar todo el sistema.

### Reutilización

Los componentes de validación, almacenamiento y notificaciones pueden reutilizarse en otros proyectos con necesidades similares.

### Pruebas

Cada componente puede probarse de manera independiente mediante datos de ejemplo y dependencias simuladas.

### Ampliación

En el futuro se pueden incorporar nuevos sensores, canales de notificación y formatos de reportes con menos cambios en el resto de la arquitectura.

## 5. Consideraciones

Esta arquitectura es una propuesta de diseño. La implementación deberá definir las interfaces entre componentes, el manejo de errores, la seguridad de las comunicaciones y la protección de los datos almacenados.
