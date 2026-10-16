# ColdSense: Análisis y mejora del diseño de software

## 1. Descripción del proyecto

ColdSense es una propuesta de sistema IoT orientado a supervisar las condiciones ambientales de espacios donde se almacenan productos sensibles a la temperatura, como medicamentos y alimentos.

El sistema contempla la recepción de datos de sensores, el registro de mediciones, la evaluación de umbrales y la generación de alertas cuando se detectan condiciones de riesgo.

Este repositorio presenta un análisis del diseño inicial propuesto y una arquitectura mejorada que separa las responsabilidades del sistema en componentes independientes.

## 2. Objetivo

Analizar los problemas de un diseño inicial concentrado en un solo componente y proponer una arquitectura modular que facilite el mantenimiento, las pruebas, la reutilización y la incorporación de nuevas funcionalidades.

## 3. Contenido del repositorio

- `docs/diseno_original.md`: descripción del diseño inicial y sus problemas.
- `docs/diagrama_original.md`: diagrama del diseño inicial.
- `docs/diseno_mejorado.md`: descripción de la arquitectura mejorada.
- `docs/diagrama_mejorado.md`: diagrama de la arquitectura propuesta.
- `docs/aportaciones.md`: registro de las contribuciones individuales del equipo.

## 4. Arquitectura propuesta

El diseño mejorado separa la recepción de datos, la validación de lecturas, la gestión de umbrales, la evaluación de alertas, las notificaciones, el almacenamiento y la generación de reportes.

Esta separación permite modificar un componente sin tener que cambiar necesariamente todo el sistema.

## 5. Alcance

El repositorio se centra en el análisis y la propuesta de diseño de software. Los diagramas representan una arquitectura conceptual; no implican que todos los componentes estén implementados o conectados a dispositivos físicos.

## 6. Equipo de trabajo

- Andrea Portillo Rosales
- Jessica Camargo Olvera
- Citlali Luna Zamorano

Las aportaciones específicas de cada integrante se documentarán en `docs/aportaciones.md` de acuerdo con el trabajo que cada persona realice.

## 7. Documentación

Para consultar el análisis, abre los archivos de la carpeta `docs`. Los diagramas están escritos en Mermaid y pueden visualizarse en plataformas compatibles, como GitHub.
