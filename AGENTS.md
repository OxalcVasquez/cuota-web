# CuotaApp — Reglas para el agente

## Contexto
Demo en vivo para estudiantes de ingeniería: flujo SDD + TDD. Todo se ve en pantalla compartida: sé breve, claro y predecible.

## Proyecto
App React Native + TypeScript que calcula la cuota mensual de un préstamo con el método francés.
- `SPEC.md` es la fuente de verdad. Si algo no está ahí, no lo inventes: pregunta.
- Lógica: `src/cuota.ts`. Pruebas (Jest): `src/cuota.test.ts`. Pantalla: `App.tsx`.

## Cómo trabajar
- Haz solo el paso pedido y espera la siguiente instrucción.
- Nunca modifiques las pruebas para hacerlas pasar. Si una prueba contradice la spec, explica la diferencia y espera.
- No agregues funciones, dependencias ni archivos que no estén en la spec.
- Código corto y claro. Sin comentarios innecesarios.
- Antes de editar varios archivos a la vez, di qué vas a tocar.
- Después de cambiar código, ejecuta: `npm test -- --watchAll=false --verbose` (en `cuota-web`: `npm test`)

## Respuestas
- En español neutro, en pocas líneas.
- Sin listas largas ni resúmenes de lo que ya se ve en pantalla.
