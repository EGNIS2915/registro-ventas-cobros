# Registro de cobros — Egnis Piliado Montaño

Proyecto del **Solana Engineering Track: Advanced** (WayLearn). Registro de clientes y ventas con PDAs en Devnet, frontend React/Vite y cliente TypeScript generado por Codama desde el IDL.

- **Participante para el certificado:** `Egnis Piliado Montaño`
- **Repo:** `https://github.com/EGNIS2915/registro-ventas-cobros`
- **Negocio usado en la app:** `Cafe Cobros Egnis`
- **Program ID:** `8H93sPVcos2HiwEHq1Ja5BcFyEQRydbjKCx9jmckyQtV` (Devnet)
- **IDL entregado:** `idl.json` (alineado con el Program ID del despliegue)
- **Evidencias:** [`EVIDENCIAS.md`](./EVIDENCIAS.md)

## Mejora funcional: control de cobros

La operación nueva `Marcar pagada` cierra una venta sin borrarla del historial:

- Instrucción Rust `marcar_pagada` (`marcarPagada` en IDL/TS): solo la autoridad del registro.
- `Venta` gana el campo `pagada: bool`; `Cliente` gana `ventas_pagadas: u16`.
- Marcar aumenta el contador del cliente en 1 y vuelve a fallar si la venta ya estaba pagada (`YaPagada`, 6005).
- La UI muestra **Pagada / Pendiente** por venta y el total cobrado por cliente.
- Refuerzo: `registrar_venta` y `cambiar_monto` exigen `monto > 0` (`MontoInvalido`, 6004).
- La baja de cliente del día 5 queda integrada en la UI como `Dar de baja`.

## Contrato del bootcamp (sin romper)

Se conservan las 6 instrucciones base, el orden de argumentos/cuentas, los seeds `registro`, `cliente`, `venta` y los errores 6000–6003. El validador `scripts/contrato-idl.mjs` acepta campos/argumentos añadidos **al final**, pero rechaza cualquier cambio en el prefijo base.

## Estructura

- `programa/src/lib.rs`: programa Anchor con las cuentas `Registro`, `Cliente` y `Venta`.
- `idl.json`: contrato fuente para Codama.
- `clients/js/src/generated`: cliente generado (instrucciones, cuentas, tipos y PDA helpers).
- `src/solana`: PDAs, lecturas, envío de transacciones, validaciones y seguridad Devnet.
- `src/components/Registro.tsx`: panel de consulta y operaciones con firma.
- `tests/integracion-cliente.test.ts`: 10 pruebas (semillas, serialización, contrato, errores y Devnet).

## Ejecutar

```powershell
npm ci
npm run cliente
npm run verificar
npm run dev
```

`npm run verificar` corre `tsc -b`, las pruebas y el build de producción. `npm run comprobar:idl` confirma que `idl.json`, `src/config/programa.json` y el cliente generado coinciden.

## Despliegue y entrega

1. En Solana Playground: pegar `programa/src/lib.rs`, conservar la línea `declare_id!` que te da Playground (el `declare_id!("")` del repo es solo marcador), `Build`, `Deploy` en Devnet y copiar el **Program ID**.
2. Exportar el IDL del programa y guardarlo localmente, por ejemplo `C:\Users\pilia\Downloads\cobros_idl.json`.
3. Importarlo y regenerar el cliente:

```powershell
npm run configurar:idl -- "C:\Users\pilia\Downloads\cobros_idl.json" --program-id TU_PROGRAM_ID
npm run verificar
```

4. Crear el negocio `Cafe Cobros Egnis` con la wallet de la entrega y capturar las firmas indicadas en `EVIDENCIAS.md`.
5. Subir este repo a `main` y enviar el formulario final con el enlace del repo y el Program ID.

No incluir claves privadas ni `keypair.json` en el repo. Las capturas deben mostrar direcciones públicas y firmas, nunca semillas.

## Arquitectura y defensa

En [`docs/ARQUITECTURA.md`](./docs/ARQUITECTURA.md) están las PDAs y seeds, las reglas de autoridad y pertenencia, la tabla de errores 6000–6005, la explicación del aporte funcional y un guion de demo de 60 segundos. Es la referencia para explicar el proyecto en la revisión y en el hackathon.

## Gate de entrega

Antes de entregar ejecuta:

```powershell
npm run verificar
npm run verificar:entrega
```

`verificar:entrega` comprueba que el IDL ya no sea el de referencia, que el Program ID y `idl.json` coincidan, que el README tenga el nombre para el certificado y que `EVIDENCIAS.md` no contenga marcadores y tenga al menos 6 firmas válidas. Falla a propósito mientras falte el despliegue o las firmas.
