# Contrato Base del Proyecto

## 1. Partes

Entre:

* **Solicitante:** Alejandro Rodriguez
* **Responsable del desarrollo:** Maximo Mule

Se acuerda el presente contrato para la definición y ejecución del proyecto técnico descrito en este documento.

## 2. Objeto del contrato

Desarrollar un worker ejecutable por CLI en Python para integración con la API de MusicBrainz, con capacidad de:

* Consumir tareas pendientes de una cola.
* Ejecutar consumo de la API de MusicBrainz, con identificación mediante `User-Agent` y respetando el límite de 1 pedido por segundo.
* Buscar discos por artista o por título de disco, y obtener el detalle completo de un disco a partir de su ID.
* Persistir payloads obtenidos.
* Inferir y versionar schemas del payload.
* Detectar cambios estructurales entre versiones.
* Registrar eventos operativos del procesamiento.

## 3. Alcance funcional mínimo

El proyecto debe incluir, como mínimo:

1. Toma exclusiva de tareas pendientes con control de concurrencia.
2. Consumo de los endpoints `GET /ws/2/release` (búsqueda de discos) y `GET /ws/2/release/<id>` (detalle de un disco).
3. Persistencia de respuesta completa en base de datos SQLite3.
4. Cálculo de hash de schema para detección de cambios.
5. Versionado de schema cuando exista diferencia estructural.
6. Registro de eventos operativos (asignación, captura, versionado, finalización, error).
7. Cierre de tarea con estado final de ejecución.

## 4. Entregables

* Código fuente funcional del worker.
* Script o instrucciones de ejecución por CLI.
* Definición de modelo de datos mínimo: `task_queue`, `assets`, `schema_versions`, `schema_snapshots`, `worker_events`.
* Documento de workplan del proyecto (`readme.txt`).

## 5. Criterios de aceptación

Se considerará cumplido el contrato cuando:

1. El worker procese una tarea completa de extremo a extremo (búsqueda de discos y obtención del detalle de un disco).
2. Se evidencie almacenamiento del payload capturado.
3. Se registre al menos un evento de ejecución.
4. El sistema detecte correctamente cambio y no cambio de schema.
5. Se mantenga trazabilidad de la tarea procesada.

## 6. Exclusiones

No se incluye en este contrato, salvo acuerdo adicional:

* Desarrollo de interfaz gráfica (frontend).
* Despliegue productivo en infraestructura final.
* Soporte posterior a la entrega fuera del período académico o acordado.
