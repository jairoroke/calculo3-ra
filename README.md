# Cálculo III en realidad aumentada (prototipo de prueba)

Simulaciones del libro *Cálculo III. Funciones reales de un vector*, de Jairo Olguín Roque
(FES Acatlán, UNAM), que aparecen en 3D sobre el código QR impreso en el libro.

- Sitio: <https://jairoroke.github.io/calculo3-ra/>
- Primera simulación: <https://jairoroke.github.io/calculo3-ra/mc/> (Monte Carlo del cono de helado,
  Sección 6.6, Ejemplo 6.11 y Tabla 6.1; programa `cap6_monte_carlo.m`).
- Tarjeta de prueba para imprimir: `descargas/Tarjeta_RA_Monte_Carlo.pdf`.

## Cómo se usa

1. Se escanea el código con la cámara del celular; el código lleva a `mc/`.
2. «Iniciar la cámara» pide permiso para usar la cámara (la página necesita https).
3. Al apuntar al código, el cubo con el cono de helado aparece encima y «Correr» lanza las cuatro
   corridas de la Tabla 6.1 (10³, 10⁴, 10⁵ y 10⁶ puntos, semilla 2027).

La cámara sólo se usa en el teléfono: no se graba ni se envía nada.

## Cómo funciona

- El marcador es un código QR (versión 3-L) dentro de un marco negro. El marco es el «marcador de
  patrón» de ARToolKit (proporción del patrón 0.75) y el QR abre la página.
- `mc/datos/marcador.patt` es el patrón del interior del marcador; `mc/datos/camera_para.dat` son los
  parámetros de cámara genéricos de ARToolKit.
- La página usa AR.js 3.4.5 (compilación para three.js) y three.js r150.1, sin modificarlos
  (`lib/`). Sobre ellos, la página hace tres ajustes:
  - analiza una imagen de 640 × 480 tomada del centro de la cámara; si el teléfono está vertical, la
    gira 90° para no deformar el código, y gira de vuelta la proyección;
  - usa siempre la estimación directa de la pose, porque la «continua» de esta versión de ARToolKit
    se dispara a valores enormes;
  - de los candidatos de cada imagen toma el de mayor área con confianza de al menos 0.7, porque
    ARToolKit también reconoce como marcadores los cuadros de posición del QR (confianza 0.6 a 0.65).
- La simulación reproduce el generador de MATLAB (`rng(2027)` y `rand`) y da las cifras de la
  Tabla 6.1 del libro.

## Probar en la computadora

```bash
python3 -m http.server 8000
# abrir http://localhost:8000/mc/ (localhost cuenta como origen seguro para la cámara)
```

## Licencias

Contenido (páginas, marcador y simulación): D. R.©, 2026, UNAM - CC BY-NC-ND. Bibliotecas de
terceros: vea `lib/licencias/LEEME.md` (three.js y AR.js con licencia MIT; ARToolKit, incluido en
AR.js, con licencia LGPL-3.0).
