# MarkItDown

MarkItDown 1.0.0 es un visor y editor de Markdown rápido y ligero para Windows, con apariencia GitHub, tema oscuro por defecto y exportación a HTML autónomo.

- C# / .NET Framework 4.6, WinForms y el motor WebBrowser de Windows.
- Sin paquetes NuGet ni dependencias externas: parser, resaltador, temas, editor y exportador propios.
- Modo vista y modo edición con el editor a la izquierda y la vista previa a la derecha.
- El visor sigue automáticamente al cursor del editor.
- Texto seleccionable y copiable, índice con enlaces internos y ventana completa en altura.
- Vigila el archivo abierto y permite preguntar, recargar siempre o no recargar los cambios.

## Características

- Renderizado de Markdown con estilos claros y oscuros inspirados en GitHub.
- Tema oscuro predeterminado. También ofrece **Sistema**, **Claro** y **Oscuro**.
- Toda la ventana acompaña al tema: barra de título, menús, desplegables, barra de estado, editor y aviso de archivo modificado.
- La ventana se abre con 1100 px de ancho (o el ancho de la pantalla si es menor) y toda la altura útil, centrada y sin maximizar.
- Apertura desde la línea de comandos y arrastrando archivos `.md` sobre la ventana o el ejecutable.
- Índice/TOC automático, anidado y con enlaces internos.
- Panel de índice estrecho a la izquierda, siempre visible, para saltar a cualquier sección en modo vista o edición.
- Exportación a un único HTML autónomo, con CSS e imágenes locales incrustadas.
- Vigilancia del archivo abierto con tres modos que solo duran la sesión actual.
- Zoom, impresión, recarga manual y barra de estado con líneas y palabras.
- Modo edición con resaltado de sintaxis Markdown, vista previa en vivo y guardado con `Ctrl+S`.
- El editor está a la izquierda y la vista previa a la derecha. Al mover el cursor, el visor se desplaza al bloque equivalente.
- Alineación bidireccional: al pulsar en el editor, el visor coloca la línea correspondiente a la misma altura; al pulsar en el visor, el editor salta a esa línea. Solo una selección explícita de texto resalta el bloque o rango equivalente en el panel contrario; un clic simple no marca nada y borra la selección anterior en ambos paneles.
- Marcadores Markdown con estilo: `#` en negrita y color del encabezado, `**Negrita**` en negrita, `*cursiva*` en cursiva y `~~tachado~~` tachado, tanto en el texto como en los marcadores.
- Normalización automática del código al definir un bloque cercado: BASIC, Fortran, SQL, LEN y LEAL en mayúsculas; Pascal en minúsculas; Visual Basic con grafía canónica; `true`/`false`/`null` de JSON en minúsculas.
- Doble clic en el divisor editor/visor restaura el reparto 50/50; doble clic en el divisor del índice lo devuelve a su ancho mínimo.
- Copia temporal automática para recuperar cambios tras un cierre inesperado.
- Continuación automática de listas, listas de tareas y citas al pulsar `Enter`.
- Exportación desde el editor con el texto actual, aunque todavía no se haya guardado.

## Requisitos

- Windows con .NET Framework 4.6 o superior.
- Internet Explorer 11 instalado (es el motor que usa el control WebBrowser).
- Visual Studio 2019 o el SDK de .NET Core 3.1.201, que es el que fija `global.json`.

## Compilación

Con Visual Studio 2019:

1. Abre `MarkItDown.sln`.
2. Selecciona **Release** y compila.
3. El ejecutable queda en `bin\Release\net46\MarkItDown.exe`.

Con la línea de comandos:

```bat
dotnet build MarkItDown.csproj -c Release
```

## Uso

```bat
MarkItDown.exe
MarkItDown.exe documento.md
MarkItDown.exe --export salida.html documento.md
MarkItDown.exe --export salida.html documento.md --theme dark
MarkItDown.exe --theme light documento.md
MarkItDown.exe --help
MarkItDown.exe --version
```

Opciones:

| Opción | Descripción |
| --- | --- |
| `-e`, `--export <archivo.html>` | Exporta el Markdown a un HTML autónomo. |
| `-t`, `--theme <modo>` | Tema para esta ejecución: `dark`, `light` o `system`. |
| `-h`, `--help` | Muestra la ayuda. |
| `-v`, `--version` | Muestra la versión. |

Si no se indica `--theme`, se usa la preferencia guardada. En la primera ejecución el tema es **oscuro**. La opción `--theme` no modifica la preferencia guardada.

También puedes arrastrar un archivo Markdown sobre la ventana del visor o sobre el ejecutable. Se admiten `.md`, `.markdown`, `.mdown`, `.mkd`, `.mdwn`, `.mdtxt` y `.mdtext`.

## Interfaz

- **Archivo**: Abrir (`Ctrl+O`), Recargar (`F5`), Editar documento (`F2`), Guardar (`Ctrl+S`), Exportar HTML (`Ctrl+E`), Imprimir (`Ctrl+P`) y Salir.
- **Ver**: Aumentar zoom (`Ctrl++`), Reducir zoom (`Ctrl+-`), Tamaño normal (`Ctrl+0`), **Índice en el documento** (alterna la TOC generada dentro del contenido), Tema y Cambios en el archivo.
- **Ayuda**: Acerca de MarkItDown.
- **Barra de estado**: ruta del archivo, número de líneas y palabras, estado de guardado y tema actual. Pulsa el tema para alternar entre claro y oscuro.
- **Índice**: panel estrecho a la izquierda con la lista de encabezados y su número. Se puede arrastrar el divisor para ajustar su ancho; el contenido conserva espacio suficiente para el editor y la vista previa. En modo vista, al pulsar una entrada el visor salta a esa sección. En modo edición, además coloca el cursor en la línea del encabezado y sincroniza la vista previa.
- Los enlaces externos se abren en el navegador predeterminado.
- Los enlaces a otros archivos Markdown se abren dentro del visor; los demás archivos locales se abren con la aplicación asociada.

## Edición

El editor usa la fuente **Segoe UI Symbol** para soportar caracteres no ASCII (CJK, árabe, matemáticas, símbolos de caja) y emoji; Windows aplica *font fallback* automático por glifo para cualquier carácter que la fuente base no incluya.

### Entrar y salir

Pulsa `F2` o usa **Archivo → Editar documento** para alternar entre tres estados:

| Estado | Vistas visibles | F2 pasa a |
| --- | --- | --- |
| **Visor solo** (inicial) | Visor | Editor + Visor |
| **Editor + Visor** | Editor + vista previa en vivo | Solo Editor |
| **Solo Editor** | Editor (vista previa oculta) | Visor solo |

- En **Visor solo** la ventana muestra el índice a la izquierda y el visor a la derecha.
- En **Editor + Visor** se añade el editor a la izquierda del visor; la vista previa se actualiza en vivo y el visor sigue al cursor.
- En **Solo Editor** la vista previa se oculta y no se actualiza; el editor ocupa todo el ancho.
- Al volver a **Visor solo** desde **Solo Editor**, el visor se re-renderiza con el documento actual (incluidos los cambios hechos en el editor) para quedar sincronizado.

El divisor entre el editor y la vista previa se puede arrastrar. El editor conserva un ancho mínimo de 300 px y la vista previa de 280 px. El panel del índice sigue visible a la izquierda y su divisor también se puede arrastrar.

Si hay cambios sin guardar al presionar `F2` desde **Solo Editor** hacia **Visor solo**, aparece el diálogo de guardado habitual.

### Guardado y conflictos

- `Ctrl+S` guarda el archivo con la codificación, el BOM y los saltos de línea originales.
- Mientras haya cambios sin guardar, el título muestra un asterisco y la barra de estado indica **Sin guardar**.
- Si el archivo cambió en el disco o se eliminó mientras editabas, el visor pide confirmación antes de sobrescribirlo o recrearlo.
- Al salir del modo edición o cerrar la ventana con cambios pendientes aparece un diálogo con **Guardar**, **Descartar** y **Cancelar**.

### Copia temporal y recuperación

Mientras hay cambios sin guardar, el editor escribe una copia temporal en:

```text
%LOCALAPPDATA%\MarkItDown\Sesiones
```

La copia se actualiza poco después de dejar de escribir y se elimina al guardar o descartar. Si el proceso se cierra de forma inesperada, al volver a abrir el mismo archivo el visor ofrece recuperar el texto pendiente. La copia conserva la codificación, el BOM y el tipo de salto de línea del archivo original.

### Vista previa y seguimiento del cursor

La vista previa se actualiza unos 350 ms después de la última pulsación. Cada bloque renderizado conserva su línea de origen mediante atributos internos, de modo que al mover el cursor el visor se desplaza al bloque equivalente:

- Al inicio del documento se muestra el principio.
- En medio de un documento se muestra la sección correspondiente.
- Al final se muestra el cierre y las notas al pie.
- Al escribir o deshacer, la vista previa se vuelve a renderizar y sigue al cursor.

Los atributos de sincronización y el script que los usa solo existen en la vista previa. La exportación HTML no los incluye.

### Sincronización bidireccional

- **Editor → visor**: al mover el cursor, el visor se desplaza al bloque equivalente sin resaltarlo. Solo cuando se selecciona texto de forma explícita se resaltan los bloques correspondientes y se desplaza la línea activa a la misma proporción vertical de la ventana (no la fija al borde superior).
- **Visor → editor**: un clic en un bloque del visor mueve el cursor del editor a la línea de origen, la coloca a la altura proporcional y borra cualquier selección anterior en ambos paneles; el clic nunca selecciona la línea pulsada. Arrastrar para seleccionar texto en el visor sí selecciona el rango de líneas correspondiente en el editor.
- Las selecciones usan el resaltado `visor-source-selected` en la vista previa; los enlaces e imágenes no activan la sincronización.
- El resaltado del visor y la selección del editor representan únicamente la selección explícita activa: al hacer clic en cualquier otro punto del documento, ambas desaparecen. Si el punto corresponde a una línea de texto, el cursor se desplaza a ella; en enlaces, imágenes y márgenes solo se limpia la selección.
- El puente solo se instala en la vista previa. El HTML exportado no contiene scripts ni atributos de sincronización.

### Marcadores y formato en el editor

El editor muestra el Markdown con formato parcial para que el documento sea legible sin ocultar la sintaxis:

- El `#` de los encabezados se dibuja en negrita y con el mismo color que el texto del encabezado.
- El texto entre `**...**` se muestra en negrita y el texto entre `*...*` en cursiva; `~~...~~` se muestra tachado. Los marcadores conservan su color de sintaxis.
- El resaltado de bloques cercados reconoce C#, JavaScript/TypeScript, C/C++, BASIC, Pascal, Fortran, JSON, LEN y LEAL, entre otros.

### Normalización automática del código

Al definir o editar un bloque cercado, el contenido se normaliza según el lenguaje (unos 500 ms después de la última pulsación; el bloque que contiene el cursor se respeta hasta que se fuerza la normalización):

| Lenguaje | Convención aplicada |
| --- | --- |
| BASIC, Fortran, SQL, LEN, LEAL, batch, Dockerfile | Palabras clave en MAYÚSCULAS |
| Pascal, INI | Palabras clave en minúsculas |
| Visual Basic | Grafía canónica de cada palabra clave |
| JSON | `true`, `false` y `null` en minúsculas |

Los lenguajes sensibles a mayúsculas (C#, JavaScript, C/C++, Python, etc.) no se modifican. **Archivo → Normalizar código** fuerza la normalización de todos los bloques y también se aplica antes de guardar.

### Divisores

- Doble clic en el divisor entre editor y vista previa: reparto 50/50.
- Doble clic en el divisor del panel del índice: el índice vuelve a su ancho mínimo.
- Los límites de arrastre siguen siendo 300 px para el editor, 280 px para la vista previa y el ancho mínimo del índice.

### Índice y navegación

El panel de la izquierda se actualiza con la vista previa: al añadir, cambiar o eliminar un encabezado, la lista y el contador se actualizan en unos 350 ms. Las entradas largas se recortan con puntos suspensivos.

- En modo vista, un clic desplaza el visor a la sección.
- En modo edición, un clic mueve el cursor del editor a la línea del encabezado y la vista previa al bloque correspondiente.
- Al mover el cursor o usar `Ctrl+Home`/`Ctrl+End`, el índice resalta la sección actual.
- `Enter` sobre una entrada seleccionada también navega a ella.

El índice lateral es independiente del índice que se puede insertar en el documento con `[TOC]`: el lateral siempre está disponible y no forma parte del HTML exportado.

### Ayudas del editor

- `Enter` dentro de una lista crea el siguiente elemento con la misma indentación y numeración.
- `Enter` dentro de una cita continúa la cita.
- `Enter` sobre un elemento vacío elimina el marcador para terminar la lista o la cita.
- `Ctrl+Z` y `Ctrl+Y` deshacen y rehacen cambios de texto; el resaltado de sintaxis no contamina el historial.

## Cambios en el archivo

El visor vigila el archivo abierto y reacciona cuando cambia en disco. En **Ver → Cambios en el archivo** hay tres modos:

- **Preguntar** (predeterminado): muestra un aviso con las opciones **Recargar**, **Recargar siempre** y **No recargar**.
- **Recargar automáticamente**: refresca el documento sin preguntar.
- **No recargar**: mantiene la vista actual; puedes actualizarla manualmente con `F5`.

La elección se guarda solo en memoria: al cerrar y volver a abrir el visor se vuelve a **Preguntar**. No se escribe nada en el registro para este ajuste.

Al recargar se conserva la posición de desplazamiento. Si el cambio modifica la altura del contenido situado por encima de la zona visible (por ejemplo, al añadir una entrada al TOC), la posición se mantiene en píxeles y el contenido puede desplazarse ligeramente. Si el archivo se elimina, la barra de estado lo indica; si vuelve a aparecer, se recarga según el modo elegido.

Mientras el modo edición está activo, la vigilancia del archivo se pausa para no interferir con los cambios locales.

## Markdown compatible

- Encabezados ATX y Setext.
- Negrita, cursiva, texto tachado y código en línea.
- Enlaces, autollenlaces, imágenes locales y remotas.
- Listas ordenadas y no ordenadas, anidadas y listas de tareas.
- Tablas con alineación de columnas.
- Citas y alertas de GitHub: `[!NOTE]`, `[!TIP]`, `[!IMPORTANT]`, `[!WARNING]` y `[!CAUTION]`.
- Bloques de código cercados e indentados, con resaltado para C#, JavaScript/TypeScript, C/C++, BASIC (incluido el BASIC clásico con número de línea), Pascal, Fortran, JSON, LEN, LEAL, XML/HTML, CSS, SQL, PowerShell, batch, diff y otros lenguajes habituales.
- LEN unifica LEN-1 y LEN-B (mnemónicos, rotaciones `RI1`–`RI15`/`RD1`–`RD15`, comentarios con `/`, cadenas con comillas simples o dobles y números `0o`/`0d`/`0x`). LEAL unifica LEAL-A y LEAL-B (43 palabras reservadas, comentarios con `;` y operadores `+ - : / ? =`). Ambos son insensibles a mayúsculas.
- Notas al pie con enlaces de ida y vuelta.
- Emoji corto, por ejemplo `:rocket:`.
- Front matter YAML oculto en la vista.
- HTML crudo seguro, incluidas etiquetas como `details` y `summary`.

El HTML crudo se sanea: se eliminan scripts, atributos `on*`, URLs `javascript:` y estilos en línea. Las etiquetas y atributos seguros se conservan.

### Índice y enlaces internos

El índice se genera automáticamente después del primer `H1` cuando hay al menos dos encabezados y el documento no incluye un marcador. Para controlar su posición, escribe `[TOC]` o `[[_TOC_]]` en el lugar deseado.

La TOC dentro del contenido está oculta por defecto. Para mostrarla, marca **Ver → Índice en el documento**; para ocultarla, desmarca la misma opción. El cambio preserva la posición de scroll del visor.

Los encabezados reciben identificadores únicos y el índice enlaza con ellos. Los enlaces internos como `[Ir a la tabla](#tabla)` funcionan tanto en el visor como en el HTML exportado. El panel lateral del visor usa esta misma lista de encabezados para navegar, pero no se incluye en la exportación.

## Exportación HTML

```bat
MarkItDown.exe --export salida.html documento.md --theme dark
```

El resultado es un único archivo HTML que funciona sin el visor:

- CSS del tema elegido incrustado en el documento.
- Imágenes locales convertidas a data URI.
- Enlaces relativos conservados.
- Sin scripts, anclas internas de sincronización ni recursos externos.
- Desplazamiento normal del navegador, también en el archivo exportado.

Si se exporta desde el modo edición, se usa el texto actual del editor, incluidos los cambios que todavía no se han guardado. Si no se indica `--theme`, se usa la preferencia actual. La exportación no cambia esa preferencia.

## Tema y apariencia

El tema oscuro es el predeterminado. El cambio de tema afecta al documento, al editor y a toda la interfaz: barra de título, menús, desplegables, barra de estado y el diálogo de archivo modificado. La preferencia de tema se guarda en `HKCU\Software\MarkItDown\Theme`.

En Windows 10 y 11 la barra de título se oscurece mediante la API DWM. En versiones anteriores el documento y los controles siguen el tema, pero la barra de título puede quedar con el estilo del sistema.

## Plugin para Total Commander

MarkItDown 1.0.0 incluye un plugin **WLX de 64 bits** para Total Commander, ubicado en `TCplg/`. Permite ver archivos `.md` directamente en el Lister (`F3`) y en el visor rápido (`Ctrl+Q`) con el mismo renderizador, temas y resaltado del visor de escritorio, pero en modo solo lectura.

### Instalación

1. Copia `MarkItDown.wlx`, `MarkItDown.Core.dll` y `vcruntime140.dll` desde `TCplg\dist\MarkItDown-1.0.0-wlx-x64\` a una carpeta estable, por ejemplo `C:\totalcmd\plugin\`.
2. En Total Commander abre **Configuración → Opciones → Lister → Configurar plugins del Lister → Añadir**.
3. Selecciona `MarkItDown.wlx` y usa la cadena de detección `EXT="MD"`.
4. Acepta y reinicia Total Commander.

En Total Commander x64 el plugin debe quedar marcado como 64 bits (`0=1` en `[ListerPlugins64]`); el diálogo de configuración lo hace automáticamente. Si se edita `wincmd.ini` a mano, sin esa marca el plugin se ignora aunque esté registrado en `[ListerPlugins]`. El valor `$checksum$` lo genera Total Commander y no se escribe a mano. Si cambias la ruta o la cadena de detección manualmente, Total Commander recalcula el checksum y elimina `0=1`; vuelve a añadir la marca o usa el diálogo de configuración.

### Uso

- `F3` sobre un `.md`: abre el Lister con MarkItDown.
- `Ctrl+Q` sobre un `.md`: muestra la vista rápida en el panel contrario.
- Flechas del panel: al cambiar entre archivos `.md`, `ListLoadNextW` reutiliza la misma ventana; al pasar a otro tipo de archivo, Total Commander vuelve a su visor interno.
- El título del Lister muestra `(markitdown)` en minúsculas porque Total Commander deriva ese texto del nombre del archivo; la versión real del DLL es `1.0.0.0`.

### Tema

El plugin lee `HKCU\Software\MarkItDown\Theme` (`dark`, `light` o `system`), la misma preferencia que el visor de escritorio. Sin valor, usa oscuro. El marco, los menús y la barra de estado del Lister pertenecen a Total Commander; el documento y su barra de desplazamiento siguen el tema elegido.

### Alcance

El plugin es solo visor: no edita, no guarda, no exporta HTML, no muestra el panel lateral de índice ni vigila cambios en disco. Solo se activa para `.md` (no para `.markdown` ni las demás extensiones del visor de escritorio). Los enlaces externos se abren en el navegador; los enlaces a otros `.md` se abren en el mismo Lister; otros archivos locales se abren con su aplicación asociada.

### Compilación y pruebas

El plugin se compila con `TCplg\build.ps1` (Visual Studio 2019 con C++/CLI y .NET SDK 3.1.201). Genera `MarkItDown.wlx` x64, `MarkItDown.Core.dll` y un ZIP en `TCplg\dist\`. Los detalles de instalación, compilación, solución de problemas y pruebas están en `TCplg\README.md`.

Se validó en Total Commander 9.22a x64 con el plugin instalado en `C:\totalcmd\plugin\`: `F3` y `Ctrl+Q`, resaltado de LEN y LEAL en ambos modos, desplazamiento con `PageDown`, cierre con `Esc`, cambio entre dos `.md`, vuelta al visor interno con `.txt`, redimensionado y temas oscuro y claro.

## Estructura del proyecto

- `MainForm.cs`: ventana principal, carga, navegación, zoom, temas, recarga, vigilancia del archivo, modo edición, divisor del índice, sincronización bidireccional y normalización.
- `TocPanel.cs`: panel del índice, lista con dibujo propio, selección y temas.
- `MarkdownEditor.cs`: editor `RichTextBox`, formato de marcadores, resaltado Markdown y de código, continuación de listas y eventos de cursor.
- `VisorScriptBridge.cs`: puente COM entre la vista previa y el editor para clics y selecciones.
- `EditSession.cs`: copia temporal, recuperación, guardado y detección de conflictos.
- `TextFileCodec.cs`: codificación, BOM, saltos de línea y escritura atómica.
- `SaveChangesDialog.cs`: diálogo temático Guardar/Descartar/Cancelar.
- `FileChangedDialog.cs`: aviso temático de archivo modificado.
- `DarkChrome.cs`: barra de título, menús, barra de estado y scrollbar de IE.
- `ThemeManager.cs`: preferencia y detección del tema del sistema.
- `Markdown/`: parser, renderizador, saneador, resaltador, normalizador de código y exportador.
- `Assets/`: hojas de estilo, icono y estado vacío.
- `test/`: documento de prueba, exportaciones, capturas y scripts de validación.
- `TCplg/`: plugin WLX para Total Commander, con fuentes, `build.ps1`, paquete y pruebas propias.

## Pruebas

Para reexportar el documento de prueba y validar ambos temas:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File .\test\verify-export.ps1
```

El script comprueba, entre otras cosas:

- 11 encabezados con identificadores únicos y 11 enlaces de TOC con destino válido.
- Enlace `#tabla` presente y resuelto.
- Ausencia de scripts, `javascript:` y atributos `on*`.
- Front matter oculto.
- 2 alertas, 1 tabla, notas al pie y tokens de resaltado.
- Imagen local incrustada como data URI.
- CSS del tema correspondiente y ausencia de recursos externos.

Resultado de la última ejecución: **todas las comprobaciones pasan** para `sample-dark.html` y `sample-light.html`.

La interfaz se valida además con un arnés que ejecuta el visor real alojado en PowerShell y comprueba el editor, el resaltado y la sincronización:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File .\test\ui_sync_verify.ps1
```

Resultado de la última ejecución: **83 comprobaciones correctas, 0 fallos**. Incluye:

- Marcadores `#`, `**Negrita**`, `*cursiva*` y `~~tachado~~` con el estilo esperado.
- Tokens de código y resaltado en el visor para C#, JavaScript, C++, BASIC, Pascal, Fortran y JSON.
- Resaltado de LEN y LEAL (mnemónicos, rotaciones, comentarios y números) y normalización a mayúsculas.
- Alineación editor → visor por proporción vertical y resaltado solo con selección explícita.
- Clic y selección visor → editor a través del puente `window.external`: el clic mueve y desmarca ambos paneles; la selección marca el rango.
- Un clic posterior a una selección borra el resaltado del visor y la selección del editor, y mover el cursor sin seleccionar no marca nada.
- Un clic en un margen sin bloque de origen o en un enlace/imagen también borra la selección de ambos paneles; en enlaces e imágenes el cursor no se mueve.
- Doble clic en ambos divisores (50/50 y ancho mínimo del índice).
- Ciclo F2 de tres estados, TOC en el documento y sincronización al volver a editar.
- Emoji, CJK, árabe, matemáticas y caracteres de caja en editor y visor.
- Normalización automática de BASIC, Fortran, Pascal, JSON y Visual Basic, incluido el respeto al bloque con el cursor y la normalización forzada.

También se probó en el visor real:

- Aviso **Preguntar** con recarga aceptada y rechazada.
- **Recargar siempre** desde el aviso y desde el menú, sin volver a preguntar.
- **No recargar** desde el menú, manteniendo el contenido anterior.
- Reinicio del visor: el modo vuelve a **Preguntar** (no se persiste).
- Conservación exacta de la posición de lectura cuando el contenido superior no cambia de altura.
- Diálogo oscuro y claro según el tema.
- Guardado normal con codificación, BOM y saltos de línea preservados.
- Copia temporal creada, eliminada al guardar/descartar y recuperada tras cerrar el proceso de forma forzada.
- Conflictos por cambio externo y archivo eliminado, con sobrescritura o recreación confirmadas.
- Diálogos **Guardar/Descartar/Cancelar** al salir del modo edición y al cerrar.
- Undo/redo sin contaminación del resaltado y continuación automática de listas.
- Desplazamiento del visor al inicio, mitad y final según el cursor.
- Seguimiento del cursor al escribir y al deshacer en la vista previa.
- Navegación desde el panel del índice en modo vista y edición, con el cursor y la vista previa sincronizados.
- Actualización del índice al añadir un encabezado nuevo (de 11 a 12 entradas).
- Resaltado de la sección actual al mover el cursor y después de `Ctrl+Home`/`Ctrl+End`.
- Anchos mínimos en edición: índice 166 px, editor 300 px y visor 286 px con una ventana de 780 px; al ensanchar, el índice vuelve a 220 px.
- Exportación desde el editor con cambios sin guardar, sin anclas ni scripts en el HTML.
- Ciclo F2 de tres estados: visor solo → editor + visor → solo editor → visor solo (con sincronización del documento al volver).
- TOC en el documento: alternar desde el menú **Ver → Índice en el documento** muestra/oculta el índice con la posición de scroll conservada.
- Editor con fuente Segoe UI Symbol: emoji, CJK, árabe y símbolos matemáticos se renderizan correctamente sin caer en `?`.
- `demo-full.md` con ejemplos de LEN y LEAL: etiquetas, comentarios `/` y `;`, rotaciones, cadenas, números `0o`/`0d`/`0x` y operadores de LEAL resaltados en el visor y en el editor.
- Clic en el visor sobre una línea del documento: el editor mueve el cursor a esa línea y la coloca a la altura proporcional, sin seleccionarla y borrando cualquier marca anterior; selección de varias líneas en el visor y reflejo del rango en el editor; un clic posterior borra la selección en ambos paneles.
- Marcadores de encabezado, negrita, cursiva y tachado visibles con su color y estilo en el editor.
- Normalización automática al crear bloques BASIC, Fortran, Pascal, JSON, Visual Basic, LEN y LEAL; **Archivo → Normalizar código** fuerza todos los bloques.

Capturas disponibles en `test/`:

- `viewer-dark-fullheight.png`: tema oscuro a altura completa.
- `viewer-light-final.png`: tema claro.
- `viewer-edit-dark.png`: modo edición con editor a la izquierda y vista previa a la derecha.
- `viewer-edit-light.png`: modo edición en tema claro.
- `about-dark.png`: diálogo Acerca de con la versión 1.0.0 y el autor.
- `viewer-split-min-editor-dark.png` y `viewer-split-min-preview-dark.png`: anchos mínimos del divisor.
- `sync-home-dark.png`, `sync-middle-dark.png` y `sync-end-dark.png`: seguimiento del cursor al inicio, en medio y al final.
- `sync-typed-dark.png` y `sync-undone-dark.png`: vista previa tras escribir y tras deshacer.
- `viewer-dark-menu.png`: menú Ver con el submenú de cambios en el archivo.
- `viewer-watch-prompt.png` y `viewer-watch-prompt-light.png`: aviso de archivo modificado.
- `viewer-watch-reloaded.png`: documento recargado.
- `viewer-watch-auto.png` y `viewer-watch-menu-auto.png`: recarga automática.
- `viewer-watch-scroll-before.png` y `viewer-watch-scroll-after.png`: conservación del desplazamiento.
- `toc-view-dark.png` y `toc-view-light.png`: panel del índice en modo vista.
- `toc-nav-codigo-dark.png` y `toc-nav-final-dark.png`: navegación a una sección intermedia y al final.
- `toc-edit-initial-dark.png` y `toc-edit-light.png`: modo edición con el panel del índice.
- `toc-edit-light-newheading.png`: índice actualizado tras añadir un encabezado.
- `toc-edit-light-minwidth.png` y `toc-edit-light-restored.png`: anchos mínimos y restauración del ancho.
- `toc-focus-last-dark.png`, `toc-focus-home-dark.png` y `toc-focus-end-dark.png`: resaltado de la sección actual al mover el cursor.
- `lenleal-view-dark.png`: visor con LEN y LEAL resaltados.
- `lenleal-edit-dark.png`: editor y visor con LEN y LEAL, marcadores de encabezado/negrita/cursiva y sincronización.

## Limitaciones

- El motor es Internet Explorer 11. No se usan variables CSS, `:has`, `position: sticky` ni otras características modernas.
- La barra de desplazamiento nativa de IE puede seguir viéndose clara en algunos equipos aunque el resto de la ventana sea oscuro; es una limitación del control.
- La impresión utiliza el diálogo y la vista previa de IE.
- El zoom es cosmético y va del 50 % al 300 %.
- El editor es un `RichTextBox`: el resaltado se aplica por líneas y se omite en documentos de más de 400.000 caracteres para mantener la respuesta.
- El seguimiento del cursor es por bloques. Dentro de un bloque muy largo, como un párrafo o un bloque de código de muchas líneas, el visor mantiene el inicio del bloque.
- El panel del índice solo muestra encabezados Markdown; no incluye encabezados escritos dentro de HTML crudo ni se puede contraer.
- El modo edición trabaja con un archivo cada vez; no hay pestañas ni edición de varios documentos a la vez.
- La copia temporal protege ante cierres inesperados, pero no sustituye a guardar el archivo.
- La detección de cambios depende del sistema de archivos y del editor. Si un cambio no se detecta, `F5` recarga manualmente.

## Licencia

MIT.
