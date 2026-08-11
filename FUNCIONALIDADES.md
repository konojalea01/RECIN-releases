# Funcionalidades de RECIN

Lista correspondiente a RECIN 0.2.8.

## Registros

- Alta manual de incapacidades.
- Edición de registros existentes.
- Eliminación individual con confirmación.
- Eliminación conjunta de incapacidades vencidas.
- Folio numérico único por registro.
- Nombre, días, fecha inicial, fecha final y tipo.
- Tipos `Inicial` y `Subsecuente`.
- Mensajes de confirmación y error dentro de la interfaz.

## Fechas y validación

- Fecha inicial predeterminada al día actual.
- Cálculo de fecha final a partir de los días.
- Cálculo de días a partir de las fechas.
- Sobrescritura manual de ambas fechas.
- Validación de enteros positivos.
- Rechazo de fechas finales iguales o anteriores a la inicial.
- Verificación de congruencia entre días y fechas.
- Prevención de folios duplicados.

## Dashboard y tabla

- Ventana principal maximizada.
- Tabla desplazable y encabezado fijo.
- Orden por vencimiento más próximo.
- Búsqueda por nombre, folio o tipo.
- Contadores total, seguro, próximo y urgente.
- Etiqueta de días restantes o días vencidos.
- Filas verdes, amarillas y rojas según vencimiento.
- Botones de edición y eliminación por fila.
- Estado vacío y contador de resultados.
- Versión visible y crédito al Dpto. de Desarrollo y Sistemas de Apolo Platinum.

## Excel

- Importación de archivos `.xlsx`.
- Reconocimiento normalizado de encabezados.
- Lectura de fechas nativas de Excel.
- Validación de columnas, días, fechas, tipo y folio.
- Omisión controlada de filas inválidas.
- Detección de duplicados internos y existentes.
- Resumen de filas importadas y omitidas.

## Persistencia y privacidad

- Almacenamiento JSON local compartido.
- Escritura atómica mediante archivo temporal.
- Migración de datos antiguos desde `localStorage`.
- Conservación de registros tras actualizar o desinstalar.
- Sin envío de datos personales a servicios externos.

## Notificaciones de Windows

- Proceso independiente sin consola.
- Inicio automático mediante tarea programada.
- Funcionamiento con la ventana principal cerrada.
- Revisión inmediata y cada hora.
- Avisos a tres días o menos, mañana, hoy y vencida.
- Control persistente para evitar avisos duplicados.
- Archivo de diagnóstico `notifier.log`.
- Modo de prueba `RECINNotifier.exe --test`.

## Actualización

- Comprobación al iniciar y cada 30 segundos.
- Comparación semántica de versiones.
- Modal integrado con notas de versión.
- Progreso real de descarga.
- Descarte durante la sesión actual.
- Nueva oferta al reiniciar si sigue pendiente.
- Elevación UAC mediante API nativa de Windows.
- Instalación silenciosa y reinicio automático.
- Descargas restringidas al canal autorizado.
- Ruta inmutable por versión para evitar caché obsoleta.

## Instalación y distribución

- Instalación nueva y actualización sobre una existente.
- Instalación de aplicación y notificador.
- Accesos directos en escritorio y menú Inicio.
- Registro y eliminación de la tarea programada.
- Desinstalador incluido.
- Icono nativo del ejecutable, ventana, barra de tareas e instalador.
- Builds y releases automatizados mediante GitHub Actions.
- Código fuente privado y canal binario público independiente.
