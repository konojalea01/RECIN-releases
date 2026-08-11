# Documentación de RECIN

## Información del producto

- **Nombre:** RECIN — Recordatorio de Incapacidades.
- **Versión documentada:** 0.2.8.
- **Plataforma de operación:** Windows 10 y Windows 11 de 64 bits.
- **Desarrollo:** Dpto. de Desarrollo y Sistemas de Apolo Platinum.
- **Tecnologías:** Wails, Go, Vue y TypeScript.

RECIN es una aplicación de escritorio para registrar incapacidades, visualizar su proximidad de vencimiento e informar al usuario mediante notificaciones de Windows aun cuando la ventana principal esté cerrada.

## Componentes instalados

| Componente | Responsabilidad |
|---|---|
| `RECIN.exe` | Interfaz, captura, importación, almacenamiento y actualización. |
| `RECINNotifier.exe` | Revisión periódica y notificaciones en segundo plano. |
| `RECIN Notifications` | Tarea programada que inicia el notificador al entrar a Windows. |
| `incapacidades.json` | Registros locales del usuario. |
| `notificaciones.json` | Control de avisos ya enviados. |
| `notifier.log` | Diagnóstico del notificador. |

## Flujo de operación

1. El usuario registra una incapacidad manualmente o importa un archivo Excel.
2. RECIN valida folio, nombre, días, fechas y tipo.
3. El registro se guarda localmente en el perfil de Windows.
4. El dashboard calcula el estado con respecto a la fecha actual.
5. El notificador lee el mismo archivo al iniciar y cada hora.
6. Cuando un registro entra en un umbral relevante, Windows muestra un aviso único.

## Captura manual

El formulario solicita folio, nombre, días, fecha inicial, fecha final y tipo. La fecha inicial utiliza el día actual por defecto. Al cambiar los días se calcula la fecha final; al cambiar cualquiera de las fechas se recalculan los días. No se aceptan folios repetidos, valores no enteros, fechas incongruentes ni una fecha final que no sea posterior a la inicial.

## Importación de Excel

El formato admitido es `.xlsx` y requiere las columnas `Folio`, `Nombre`, `Días`, `Fecha de inicio`, `Fecha final` y `Tipo`. El tipo debe ser `Inicial` o `Subsecuente`. Las filas inválidas o duplicadas se omiten y al finalizar se presenta un resumen de importación.

## Clasificación por vencimiento

- **Verde:** quedan más de tres días.
- **Amarillo:** quedan dos o tres días.
- **Rojo:** queda un día, vence hoy o ya venció.

La tabla se ordena por fecha final ascendente y puede buscarse por nombre, folio o tipo.

## Notificaciones

`RECINNotifier.exe` se ejecuta en la sesión interactiva del usuario mediante la tarea `RECIN Notifications`. Revisa al comenzar y cada hora. Notifica cuando faltan tres días o menos, cuando vence mañana, cuando vence hoy y cuando ya venció. Cada combinación de folio, fecha final y umbral se envía una sola vez.

Para comprobarlo desde PowerShell:

```powershell
$notifier = (Get-Process RECINNotifier).Path
Stop-Process -Name RECINNotifier -Force
& $notifier --test
Start-ScheduledTask -TaskName "RECIN Notifications"
Get-Content "$env:APPDATA\RECIN\notifier.log" -Tail 30
```

## Actualizaciones

RECIN consulta el canal público al abrirse y cada 30 segundos. Una versión posterior abre un modal con progreso de descarga. El instalador solicita elevación UAC, cierra los procesos anteriores, reemplaza los archivos y vuelve a abrir RECIN. Cada versión utiliza una URL inmutable para evitar contenido obsoleto de caché.

## Datos y privacidad

Los registros se almacenan normalmente en `%AppData%\RECIN\incapacidades.json`. No se transmiten incapacidades, nombres ni folios a GitHub. El repositorio público contiene únicamente documentación, instaladores, checksums y metadatos de versión. Una actualización o desinstalación conserva los registros para prevenir pérdidas accidentales.

## Instalación y desinstalación

El instalador crea accesos directos en el escritorio y menú Inicio, registra la tarea del notificador y abre RECIN al finalizar. El desinstalador elimina aplicación, accesos directos, tarea y proceso en segundo plano, pero conserva los datos del usuario.

## Documentos relacionados

- [Lista completa de funcionalidades](FUNCIONALIDADES.md)
- [Manual de uso](USO.md)
- [Arquitectura](ARQUITECTURA.md)
- [Desarrollo](DESARROLLO.md)
- [Publicación de versiones](../RELEASING.md)
