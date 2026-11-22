# Evidencias — Registro de cobros (Egnis Piliado Montaño)

Programa: `8H93sPVcos2HiwEHq1Ja5BcFyEQRydbjKCx9jmckyQtV` · Repo: `https://github.com/EGNIS2915/registro-ventas-cobros` · Red: **Devnet** · Participante: `Egnis Piliado Montaño`

Cada firma se verifica en `https://explorer.solana.com/tx/<FIRMA>?cluster=devnet`.
Sustituir los marcadores por la firma real antes de entregar. No capturar claves privadas.

| # | Caso | Operación en la UI | Resultado esperado | Firma / mensaje |
|---|---|---|---|---|
| 1 | Crear registro | `Crear registro` | Cuenta `Registro` creada para `Cafe Cobros Egnis` | `WVw44ybMoiUqBFwfjSP7QdoHsjagseiTvWbDohfDBYskDraFNgzRxQ3YSoww2BwWoPYMkrmta1BW89L9fnaa7Ff` |
| 2 | Crear cliente | `Crear cliente` | Cliente #1 con 0 cobradas | `21Vow6XbmVKEa6q4mnfeUdfrsUhkK9KxHEAGXWppfCfmpf3CbDKj2pRQGHoaxRbCuSMNJJHwQ1bkJPmSSiguHLoH` |
| 3 | Venta válida | `Registrar venta` | Venta activa en historial, `pagada=false` | `5F9DvD2kUajSYWaLs3TyF6iRkt9cice12pEPwvDL96YnVN5RfeLoW8ntmNJSyYQQtvUgYjGi34WC3g6QLRD33YKk` |
| 4 | Corregir importe | `Corregir importe` | Monto actualizado sin cerrar la venta | `5rQjGBfceU8uYsbpmkGX6d6sWut3EJFa92inLf8N7SkqLukMHmTrcgTowApQkH4ArVcZFkZoFRvXzwRKyaPAiMw8` |
| 5 | Devolución | `Devolución` | Venta eliminada del historial | `51HzM7nGpKfSDD3wGB1hKo7PnopCHWTXPk4UBJ1iyPmB2bLR1Ph6qmqjNaue8NbdstcdKk5hzw33ueAh8JT5jmA2` |
| 6 | Baja de cliente vacío | `Dar de baja` | Cliente sin ventas se elimina del registro | `3MWo8SdxH5eqVaKExJx1sEhiyoCdHNSbAxuau7MnWq9NNjn7yKU2bbAULHTwdeuSaJLNoQAj74u4QvNDu6qKtLEB` |
| 7 | Wallet no autorizada | Cualquier escritura con otra wallet | `NoOwner` / 6000 | `5NqugegNKjHPHXdJzmMgNxewS8DKB3ir9LieKJLHNeUXpoush7optXvHSM1txHQDH5iiH5A7V93RbMzxtqgdt6dG` (tx fallida: NoOwner 6000, `0x1770`) |
| 8 | Venta ajena | Venta con cliente fuera del registro | `ConstraintSeeds` / 2006 (cliente ajeno al registro) | `ConstraintSeeds 2006 (simulación RPC, sin firma)` |
| 9 | **Mejora: marcar pagada** | `Marcar pagada` | Badge *Pagada*, contador del cliente +1 | `2BX92Vb5SwQ4haU53aX4Sz3r7CYfanWwoCtvUNepiMaFdXCNvPmd8L5rtWRQQtysWgqssSEhnEsCtPi2rKHmvgx7` |
| 10 | **Mejora: cobro repetido** | `Marcar pagada` otra vez | `YaPagada` / 6005 | `YaPagada 6005 (0x1775, simulación RPC, sin firma)` |
| 11 | **Mejora: monto inválido** | `Registrar venta` con 0 | `MontoInvalido` / 6004 | `MontoInvalido 6004 (simulación RPC, sin firma)` |
| 12 | Baja con ventas activas | `Dar de baja` con historial | `ClienteConVentas` / 6003 | `ClienteConVentas 6003 (simulación RPC, sin firma)` |

## Checklist de captura

- [ ] Explorer en Devnet con la firma legible.
- [ ] Panel `Clientes y ventas` mostrando el badge **Pagada** y el contador de cobros.
- [ ] Consola o aviso de la app con el error del programa cuando aplique.
- [ ] Sin `keypair.json`, semillas ni claves en pantalla.
- [ ] IDL exportado del despliegue guardado como `idl.json` y `npm run verificar` en verde.

## Cómo completar cada fila

Para cada caso registra el estado inicial (negocio, ID de cliente y monto), la operación ejecutada, el resultado observado en las cuentas y la firma o el error. Usa enlaces `https://explorer.solana.com/tx/<FIRMA>?cluster=devnet`. Si el rechazo ocurre en simulación previa y no hay transacción consultable, conserva el mensaje de error y comprueba que el estado del negocio no cambió.

## Cierre automático

Ejecuta `npm run verificar:entrega` antes de entregar. El gate revisa Program ID, IDL real, nombre del participante, ausencia de marcadores y firmas válidas; mientras quede algún marcador sin completar, el cierre falla y el repo no debe enviarse.
