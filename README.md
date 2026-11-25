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
- Normalización automática del código al definir un bloque cercado, activable en **Editar → Normalizar código**: BASIC, Fortran, SQL, LEN y LEAL en mayúsculas; Pascal en minúsculas; Visual Basic con grafía canónica; `true`/`false`/`null` de JSON en minúsculas.
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

- **Archivo**: Abrir (`Ctrl+O`), Recargar (`F5`), Guardar (`Ctrl+S`), Exportar HTML (`Ctrl+E`), Imprimir (`Ctrl+P`) y Salir.
- **Ver**: Aumentar zoom (`Ctrl++`), Reducir zoom (`Ctrl+-`), Tamaño normal (`Ctrl+0`), **Índice en el documento** (`F3`, alterna la TOC generada dentro del contenido), **Resaltar código en bloques del editor**, Tema (`F2`, alterna claro/oscuro) y Cambios en el archivo.
- **Editar**: **Editar documento** (`F4`) y **Normalizar código**, con las opciones **Automáticamente** (activable) y **Normalizar ahora** (una sola vez).
- **Ayuda**: Acerca de MarkItDown.
- **Opciones guardadas**: el índice en el documento, el tema, el resaltado de código del editor y la normalización automática se conservan entre ejecuciones en `HKCU\Software\MarkItDown`. Los tres modos de vigilancia del archivo siguen siendo solo de la sesión actual.
- **Barra de estado**: ruta del archivo, número de líneas y palabras, estado de guardado y tema actual. Pulsa el tema para alternar entre claro y oscuro.
- **Índice**: panel estrecho a la izquierda con la lista de encabezados y su número. Se puede arrastrar el divisor para ajustar su ancho; el contenido conserva espacio suficiente para el editor y la vista previa. En modo vista, al pulsar una entrada el visor salta a esa sección. En modo edición, además coloca el cursor en la línea del encabezado y sincroniza la vista previa.
- Los enlaces externos se abren en el navegador predeterminado.
- Los enlaces a otros archivos Markdown se abren dentro del visor; los demás archivos locales se abren con la aplicación asociada.

### Atajos

| Atajo | Acción |
| --- | --- |
| `F2` | Alterna entre tema oscuro y claro. |
| `F3` | Muestra u oculta el índice generado dentro del documento. |
| `F4` | Alterna entre visor y edición (tres estados). |
| `F5` | Recarga el documento desde el disco. |

Los atajos `F2`-`F5` funcionan también con el foco en la vista previa: un filtro de mensajes los intercepta antes de que el control ActiveX del visor los consuma.

## Edición

El editor usa la fuente **Segoe UI Symbol** para soportar caracteres no ASCII (CJK, árabe, matemáticas, símbolos de caja) y emoji; Windows aplica *font fallback* automático por glifo para cualquier carácter que la fuente base no incluya.

### Entrar y salir

Pulsa `F4` o usa **Editar → Editar documento** para alternar entre tres estados:

| Estado | Vistas visibles | F4 pasa a |
| --- | --- | --- |
| **Visor solo** (inicial) | Visor | Editor + Visor |
| **Editor + Visor** | Editor + vista previa en vivo | Solo Editor |
| **Solo Editor** | Editor (vista previa oculta) | Visor solo |

- En **Visor solo** la ventana muestra el índice a la izquierda y el visor a la derecha.
- En **Editor + Visor** se añade el editor a la izquierda del visor; la vista previa se actualiza en vivo y el visor sigue al cursor.
- En **Solo Editor** la vista previa se oculta y no se actualiza; el editor ocupa todo el ancho.
- Al volver a **Visor solo** desde **Solo Editor**, el visor se re-renderiza con el documento actual (incluidos los cambios hechos en el editor) para quedar sincronizado.

El divisor entre el editor y la vista previa se puede arrastrar. El editor conserva un ancho mínimo de 300 px y la vista previa de 280 px. El panel del índice sigue visible a la izquierda y su divisor también se puede arrastrar.

Si hay cambios sin guardar al presionar `F4` desde **Solo Editor** hacia **Visor solo**, aparece el diálogo de guardado habitual.

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

La vista previa se actualiza mientras se escribe y, además, unos 350 ms después de la última pulsación. Para que el texto escrito se vea sin esperar a pausar:

- Se refresca en cuanto se han escrito más de cinco caracteres desde la última actualización.
- También se refresca al aplicar un marcador Markdown (`#`, `*`, `_`, `` ` ``, `>`, `[`, `]`, etc.), al pulsar `Enter` y ante cualquier cambio que no sea escritura (pegar, borrar, deshacer).
- El temporizador de 350 ms sigue actuando como red de seguridad: si no se cumple ninguno de los disparadores anteriores, la vista previa se actualiza al dejar de escribir.

Solo hay un renderizado de vista previa en curso a la vez. Si llegan nuevas peticiones mientras tanto, se guarda únicamente la más reciente y se lanza al terminar la actual, de modo que las peticiones no se acumulan ni compiten por el hilo de interfaz.

Cada bloque renderizado conserva su línea de origen mediante atributos internos, de modo que al mover el cursor el visor se desplaza al bloque equivalente:

- Al inicio del documento se muestra el principio.
- En medio de un documento se muestra la sección correspondiente.
- Al final se muestra el cierre y las notas al pie.
- Al escribir o deshacer, la vista previa se vuelve a renderizar y sigue al cursor.

Los atributos de sincronización y el script que los usa solo existen en la vista previa. La exportación HTML no los incluye.

### Rendimiento

El visor mantiene la respuesta en documentos grandes gracias a dos mecanismos:

- **Resaltado y renderizado en segundo plano.** El editor tokeniza el resaltado de sintaxis y la vista previa genera el HTML en un hilo de trabajo. Cada resultado se aplica después en el hilo de interfaz como un único lote (los trazos de color del editor y el cuerpo de la vista previa), de modo que escribir no se ralentiza por el procesado.
- **Resaltado incremental del editor.** Los tramos de color se normalizan a una lista ordenada y sin solapes. Al escribir, solo se vuelve a aplicar el intervalo afectado por el cambio (la línea actual, la anterior por los encabezados setext y las líneas posteriores que puedan cambiar por un bloque cercado), en lugar de recorrer todos los tramos del documento. Si el cambio es estructural o el documento supera el límite de resaltado, se recurre al recorrido completo.
- **Resaltado opcional del código.** Con **Ver → Resaltar código en bloques del editor** desactivado, el tokenizador no se ejecuta para los bloques cercados: cada bloque se emite como un único tramo en color de comentario (verde), marcadores incluidos. En una prueba de esfuerzo con un documento de 56 218 caracteres, desactivarlo redujo el tiempo de reaplicación completa del resaltado un 17,6 % y el número de tramos un 19,6 % (1521,95 ms y 1915 tramos con resaltado, 1254,6 ms y 1540 tramos sin él).
- **Actualización incremental de la vista previa.** La página del visor es una plantilla fija (hoja de estilo, guion de sincronización y el contenedor del contenido). Al actualizar la vista previa, en lugar de recargar la página completa, se sustituye solo el contenido del cuerpo y se avanza su identificador de generación para que el guion vuelva a recopilar las anclas de sincronización. Así se evita el parpadeo y la pérdida de posición de una carga completa.
  - Solo se recarga la página completa cuando hace falta: en la carga inicial, al cambiar el tema (el CSS va incrustado en la página) y como reserva si la sustitución in situ falla.
  - Alternar **Ver → Índice en el documento** también usa el camino incremental: solo cambia la visibilidad del índice dentro del contenido y conserva la posición de scroll.

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
- El resaltado de bloques cercados reconoce C#, JavaScript/TypeScript, C/C++, BASIC, Pascal, Fortran, JSON, HTML/XML/SVG/Razor, CSS/SCSS/Less, LEN y LEAL, entre otros.
- Los marcadores de los fences se dibujan siempre en verde (`#7EE787` en tema oscuro, `#116329` en tema claro), en ambas líneas de cierre y apertura: las comillas ``` y, en la línea de apertura, también el identificador de lenguaje (por ejemplo, el `javascript` de ```javascript).
- Con **Ver → Resaltar código en bloques del editor** activado, solo se tokeniza el contenido entre los fences: las palabras clave usan el color de palabra clave, los comentarios se muestran en verde y el resto del código usa el color de texto del tema (blanco sobre oscuro, negro sobre claro). En bloques **HTML/XML** los nombres de etiqueta se pintan en verde (igual que los comentarios), los atributos y el `<!DOCTYPE>`/`<?xml ...?>` en azul, y los comentarios `<!-- -->` en verde; en bloques **CSS** los selectores se pintan en verde, las propiedades en azul, las reglas `@media`/`@keyframes` con el color de palabra clave y los comentarios `/* */` en verde. Las cadenas y números conservan el color de texto, como en el resto de lenguajes del editor.
- Si el fence no declara ningún lenguaje, usa `text` o declara un lenguaje no reconocido (incluidos `yaml`, `markdown` y `diff`, que se resaltan solo en el visor), el bloque completo (marcadores y contenido) se muestra en ese mismo verde: no hay token que aplicar.
- Al desactivar esa opción, el bloque completo (marcadores y contenido) se muestra en ese mismo verde y el tokenizador no se ejecuta, lo que reduce el trabajo del editor en documentos grandes. La preferencia se guarda y se aplica al volver a abrir el programa.

### Normalización del código

Al definir o editar un bloque cercado, el contenido se normaliza según el lenguaje (unos 500 ms después de la última pulsación; el bloque que contiene el cursor se respeta hasta que se fuerza la normalización). La opción **Editar → Normalizar código → Automáticamente** controla este comportamiento, se guarda en el registro y viene activada de forma predeterminada:

| Lenguaje | Convención aplicada |
| --- | --- |
| BASIC, Fortran, SQL, LEN, LEAL, batch, Dockerfile | Palabras clave en MAYÚSCULAS |
| Pascal, INI | Palabras clave en minúsculas |
| Visual Basic | Grafía canónica de cada palabra clave |
| JSON | `true`, `false` y `null` en minúsculas |

Los lenguajes sensibles a mayúsculas (C#, JavaScript, C/C++, Python, etc.) no se modifican. **Editar → Normalizar código → Normalizar ahora** fuerza la normalización de todos los bloques, aunque la opción automática esté desactivada. Al activar **Automáticamente** se normaliza también el texto que ya está abierto. Al guardar solo se normaliza si la opción automática está activa.

### Divisores

- Doble clic en el divisor entre editor y vista previa: reparto 50/50.
- Doble clic en el divisor del panel del índice: el índice vuelve a su ancho mínimo.
- Los límites de arrastre siguen siendo 300 px para el editor, 280 px para la vista previa y el ancho mínimo del índice.

### Índice y navegación

El panel de la izquierda se actualiza con la vista previa: al añadir, cambiar o eliminar un encabezado, la lista y el contador se actualizan con el mismo ritmo que la vista previa (de inmediato al pulsar `Enter` o aplicar un marcador, y como máximo unos 350 ms después de la última edición). Las entradas largas se recortan con puntos suspensivos.

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

- `MainForm.cs`: ventana principal, carga, navegación, zoom, temas, recarga, vigilancia del archivo, modo edición, divisor del índice, visor incremental, sincronización bidireccional y normalización.
- `TocPanel.cs`: panel del índice, lista con dibujo propio, selección y temas.
- `MarkdownEditor.cs`: editor `RichTextBox`, formato de marcadores, resaltado Markdown y de código en segundo plano, continuación de listas y eventos de cursor.
- `VisorScriptBridge.cs`: puente COM entre la vista previa y el editor para clics y selecciones.
- `EditSession.cs`: copia temporal, recuperación, guardado y detección de conflictos.
- `TextFileCodec.cs`: codificación, BOM, saltos de línea y escritura atómica.
- `SaveChangesDialog.cs`: diálogo temático Guardar/Descartar/Cancelar.
- `FileChangedDialog.cs`: aviso temático de archivo modificado.
- `DarkChrome.cs`: barra de título, menús, barra de estado y scrollbar de IE.
- `ThemeManager.cs`: preferencia y detección del tema del sistema.
- `SettingsStore.cs`: preferencias booleanas del visor en el registro (índice, resaltado de código y normalización automática).
- `Markdown/`: parser, renderizador, saneador, resaltador, normalizador de código y exportador.
- `Assets/`: hojas de estilo, icono y estado vacío.
- `test/`: documento de prueba, exportaciones, capturas y scripts de validación.
- `TCplg/`: plugin WLX para Total Commander, con fuentes, `build.ps1`, paquete y pruebas propias.

## Pruebas

Las suites de prueba se ejecutan en PowerShell y validan la interfaz, la exportación HTML y el comportamiento con documentos grandes. Ver `test/README.md` para detalles completos.

- `verify-export.ps1`: exporta `test/sample.md` a HTML autónomo (temas oscuro y claro) y comprueba encabezados, enlaces, seguridad y recursos.
- `ui_sync_verify.ps1`: ejecuta el visor real alojado en PowerShell y comprueba editor, visor, sincronización, atajos F2-F5 y el índice generado (viewer-only).
- `stress-large.ps1`: valida rendimiento con un documento de más de 2000 líneas y 144 bloques cercados.

Resultado actual: **145 PASS, 0 FAIL** en la suite principal, y todos los checks pasan en exportación y estrés.

## Limitaciones

- El motor es Internet Explorer 11. No se usan variables CSS, `:has`, `position: sticky` ni otras características modernas.
- La barra de desplazamiento nativa de IE puede seguir viéndose clara en algunos equipos aunque el resto de la ventana sea oscuro; es una limitación del control.
- La impresión utiliza el diálogo y la vista previa de IE.
- El zoom es cosmético y va del 50 % al 300 %.
- El editor es un `RichTextBox`: el resaltado se aplica como tramos ordenados y sin solapes; en documentos de más de 400.000 caracteres se omite para mantener la respuesta.
- El seguimiento del cursor es por bloques. Dentro de un bloque muy largo, como un párrafo o un bloque de código de muchas líneas, el visor mantiene el inicio del bloque.
- El panel del índice solo muestra encabezados Markdown; no incluye encabezados escritos dentro de HTML crudo ni se puede contraer.
- El modo edición trabaja con un archivo cada vez; no hay pestañas ni edición de varios documentos a la vez.
- La copia temporal protege ante cierres inesperados, pero no sustituye a guardar el archivo.
- La detección de cambios depende del sistema de archivos y del editor. Si un cambio no se detecta, `F5` recarga manualmente.

## Licencia

MIT.
