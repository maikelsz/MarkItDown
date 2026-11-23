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
- **Ver**: Aumentar zoom (`Ctrl++`), Reducir zoom (`Ctrl+-`), Tamaño normal (`Ctrl+0`), Tema y Cambios en el archivo.
- **Ayuda**: Acerca de MarkItDown.
- **Barra de estado**: ruta del archivo, número de líneas y palabras, estado de guardado y tema actual. Pulsa el tema para alternar entre claro y oscuro.
- **Índice**: panel estrecho a la izquierda con la lista de encabezados y su número. Se puede arrastrar el divisor para ajustar su ancho; el contenido conserva espacio suficiente para el editor y la vista previa. En modo vista, al pulsar una entrada el visor salta a esa sección. En modo edición, además coloca el cursor en la línea del encabezado y sincroniza la vista previa.
- Los enlaces externos se abren en el navegador predeterminado.
- Los enlaces a otros archivos Markdown se abren dentro del visor; los demás archivos locales se abren con la aplicación asociada.

## Edición

### Entrar y salir

Pulsa `F2` o usa **Archivo → Editar documento** para abrir el editor. La ventana muestra tres zonas:

- **Índice**: panel estrecho a la izquierda con la lista de encabezados.
- **Centro**: editor de texto con resaltado Markdown.
- **Derecha**: vista previa renderizada.

El divisor entre el editor y la vista previa se puede arrastrar. El editor conserva un ancho mínimo de 300 px y la vista previa de 280 px. El panel del índice sigue visible a la izquierda y su divisor también se puede arrastrar. Para volver al modo vista, pulsa `F2` de nuevo.

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
- Bloques de código cercados e indentados, con resaltado para C#, JavaScript/TypeScript, JSON, XML/HTML, CSS, SQL, PowerShell, batch, diff y otros lenguajes habituales.
- Notas al pie con enlaces de ida y vuelta.
- Emoji corto, por ejemplo `:rocket:`.
- Front matter YAML oculto en la vista.
- HTML crudo seguro, incluidas etiquetas como `details` y `summary`.

El HTML crudo se sanea: se eliminan scripts, atributos `on*`, URLs `javascript:` y estilos en línea. Las etiquetas y atributos seguros se conservan.

### Índice y enlaces internos

El índice se genera automáticamente después del primer `H1` cuando hay al menos dos encabezados y el documento no incluye un marcador. Para controlar su posición, escribe `[TOC]` o `[[_TOC_]]` en el lugar deseado.

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

## Estructura del proyecto

- `MainForm.cs`: ventana principal, carga, navegación, zoom, temas, recarga, vigilancia del archivo, modo edición, divisor del índice y sincronización del cursor.
- `TocPanel.cs`: panel del índice, lista con dibujo propio, selección y temas.
- `MarkdownEditor.cs`: editor `RichTextBox`, resaltado Markdown, continuación de listas y eventos de cursor.
- `EditSession.cs`: copia temporal, recuperación, guardado y detección de conflictos.
- `TextFileCodec.cs`: codificación, BOM, saltos de línea y escritura atómica.
- `SaveChangesDialog.cs`: diálogo temático Guardar/Descartar/Cancelar.
- `FileChangedDialog.cs`: aviso temático de archivo modificado.
- `DarkChrome.cs`: barra de título, menús, barra de estado y scrollbar de IE.
- `ThemeManager.cs`: preferencia y detección del tema del sistema.
- `Markdown/`: parser, renderizador, saneador, resaltador y exportador.
- `Assets/`: hojas de estilo, icono y estado vacío.
- `test/`: documento de prueba, exportaciones, capturas y scripts de validación.

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
