# RECIN Releases

Canal público oficial de instaladores y actualizaciones de **RECIN — Recordatorio de Incapacidades**.

Este repositorio no contiene el código fuente ni datos de usuarios. Su única función es distribuir:

- El instalador más reciente para Windows x64.
- Releases versionados.
- El manifiesto `latest.json` utilizado por el actualizador automático.
- El checksum SHA-256 del instalador.

## Descargar

La opción recomendada es descargar la versión más reciente desde la sección [Releases](../../releases/latest).

El archivo `RECIN-windows-amd64-installer.exe` de la rama `main` siempre corresponde a la actualización más reciente.

## Verificar la descarga

En PowerShell:

```powershell
Get-FileHash .\RECIN-windows-amd64-installer.exe -Algorithm SHA256
```

El resultado debe coincidir con el valor publicado en `SHA256SUMS.txt`.

## Actualizaciones automáticas

RECIN consulta `latest.json` al iniciar. Cuando existe una versión posterior, solicita confirmación, descarga el instalador desde este repositorio y ejecuta la actualización silenciosa.

## Privacidad

Los registros de incapacidades permanecen únicamente en el equipo del usuario. RECIN no los envía a este repositorio ni a GitHub.
