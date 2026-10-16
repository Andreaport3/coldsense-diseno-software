# Análisis del diseño de alertas y notificaciones de ColdSense IoT

## 1. Introducción

ColdSense IoT permite monitorear las condiciones ambientales de almacenes donde se conservan medicamentos o alimentos.

Mi aportación consiste en analizar y mejorar el diseño de las alertas y notificaciones para separar responsabilidades y facilitar el mantenimiento del software.

## 2. Problema del diseño original

En un diseño concentrado, una clase principal podría encargarse de recibir lecturas, evaluar las condiciones ambientales, generar alertas y enviar notificaciones.

Esta concentración presenta varios problemas:

- Dificulta el mantenimiento del código.
- Complica las pruebas individuales.
- Genera dependencias entre distintas responsabilidades.
- Dificulta incorporar nuevos medios de notificación.
- Hace que los cambios en una función puedan afectar a otras.

Por ello, se propone distribuir las responsabilidades entre clases especializadas.

## 3. Propuesta de diseño mejorado

Se propone separar la evaluación del riesgo, la gestión de alertas y el envío de notificaciones.

### 3.1. EvaluadorRiesgo

Responsabilidad:

Analizar las lecturas de temperatura y humedad y compararlas con los límites configurados.

Funciones principales:

- Recibir los valores de una lectura.
- Comparar las lecturas con los límites permitidos.
- Identificar condiciones fuera del rango establecido.
- Determinar la gravedad del riesgo según las reglas definidas.

Esta clase no se encarga de enviar notificaciones.

### 3.2. GestorAlertas

Responsabilidad:

Gestionar las alertas cuando se detecta una condición peligrosa.

Funciones principales:

- Recibir el resultado de la evaluación.
- Determinar si corresponde generar una alerta.
- Asociar la alerta con el dispositivo correspondiente.
- Registrar la información necesaria para su seguimiento.

Esta clase no contiene el mecanismo específico para enviar correos electrónicos o mensajes.

### 3.3. ServicioNotificaciones

Responsabilidad:

Gestionar el envío de avisos al personal responsable.

Funciones principales:

- Recibir la información de una alerta.
- Preparar el mensaje.
- Enviar la notificación mediante el canal configurado.
- Informar si el envío fue exitoso o si ocurrió un error.

En el futuro se podrían incorporar diferentes canales, como correo electrónico o mensajes.

## 4. Flujo de funcionamiento

1. Un sensor registra la temperatura y la humedad.
2. El sistema recibe la lectura.
3. EvaluadorRiesgo compara los valores con los límites.
4. Si detecta una condición peligrosa, comunica el resultado.
5. GestorAlertas genera y registra la alerta correspondiente.
6. ServicioNotificaciones envía el aviso al personal responsable.

Si la lectura está dentro de los límites permitidos, no se genera una alerta por esa evaluación.

## 5. Ejemplo de funcionamiento

Supongamos que un refrigerador tiene un límite máximo de temperatura configurado en 8 °C.

El sensor registra una temperatura de 9 °C.

EvaluadorRiesgo identifica que la temperatura supera el límite permitido.

GestorAlertas genera una alerta con la información de la lectura y del dispositivo.

Finalmente, ServicioNotificaciones envía un aviso al personal responsable para que revise el refrigerador.

Este ejemplo describe el comportamiento propuesto; no implica que el envío de notificaciones esté implementado.

## 6. Beneficios de la propuesta

- Mayor modularidad.
- Menor dependencia entre responsabilidades.
- Mantenimiento más sencillo.
- Pruebas individuales más fáciles.
- Posibilidad de incorporar nuevos canales de notificación.
- Mayor facilidad para modificar las reglas de evaluación.
- Mejor organización del código.

## 7. Pruebas propuestas

### Prueba 1: Temperatura dentro del límite

Entrada: temperatura de 5 °C y límite máximo de 8 °C.

Resultado esperado: no se genera una alerta por superar el límite de temperatura.

### Prueba 2: Temperatura fuera del límite

Entrada: temperatura de 9 °C y límite máximo de 8 °C.

Resultado esperado: se identifica la condición peligrosa y se genera la alerta correspondiente.

### Prueba 3: Error en una notificación

Entrada: una alerta válida y un servicio de notificaciones que devuelve un error.

Resultado esperado: se identifica el fallo del envío sin modificar las reglas de evaluación del riesgo.

Estas pruebas describen resultados esperados del diseño; no se afirma que hayan sido ejecutadas.

## 8. Aportación individual

Mi aportación consiste en analizar el diseño de las alertas y notificaciones de ColdSense IoT y proponer la separación de responsabilidades mediante las clases EvaluadorRiesgo, GestorAlertas y ServicioNotificaciones.

Esta propuesta busca mejorar la modularidad, el mantenimiento y la capacidad de ampliación del sistema.
