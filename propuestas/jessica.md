+# Propuesta individual de Jessica: almacenamiento d

## 1. Enfoque de la propuesta

Mi propuesta de mejora para ColdSense se enfoca en separar la responsabilidad de almacenamiento de las lecturas ambientales de la lógica principal del sistema.

En el diseño original, el componente principal de ColdSense concentra varias responsabilidades y podría terminar dependiendo directamente de una base de datos específica. Esto dificulta cambiar la tecnología de almacenamiento, realizar pruebas y reutilizar la lógica del sistema.

La propuesta consiste en crear una interfaz `RepositorioLecturas` que defina las operaciones necesarias para guardar y consultar lecturas, sin depender de una tecnología específica de base de datos.

## 2. Nuevas clases propuestas

### RepositorioLecturas

Responsabilidad:
- Guardar lecturas ambientales.
- Consultar lecturas por fecha o dispositivo.
- Recuperar el historial de mediciones.
- Definir las operaciones que necesita el sistema para trabajar con las lecturas.

Esta clase o interfaz evita que la lógica principal dependa directamente de una base de datos.

### RepositorioSQLite

Responsabilidad:
- Implementar `RepositorioLecturas`.
- Guardar las lecturas utilizando SQLite.
- Recuperar el historial almacenado en SQLite.

### RepositorioMongoDB

Responsabilidad:
- Implementar `RepositorioLecturas`.
- Guardar las lecturas utilizando MongoDB.
- Recuperar el historial almacenado en MongoDB.

Esta implementación representa una alternativa futura y no significa que MongoDB tenga que implementarse actualmente.

### ServicioHistorial

Responsabilidad:
- Solicitar al repositorio las lecturas históricas.
- Filtrar o consultar información necesaria para el historial.
- Entregar los datos para reportes o consultas.

El servicio no necesita conocer cómo funciona internamente la base de datos.

## 3. Diagrama de la propuesta

```mermaid
classDiagram

class ServicioHistorial {
    +consultarHistorial(dispositivo, fecha)
}

class RepositorioLecturas {
    <<interface>>
    +guardarLectura(lectura)
    +consultarLecturas(dispositivo, fecha)
    +obtenerHistorial(dispositivo)
}

class RepositorioSQLite {
    +guardarLectura(lectura)
    +consultarLecturas(dispositivo, fecha)
    +obtenerHistorial(dispositivo)
}

class RepositorioMongoDB {
    +guardarLectura(lectura)
    +consultarLecturas(dispositivo, fecha)
    +obtenerHistorial(dispositivo)
}

class LecturaAmbiental {
    +temperatura
    +humedad
    +fechaHora
    +dispositivoId
}

ServicioHistorial --> RepositorioLecturas
RepositorioSQLite ..|> RepositorioLecturas
RepositorioMongoDB ..|> RepositorioLecturas
RepositorioLecturas --> LecturaAmbiental
## 4. Diferencia con la propuesta de Andrea

La propuesta de Andrea se enfoca principalmente en dividir las responsabilidades generales del sistema ColdSense en componentes especializados.

Mi propuesta se concentra específicamente en el almacenamiento y acceso a las lecturas. El objetivo es aplicar una separación entre la lógica del sistema y la tecnología utilizada para guardar los datos.

De esta manera, las dos propuestas aportan mejoras diferentes al diseño del proyecto.

## 5. Justificación

Esta separación permite:

- Cambiar SQLite por otra tecnología sin modificar la lógica principal.
- Realizar pruebas utilizando un repositorio simulado.
- Reducir el acoplamiento entre el sistema y la base de datos.
- Reutilizar el acceso a las lecturas desde diferentes funcionalidades.
- Facilitar futuras ampliaciones del sistema.
- Mantener más organizada la responsabilidad relacionada con los datos.

## 6. Beneficios para ColdSense

La propuesta facilita el mantenimiento porque los cambios relacionados con la base de datos se concentran en las implementaciones del repositorio.

También mejora las pruebas, ya que se puede utilizar una implementación de prueba de `RepositorioLecturas` sin necesidad de utilizar una base de datos real.

Además, permite que ColdSense pueda evolucionar hacia diferentes tecnologías de almacenamiento sin modificar directamente los componentes que procesan las lecturas ambientales.

## 7. Alcance

Esta propuesta corresponde a un diseño conceptual de software. Las clases representan una organización propuesta de responsabilidades y no implican que actualmente exista una implementación funcional de SQLite o MongoDB en el proyecto.
## 4. Diferencia con la propuesta de Andrea

La propuesta de Andrea se enfoca principalmente en dividir las responsabilidades generales del sistema ColdSense en componentes especializados.

Mi propuesta se concentra específicamente en el almacenamiento y acceso a las lecturas. El objetivo es separar la lógica del sistema de la tecnología utilizada para guardar los datos.

De esta manera, las dos propuestas aportan mejoras diferentes al diseño del proyecto.

## 5. Justificación

Esta separación permite:

- Cambiar SQLite por otra tecnología sin modificar la lógica principal.
- Realizar pruebas utilizando un repositorio simulado.
- Reducir el acoplamiento entre el sistema y la base de datos.
- Reutilizar el acceso a las lecturas desde diferentes funcionalidades.
- Facilitar futuras ampliaciones del sistema.
- Mantener organizada la responsabilidad relacionada con los datos.

## 6. Beneficios para ColdSense

La propuesta facilita el mantenimiento porque los cambios relacionados con la base de datos se concentran en las implementaciones del repositorio.

También mejora las pruebas, ya que se puede utilizar una implementación de prueba de `RepositorioLecturas` sin necesidad de utilizar una base de datos real.

Además, permite que ColdSense pueda evolucionar hacia diferentes tecnologías de almacenamiento sin modificar directamente los componentes que procesan las lecturas ambientales.

## 7. Alcance

Esta propuesta corresponde a un diseño conceptual de software. Las clases representan una organización propuesta de responsabilidades y no implican que actualmente exista una implementación funcional de SQLite o MongoDB en el proyecto.
