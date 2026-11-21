# Evidencias — Registro de cobros (Egnis Piliado Montaño)

Programa: `PENDIENTE` · Repo: `https://github.com/EGNIS2915/registro-ventas-cobros` · Red: **Devnet** · Participante: `Egnis Piliado Montaño`

Cada firma se verifica en `https://explorer.solana.com/tx/<FIRMA>?cluster=devnet`.
Sustituir `[PENDIENTE]` por la firma real antes de entregar. No capturar claves privadas.

| # | Caso | Operación en la UI | Resultado esperado | Firma / mensaje |
|---|---|---|---|---|
| 1 | Crear registro | `Crear registro` | Cuenta `Registro` creada para `Cafe Cobros Egnis` | `[PENDIENTE]` |
| 2 | Crear cliente | `Crear cliente` | Cliente #1 con 0 cobradas | `[PENDIENTE]` |
| 3 | Venta válida | `Registrar venta` | Venta activa en historial, `pagada=false` | `[PENDIENTE]` |
| 4 | Corregir importe | `Corregir importe` | Monto actualizado sin cerrar la venta | `[PENDIENTE]` |
| 5 | Devolución | `Devolución` | Venta eliminada del historial | `[PENDIENTE]` |
| 6 | Baja de cliente vacío | `Dar de baja` | Cliente sin ventas se elimina del registro | `[PENDIENTE]` |
| 7 | Wallet no autorizada | Cualquier escritura con otra wallet | `NoOwner` / 6000 | `[PENDIENTE: error 6000]` |
| 8 | Venta ajena | Venta con cliente fuera del registro | `NoClienteEnRegistro` / 6002 o `NoSKU` / 6001 | `[PENDIENTE: error]` |
| 9 | **Mejora: marcar pagada** | `Marcar pagada` | Badge *Pagada*, contador del cliente +1 | `[PENDIENTE]` |
| 10 | **Mejora: cobro repetido** | `Marcar pagada` otra vez | `YaPagada` / 6005 | `[PENDIENTE: error 6005]` |
| 11 | **Mejora: monto inválido** | `Registrar venta` con 0 | `MontoInvalido` / 6004 | `[PENDIENTE: error 6004]` |

## Checklist de captura

- [ ] Explorer en Devnet con la firma legible.
- [ ] Panel `Clientes y ventas` mostrando el badge **Pagada** y el contador de cobros.
- [ ] Consola o aviso de la app con el error del programa cuando aplique.
- [ ] Sin `keypair.json`, semillas ni claves en pantalla.
- [ ] IDL exportado del despliegue guardado como `idl.json` y `npm run verificar` en verde.
