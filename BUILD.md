# Compilar Biblioteca_Back (jellyfin)

Fork del servidor de Jellyfin (C#/.NET). Ver CHANGES.md para los cambios
respecto a upstream. Rama base: release-12.z.

## Requisitos (una sola vez)

- .NET SDK 10.x  (`dotnet --list-sdks` debe mostrar un 10.x)
- Se instala con: `winget install Microsoft.DotNet.SDK.10`

Tras instalar, cerrar y reabrir la terminal. El global.json fija la 10 con
rollForward latestMinor.

## Compilar (publish para Windows)

```powershell
cd C:\Users\34674\Desktop\Mis_Proyectos\Mi_Biblioteca\Codigo\jellyfin
dotnet publish Jellyfin.Server\Jellyfin.Server.csproj -c Release -r win-x64 --self-contained false -o C:\Users\34674\Desktop\Mis_Proyectos\Mi_Biblioteca\build-out\server
```

- Las líneas `warning CS...` son normales.
- Éxito = `Compilación realizado correctamente`.
- Resultado: `build-out\server\` con jellyfin.exe y sus .dll.
- `--self-contained false` = usa el runtime .NET instalado (más ligero). Para un
  paquete que no dependa de .NET instalado: `--self-contained true`.

## Arrancar en modo prueba (sin tocar el Jellyfin real)

```powershell
cd C:\Users\34674\Desktop\Mis_Proyectos\Mi_Biblioteca\build-out\server
.\jellyfin.exe --datadir "C:\Users\34674\Desktop\Mis_Proyectos\Mi_Biblioteca\test-data" --webdir "C:\Users\34674\Desktop\Mis_Proyectos\Mi_Biblioteca\Codigo\jellyfin-web\dist"
```

- `--datadir` = carpeta de datos de prueba (config, base de datos), aislada de tu
  instalación real. `--webdir` = apunta al front recién compilado sin copiarlo.
- Abrir http://localhost:8096 . Parar con Ctrl+C.
- Aviso "Incompatibilidad de Servidor" en el navegador: es normal si antes
  visitaste tu Jellyfin real en ese puerto (el navegador recuerda el ID viejo).
  Pulsar "Conectar de todos modos".

## Empaquetado final (back + front juntos)

Para distribuir: copiar la carpeta `dist/` del front dentro de `build-out\server\`
con el nombre `jellyfin-web` (el servidor la busca ahí por defecto, sin --webdir).
