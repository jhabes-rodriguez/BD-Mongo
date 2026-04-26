# Taller MongoDB con Python (PyMongo)

Este repositorio o directorio contiene el desarrollo práctico para conectar un entorno de Python (como Google Colab) a un clúster de base de datos no relacional **MongoDB Atlas**, empleando la librería `pymongo`. 

A lo largo del taller, implementamos operaciones completas de CRUD (Crear, Leer, Actualizar y Eliminar) administradas mediante una interfaz interactiva de consola.

## Archivos Principales
*   **`mongodb_for_all.ipynb`**: Cuaderno base del taller. Contiene la importación de liberías, la cadena de conexión a MongoDB Atlas y la definición lógica de las funciones que acceden e interactúan con la base de datos `BD_CursoMongo` y su colección `Estudiantes`.
*   **`mongo.docx`**: Documento de referencia con el paso a paso teórico proporcionado en el material de clase para la creación de un clúster, ajustes de IP (Network Access) y usuarios de base de datos en AWS (Atlas).

---

## Modificaciones y Mejoras Realizadas

Respecto al cuaderno original, se realizaron las correspondientes integraciones y refactorizaciones para cumplir con los entregables del taller:

### 1. Configuración de Credenciales Reales
*   La variable `cliente = MongoClient(...)` fue actualizada en el código para apuntar ahora a tu URL personal, insertando automáticamente tu usuario y contraseña de base de datos, garantizando así la conexión correcta hacia el clúster.

### 2. Mejora Visual ("Pretty Print")
*   La función encargada de leer la base de datos (`listar_estudiantes()`) imprimía diccionarios completos en crudo que incluían identificadores de objeto complejos (`_id: ObjectId(...)`). 
*   **Mejora:** Modificamos este comportamiento para que la lista extraiga únicamente las llaves relevantes (`nombre`, `edad`, `carrera`) y formatee los strings visualmente como viñetas de tabla.
    *   *Ejemplo de salida actual:* `🔹 Nombre: Jhabes | Edad: 19 | Carrera: Ciencia de datos`

### 3. Dinamismo en la Actualización de Documentos
*   El código base originalmente limitaba la actualización *sólo a la edad* (`actualizar_edad()`). 
*   **Mejora:** La función fue reemplazada por la función paramétrica `actualizar_estudiante(nombre_actual, campo, nuevo_valor)`. Gracias a esto, no se duplican operaciones en Python; una misma función ahora es capaz de apuntar a una llave de MongoDB específica y actualizar `nombre`, `edad` o `carrera` usando el operador `$set` internamente.

### 4. Implementación del Menú Interactivo de Usuario
*   Respondiendo al requerimiento final del taller, se integró una nueva celda en el cuaderno definiendo la función `menu()`, la cual encapsula la lógica procedural dentro de un ciclo infinito (`while True`).
*   La terminal imprime las siguientes opciones, requiriendo `inputs()` para atrapar texto:
    1.  **Insertar estudiante:** Solicita en orden el nombre, edad (validando que sea un número) y carrera, para luego empujar un nuevo documento JSON a la colección.
    2.  **Listar estudiantes:** Llama la función de lectura previamente mejorada.
    3.  **Actualizar información:** Primero consulta qué usuario editar. Luego, despliega un **Sub-Menú** que consulta al usuario cuál llave quiere cambiar (Nombre, Edad o Carrera), intercepta y envía exclusivamente esa información para la edición.
    4.  **Eliminar estudiante:** Recibe un nombre exacto y remueve por completo su documento asociado.
    5.  **Salir:** Rompe adecuadamente el ciclo (comando `break`).

## Cómo ejecutar este proyecto
1. Ingresa a [Google Colab](https://colab.research.google.com/) y sube el archivo `.ipynb`.
2. Para evitar problemas de variables en caché, asegúrate de correr las celdas en el orden en el que aparecen, de arriba a abajo.
3. Puedes utilizar la opción **Ejecutar todo** (`Ctrl + F9`). 
4. Baja hasta la última celda. Verás que el código se queda cargando; esto significa que está a la espera de que ingreses una opción de texto en el bloque desplegado, comportándose como una aplicación de consola.
