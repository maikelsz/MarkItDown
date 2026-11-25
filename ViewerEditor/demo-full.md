---
title: Demo completo MarkItDown
author: MaikelSZ
---

# Demo completo de MarkItDown

[TOC]

Este documento ejercita **todas** las capacidades de marcado soportadas, incluidos caracteres especiales y bloques de código en varios lenguajes.

## Encabezados

### Nivel 3 con **negrita** y *cursiva*

#### Nivel 4 con `código` y [enlace](https://example.com)

Encabezado Setext 1
====================

Encabezado Setext 2
-------------------

Encabezado con cierre ATX optional #### así ##

## Formato en línea

**Negrita**, *cursiva*, ***ambas juntas***, ~~tachado~~, `código inline`, [enlace externo](https://example.com "Título"),
[enlace sin título](https://example.org), autolink <https://auto.link/x?y=1> y correo <correo@example.com>.

También funciona la referencia definida: [ver referencia][ref] y un enlace a otra página interna [la tabla](#tabla).

> Nota: el texto con escapes: \*no cursiva\*, \#no encabezado\* y \\barra invertida\\.

## Imágenes

![Icono vacío](Assets/empty.svg)

![Remoto](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4a/Markdown_logo.svg/240px-Markdown_logo.svg.png)

## Listas

- [x] Tarea completada
- [ ] Tarea pendiente
  - Elemento anidado 1
  - Elemento anidado 2
    1. Sub-ordenado 1
    2. Sub-ordenado 2
      - Sub-anidado profundo
- Elemento normal con **formato**
- Otro elemento

1. Primero
2. Segundo
   - Mezcla ordenado/anidado
   - Con `código`
3. Tercero

- Elemento suelto con espacio en blanco entre elementos:

  Y un segundo párrafo del mismo elemento (lista suelta).

- Elemento con código inline y [enlace](https://example.com).

## Tabla

<table id="tabla"></table>

| Columna A | Columna B | Número | Estado |
| :-------- | :-------: | -----: | :----: |
| texto     | **negrita** | 42    | [ok](https://example.com) |
| `a\|b`    | *cursiva*  | 7     | pendiente |
| imagen    | ![i](Assets/empty.svg) | 99 | ✔ |

## Citas y alertas

> Cita normal con **formato**.
>
> Segunda línea de la cita tras un salto vacío dentro de la cita.
> - Puesto en lista dentro de la cita

> [!NOTE]
> Nota importante con `código` y [enlace](https://example.com).

> [!TIP]
> Consejo útil con **negrita**.

> [!IMPORTANT]
> Información crítica.

> [!WARNING]
> Cuidado con `esto` y los enlaces [peligrosos](javascript:alert(1)).

> [!CAUTION]
> Precaución con el contenido no validado.

## Bloques de código

### C#

```csharp
using System;
using System.Linq;
using System.Collections.Generic;

namespace Ejemplo
{
    public sealed class Calculadora
    {
        public static double Sumar(params double[] valores)
        {
            double total = 0.0; // comentario de línea
            /* comentario
               en bloque */
            foreach (double v in valores)
            {
                total += v;
            }
            return total;
        }

        public static void Main()
        {
            Console.WriteLine(Sumar(1, 2, 3));
        }
    }
}
```

### JavaScript

```javascript
const sumar = (a, b) => a + b; // comentario

/**
 * Documento JSDoc de ejemplo.
 * @param {number} x
 * @returns {number}
 */
function factorial(n) {
    return n <= 1 ? 1 : n * factorial(n - 1);
}

class Animal {
    constructor(nombre) {
        this.nombre = nombre;
    }
    hablar() {
        console.log(`${this.nombre} hace un sonido`);
    }
}

const animales = [new Animal("Gato"), new Animal("Perro")];
animales.forEach(a => a.hablar());
```

### C / C++

```cpp
#include <iostream>
#include <vector>

using namespace std;

template <typename T>
class Pila {
    vector<T> _datos;
public:
    void empujar(const T& valor) { _datos.push_back(valor); }
    T sacar() { T v = _datos.back(); _datos.pop_back(); return v; }
    bool vacia() const { return _datos.empty(); }
};

int main() {
    Pila<int> pila;
    pila.empujar(10);
    pila.empujar(20);
    // Extraer y mostrar
    cout << pila.sacar() << endl;
    return 0;
}
```

### BASIC (QuickBASIC / GW-BASIC)

```basic
' Comentario en BASIC
DIM a AS INTEGER, b AS INTEGER
LET a = 10
LET b = 20
PRINT "La suma es"; a + b
FOR i = 1 TO 5
    PRINT i; i * i
NEXT i
```

### BASIC clásico con números de línea

```basic
10 REM Programa clásico con números de línea
20 PRINT "HOLA"
30 FOR I = 1 TO 3
40 PRINT "ITERACION"; I
50 NEXT I
60 END
```

### Pascal

```pascal
{ Comentario en bloque Pascal }
program EjemploPascal;
const
  MAXIMO = 100;
var
  i: integer;
  nombre: string[50];
begin
  name := 'Hola';
  for i := 1 to 10 do
  begin
    writeln('Iteracion: ', i);
  end;
  readln;
end.
```

### Fortran

```fortran
C     Comentario en Fortran (primera columna)
      PROGRAM EJEMPLO
      IMPLICIT NONE
      INTEGER :: I, RESULTADO
      REAL :: X
      X = 3.14159
      RESULTADO = 0
      DO I = 1, 10
         RESULTADO = RESULTADO + I
      END DO
      WRITE (*,*) 'SUMA =', RESULTADO
      WRITE (*,*) 'PI =', X
      END PROGRAM EJEMPLO
```

### LEN (ensamblador CID 201/201A/201B)

```len
/ Programa de ejemplo LEN
INICIO, LAC DATO
        SUM UNO
        DEL RESULT
        VEA FIN
DATO,   0x0010
UNO,    0o0001
RESULT, 0
FIN,    ALT
$
```

### LEAL (compilador CID 201/201A/201B)

```leal
LEAL
TITULO DEMOSTRACION LEAL
ENT A, B, R
REF
LEC A
LEC B
A + B = R
PER R
LIN
FIN
```

### JSON

```json
{
  "nombre": "MarkItDown",
  "version": "1.0.0",
  "activado": true,
  "limites": null,
  "tags": ["markdown", "visor", "editor"],
  "anidado": {
    "tema": "oscuro",
    "columnas": 80
  }
}
```

### Python (comparación)

```python
def fibonacci(n):
    a, b = 0, 1  # comentario
    resultado = []
    for _ in range(n):
        resultado.append(a)
        a, b = b, a + b
    return resultado

# Cadena triple
doc = """
Texto multilinea con formato **no** interpretado.
"""
print(fibonacci(10))
```

### SQL

```sql
-- Consulta de ejemplo
SELECT id, nombre, precio
FROM productos
WHERE categoria = 'informática'
  AND precio < 100.50
ORDER BY nombre ASC;
```

### HTML / CSS / shell (ya soportados, incluidos para referencia)

```html
<!DOCTYPE html>
<html lang="es">
<head><meta charset="utf-8"><title>Ejemplo</title></head>
<body>
  <div class="caja">Contenido &amp; más</div>
</body>
</html>
```

```css
.caja {
  color: #ff5722; /* comentario CSS */
  border: 1px solid #ddd;
}
@media (max-width: 600px) {
  .caja { font-size: 14px; }
}
```

```bash
#!/usr/bin/env bash
# Script de ejemplo
for archivo in *.md; do
    echo "Procesando $archivo"
done
```

## Caracteres especiales

### Emojis

😀 😊 👋 🚀 🎉 💡 ✨ 🇲🇽 🇪🇸 🇬🇹 ⭐ 🐍 🔥

:rocket: :smile: :white_check_mark: :tada: :fire: :star:

### CJK y árabe

日本語テスト — 中文测试 — العربية —한국어 — 你好世界

### Símbolos matemáticos

α β γ δ ε ≠ ± × ÷ √ ∞ → ← ↑ ↓ ∑ ∏ ∫ ∂ ≤ ≥ ≈

E = mc², a² + b² = c², ∮ E·dA = Q/ε₀

### Caracteres de caja y bloques

┌─────────┐
│ cuadro  │
└─────────┘
├─┬─┬─┤
├─┼─┼─┤
└─┴─┴─┘
█ █▓▒░▐▌▖▗▝▞

### Acentos y caracteres extendidos

á é í ó ú ñ ¿ ¡ ð þ œ æ ç ƒ ı ÿ

### Espacios especiales

Tabulador:	
No romper: nbsp

## Notas al pie

Esto tiene una nota al pie[^1] y otra[^2] con un [enlace interno](#caracteres-especiales).

[^1]: Primera nota con **formato** y `código`.
[^2]: Segunda nota con un [enlace](https://example.com) y un salto de línea dentro de la nota.

## HTML crudo

<details>
<summary>Más información</summary>

Contenido dentro de details, con **formato** y [enlace](https://example.com).

</details>

<div align="center"><strong>HTML crudo permitido</strong></div>

<script>alert('esto debe desaparecer');</script>

<img src="javascript:alert(1)" onerror="alert(1)" alt="peligro">

<hr>

## Referencias definidas

Texto con una referencia [definida][ref] y otra [con título][titulo].

[ref]: https://example.com/definida "Título de la referencia"
[titulo]: https://example.org

Texto final.
