# SPEC — CuotaApp

Calcula la cuota mensual de un préstamo con el método francés (cuota fija).

## 1. Función

`calcularCuota(monto: number, tea: number, meses: number): number`

Archivo: `src/cuota.ts` (exportación nombrada).

## 2. Entradas

| Parámetro | Significado | Regla |
|---|---|---|
| `monto` | Capital prestado en soles | Número mayor que 0 |
| `tea` | Tasa Efectiva Anual en porcentaje (30 = 30%) | Número mayor o igual a 0 |
| `meses` | Plazo en meses | Entero mayor o igual a 1 |

## 3. Cálculo

1. Tasa mensual equivalente: `i = (1 + tea / 100)^(1/12) − 1`
2. Si `i > 0`: `cuota = monto · i / (1 − (1 + i)^(−meses))`
3. Si `tea = 0`: `cuota = monto / meses`
4. Redondear el resultado a 2 decimales: `Math.round(cuota * 100) / 100`

## 4. Errores

La función lanza `Error` con el mensaje exacto:

| Condición | Mensaje |
|---|---|
| `monto` no es un número mayor que 0 (incluye `NaN`) | `Monto inválido` |
| `tea` no es un número mayor o igual a 0 (incluye `NaN`) | `Tasa inválida` |
| `meses` no es un entero mayor o igual a 1 | `Plazo inválido` |

Si hay varios errores, se valida en este orden: monto, tasa, plazo.

## 5. Ejemplos (cada uno es una prueba)

| # | monto | tea | meses | Resultado |
|---|---|---|---|---|
| E1 | 10000 | 30 | 12 | 957.86 |
| E2 | 5000 | 45 | 6 | 927.42 |
| E3 | 3000 | 35 | 24 | 168.34 |
| E4 | 10000 | 0 | 12 | 833.33 |
| E5 | 0 | 30 | 12 | Error `Monto inválido` |
| E6 | 10000 | -5 | 12 | Error `Tasa inválida` |
| E7 | 10000 | 30 | 0 | Error `Plazo inválido` |
| E8 | 10000 | 30 | 6.5 | Error `Plazo inválido` |

## 6. Pantalla (`App.tsx`)

### Contenido
- Título `CuotaApp` y subtítulo `Método francés · TEA`.
- Tres campos numéricos, cada uno con su etiqueta encima: `Monto (S/)`, `TEA (%)`, `Plazo (meses)`.
- Un botón de ancho completo: `Calcular`.
- Si el cálculo es válido, una tarjeta de resultado con la etiqueta `Cuota mensual` y debajo el monto en grande: `S/ 957.86`.
- Si `calcularCuota` lanza un error, muestra su mensaje en color de error, en lugar de la tarjeta.
- Sin navegación, sin librerías de UI externas: solo componentes de React Native.

### Diseño
| Token | Valor |
|---|---|
| Fondo | `#121318` |
| Superficie (campos y tarjeta) | `#1C1E25`, borde `#2A2D36` de 1 px, radio 12 |
| Texto principal | `#F2EFE6` |
| Texto secundario (etiquetas, subtítulo, placeholder) | `#9AA0AA` |
| Acento (botón, monto del resultado, borde del campo con foco) | `#4C7DFF` |
| Error | `#FF6B6B` |
| Tipografía | Monoespaciada del sistema (`monospace` en Android, `ui-monospace, monospace` en web) |
| Tamaños | Título 28, subtítulo 14, etiquetas 13, campos 16, monto del resultado 36 en negrita |
| Espaciado | Margen lateral 24, separación entre elementos 16, alto de campos y botón 52 |

- El contenido se centra verticalmente; ancho máximo 420.
- El botón tiene fondo de acento y texto `#FFFFFF` en negrita.
- La barra de estado del teléfono va en modo claro sobre el fondo oscuro.

## 7. Fuera de alcance

- Cronograma de pagos, seguros, comisiones, ITF o TCEA.
- Persistencia, red, autenticación.
- Otras monedas.

## 8. Versión web

- Proyecto separado `cuota-web`: Vite + React + TypeScript.
- Copia `src/cuota.ts` y `src/cuota.test.ts` sin cambiar la lógica ni las pruebas.
- Pruebas con Vitest (`globals: true`). Script `"test": "vitest run"`.
- `vite.config.ts` importa `defineConfig` desde `vitest/config`.
- Los archivos `*.test.ts` no entran en el build: `"exclude": ["src/**/*.test.ts"]` en `tsconfig.app.json`.
- `src/App.tsx`: la misma pantalla y el mismo diseño de la sección 6, con elementos HTML (`input`, `button`) y CSS en `src/index.css`. El fondo cubre toda la página.
- Despliegue en GitHub Pages con el paquete `gh-pages`: `base: '/cuota-web/'` en `vite.config.ts` y script `"deploy": "npm run build && gh-pages -d dist"`.
- Dependencias permitidas: `vitest` y `gh-pages` (desarrollo).
