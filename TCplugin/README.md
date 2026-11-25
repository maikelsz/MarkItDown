# MarkItDown para Total Commander

Plugin **WLX** de Total Commander para ver archivos Markdown (`.md`) dentro del Lister y del visor rápido. Es la versión 1.0.0 del visor MarkItDown adaptada a Total Commander: reutiliza el mismo parser y renderizador, pero es **solo lectura**.

## Características

- Visor nativo WLX de **64 bits** para `TOTALCMD64.EXE` (Total Commander 9.22a x64 o superior).
- Se activa únicamente para la extensión `.md` mediante la cadena de detección `EXT="MD"`.
- Renderizado Markdown con el mismo motor, CSS y resaltado que el visor de escritorio MarkItDown 1.0.0.
- Resaltado de código para C#, JavaScript, C/C++, BASIC, Pascal, Fortran, JSON, LEN y LEAL, entre otros; LEN y LEAL se muestran con sus mnemónicos, rotaciones, comentarios y números.
- Tema oscuro por defecto; también admite tema claro y seguimiento del tema de Windows.
- Funciona en el Lister normal (`F3`) y en el visor rápido (`Ctrl+Q`).
- `ListLoadNextW` reutiliza la misma ventana al cambiar de archivo con las flechas del panel.
- Los archivos que no son `.md` (por ejemplo `.txt`) vuelven al visor interno de Total Commander.
- Sin edición, sin panel de índice lateral, sin exportación HTML y sin procesos externos.
- Enlaces externos abiertos en el navegador; enlaces a otros `.md` abiertos en el mismo visor; otros archivos locales con su aplicación asociada.

## Archivos

| Archivo | Descripción |
| --- | --- |
| `MarkItDown.wlx` | Plugin WLX mixto C++/CLI con los exports nativos y la ventana WinForms/WebBrowser. |
| `MarkItDown.Core.dll` | Núcleo .NET Framework 4.6 con el parser y el renderizador Markdown. Debe estar en la misma carpeta que el `.wlx`. |
| `vcruntime140.dll` | Runtime de Visual C++ necesario si no está instalado el redistribuible 2015-2022. |

El plugin resuelve `MarkItDown.Core.dll` desde su propio directorio mediante `AssemblyResolve`, así que la carpeta puede estar en cualquier ruta.

## Instalación

1. Copia `MarkItDown.wlx`, `MarkItDown.Core.dll` y `vcruntime140.dll` a una carpeta estable, por ejemplo:

   ```text
   C:\totalcmd\plugin\
   ```

2. En Total Commander abre **Configuración → Opciones → Lister → Configurar plugins del Lister**.
3. Pulsa **Añadir**, selecciona `MarkItDown.wlx` y acepta. La cadena de detección debe ser:

   ```text
   EXT="MD"
   ```

4. Acepta y reinicia Total Commander.

También se puede instalar editando `wincmd.ini` con Total Commander cerrado:

```ini
[ListerPlugins]
0=C:\totalcmd\plugin\MarkItDown.wlx
0_detect=EXT="MD"

[ListerPlugins64]
0=1
```

> **Importante:** en Total Commander x64 el plugin debe estar marcado como 64 bits con `0=1` en `[ListerPlugins64]`. Sin esa marca, Total Commander ignora el plugin aunque esté en `[ListerPlugins]`. El valor `$checksum$` lo genera Total Commander sobre la sección `[ListerPlugins]`; no hay que escribirlo a mano. Si cambias a mano la ruta o la cadena de detección, el checksum deja de coincidir y Total Commander elimina la marca `0=1` al arrancar: vuelve a añadirla o usa el diálogo de configuración, que mantiene ambas secciones correctamente.

### Desinstalación

Elimina el plugin desde **Configuración → Opciones → Lister → Configurar plugins del Lister** y borra la carpeta donde copiaste los archivos. Si lo instalaste a mano, elimina la entrada de `[ListerPlugins]` y la marca correspondiente de `[ListerPlugins64]` con Total Commander cerrado.

## Uso

- **F3** sobre un `.md`: abre el Lister con MarkItDown.
- **Ctrl+Q** sobre un `.md`: muestra la vista rápida en el panel contrario.
- Flechas arriba/abajo en el panel: al pasar a otro `.md`, el visor se actualiza en la misma ventana.
- Al pasar a un archivo no Markdown, Total Commander usa su visor interno.
- **Esc** o el botón de cerrar del Lister vuelven al panel.

El título del Lister muestra `(markitdown)` en minúsculas porque Total Commander deriva ese texto del nombre del archivo. Es solo cosmético; la información de versión del DLL es `1.0.0.0` y la descripción `MarkItDown - Total Commander Lister plugin`.

## Tema

El plugin lee la preferencia de tema de:

```text
HKCU\Software\MarkItDown\Theme
```

Valores admitidos:

| Valor | Efecto |
| --- | --- |
| `dark` | Tema oscuro. Es el valor predeterminado si no existe la clave. |
| `light` | Tema claro. |
| `system` | Sigue el tema de aplicaciones de Windows. |

La preferencia es la misma que usa el visor de escritorio MarkItDown. El marco, los menús y la barra de estado de la ventana del Lister pertenecen a Total Commander y no cambian con este ajuste; el documento, los colores y la barra de desplazamiento del contenido sí.

Para fijar el tema claro desde la línea de comandos:

```bat
reg add "HKCU\Software\MarkItDown" /v Theme /t REG_SZ /d light /f
```

Para volver al oscuro:

```bat
reg delete "HKCU\Software\MarkItDown" /v Theme /f
```

## Requisitos

- Total Commander 9.22a x64 o superior, ejecutable `TOTALCMD64.EXE`.
- Windows con .NET Framework 4.6 o superior.
- Internet Explorer 11 instalado (motor del control WebBrowser).
- Visual C++ Redistributable 2015-2022 x64, o el `vcruntime140.dll` incluido.

El plugin configura automáticamente `FEATURE_BROWSER_EMULATION` para `TOTALCMD64.EXE` en el modo IE11 (`11001`), de modo que el renderizado sea consistente con el visor de escritorio.

## Compilación

Requisitos:

- Visual Studio 2019 con las cargas de trabajo **Desarrollo para el escritorio con C++** y **C++/CLI**.
- .NET SDK 3.1.201 (el que fija `global.json`) y el targeting pack de .NET Framework 4.6.

Desde la raíz de `TCplg`:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File .\build.ps1
```

El script:

1. Compila `MarkItDown.Core.dll` en Release.
2. Compila `Version.rc` y `MarkItDown.wlx` con `cl /clr` en x64.
3. Copia los resultados a `build\`.
4. Crea `dist\MarkItDown-1.0.0-wlx-x64\` y el ZIP correspondiente con el `.wlx`, el núcleo, `vcruntime140.dll` y este README.

Para compilar sin crear el paquete:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File .\build.ps1 -NoPackage
```

Cierra Total Commander y cualquier Lister abierto antes de recompilar: Windows bloquea `MarkItDown.Core.dll` mientras está cargado.

## Estructura del proyecto

```text
TCplg\
  build.ps1
  global.json
  README.md
  src\
    MarkItDown.Core\          Núcleo .NET (parser y renderizador)
    MarkItDown.Wlx\           WlxPlugin.cpp y Version.rc
  build\                      MarkItDown.wlx y MarkItDown.Core.dll
  dist\                       Paquete y ZIP listos para distribuir
  test\                       Harness nativo, plugin dummy y pruebas de TC
```

El núcleo enlaza los mismos archivos que el visor de escritorio:

- `MarkItDown\Markdown\*.cs`
- `MarkItDown\TextFileCodec.cs`
- `MarkItDown\Assets\github.css`, `github-dark.css` y `empty.svg`

## Pruebas realizadas

- Carga en el Lister de Total Commander 9.22a x64 con `F3` y título `Lister (markitdown)`.
- Vista rápida con `Ctrl+Q` y renderizado en el panel derecho.
- Instalación real en `C:\totalcmd\plugin\` con la marca `0=1` de `[ListerPlugins64]` y el checksum válido.
- Resaltado de LEN y LEAL en el Lister y en el visor rápido, incluidos mnemónicos, rotaciones, comentarios `/` y `;` y números `0x`/`0o`.
- `Esc` cierra el Lister y devuelve el foco al panel; `Ctrl+Q` alterna el visor rápido y `Esc` lo cierra.
- Desplazamiento del documento con `PageDown` en el Lister y en el visor rápido.
- Cambio de `sample.md` a `second.md` con las flechas del panel, reutilizando la ventana mediante `ListLoadNextW`.
- Cambio de `.md` a `.txt`: Total Commander vuelve a su visor interno.
- Redimensionado del Lister y cierre limpio de la ventana.
- Tema oscuro y tema claro dentro de Total Commander.
- Detección correcta de `.md` y rechazo de `.txt` en el harness nativo.
- Verificación de los seis exports: `ListLoad`, `ListLoadW`, `ListLoadNext`, `ListLoadNextW`, `ListCloseWindow` y `ListGetDetectString`.
- Comprobación de que el DLL es x64 (`machine=0x8664`).

## Solución de problemas

| Síntoma | Causa probable | Solución |
| --- | --- | --- |
| El plugin no aparece al pulsar F3 | Falta `0=1` en `[ListerPlugins64]` o Total Commander es de 32 bits. | Añade la marca con el diálogo de plugins o usa `TOTALCMD64.EXE`. |
| El Lister muestra una página en blanco | Falta `MarkItDown.Core.dll` junto al `.wlx` o no se puede cargar. | Copia el núcleo en la misma carpeta y revisa el log. |
| Error de `VCRUNTIME140.dll` | No está el redistribuible de Visual C++. | Copia `vcruntime140.dll` junto al plugin o instala el redistribuible x64. |
| El tema no cambia | La clave `Theme` no existe o tiene otro valor. | Usa `dark`, `light` o `system`; sin clave se aplica oscuro. |
| `TOTALCMD64.EXE /S=L` no carga el plugin | `/S=L` fuerza el visor interno del Lister. | Prueba con la ventana principal y `F3`, o con `Ctrl+Q`. |

Los errores del plugin se registran en:

```text
%LOCALAPPDATA%\MarkItDown\MarkItDown-wlx.log
```

## Diferencias con el visor de escritorio

| Función | Visor de escritorio | Plugin WLX |
| --- | --- | --- |
| Ver Markdown | Sí | Sí |
| Editar y guardar | Sí | No |
| Índice lateral | Sí | No |
| Exportar HTML | Sí | No |
| Vigilar cambios del archivo | Sí | No (se recarga al volver a abrir o navegar) |
| Imprimir | Sí | Mediante el menú contextual del WebBrowser |
| Extensiones admitidas | `.md`, `.markdown`, `.mdown`, etc. | Solo `.md` |

## Licencia

MIT. Copyright MaikelSZ, 2026.
