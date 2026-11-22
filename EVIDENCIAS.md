# Evidencias — Registro de cobros (Egnis Piliado Montaño)

Programa: `8H93sPVcos2HiwEHq1Ja5BcFyEQRydbjKCx9jmckyQtV` · Repo: `https://github.com/EGNIS2915/registro-ventas-cobros` · Red: **Devnet** · Participante: `Egnis Piliado Montaño`

Cada firma de las operaciones válidas está enlazada a Solana Explorer en Devnet. Los rechazos de regla que no generan transacción conservan el mensaje de error y la comprobación de que el negocio no cambió. No se incluyen claves privadas.

| # | Caso | Operación en la UI | Resultado esperado | Firma / mensaje |
|---|---|---|---|---|
| 1 | Crear registro | `Crear registro` | Cuenta `Registro` creada para `Cafe Cobros Egnis` | `[WVw44ybMoiUqBFwfjSP7QdoHsjagseiTvWbDohfDBYskDraFNgzRxQ3YSoww2BwWoPYMkrmta1BW89L9fnaa7Ff](https://explorer.solana.com/tx/WVw44ybMoiUqBFwfjSP7QdoHsjagseiTvWbDohfDBYskDraFNgzRxQ3YSoww2BwWoPYMkrmta1BW89L9fnaa7Ff?cluster=devnet)` |
| 2 | Crear cliente | `Crear cliente` | Cliente #1 con 0 cobradas | `[21Vow6XbmVKEa6q4mnfeUdfrsUhkK9KxHEAGXWppfCfmpf3CbDKj2pRQGHoaxRbCuSMNJJHwQ1bkJPmSSiguHLoH](https://explorer.solana.com/tx/21Vow6XbmVKEa6q4mnfeUdfrsUhkK9KxHEAGXWppfCfmpf3CbDKj2pRQGHoaxRbCuSMNJJHwQ1bkJPmSSiguHLoH?cluster=devnet)` |
| 3 | Venta válida | `Registrar venta` | Venta activa en historial, `pagada=false` | `[5F9DvD2kUajSYWaLs3TyF6iRkt9cice12pEPwvDL96YnVN5RfeLoW8ntmNJSyYQQtvUgYjGi34WC3g6QLRD33YKk](https://explorer.solana.com/tx/5F9DvD2kUajSYWaLs3TyF6iRkt9cice12pEPwvDL96YnVN5RfeLoW8ntmNJSyYQQtvUgYjGi34WC3g6QLRD33YKk?cluster=devnet)` |
| 4 | Corregir importe | `Corregir importe` | Monto actualizado sin cerrar la venta | `[5rQjGBfceU8uYsbpmkGX6d6sWut3EJFa92inLf8N7SkqLukMHmTrcgTowApQkH4ArVcZFkZoFRvXzwRKyaPAiMw8](https://explorer.solana.com/tx/5rQjGBfceU8uYsbpmkGX6d6sWut3EJFa92inLf8N7SkqLukMHmTrcgTowApQkH4ArVcZFkZoFRvXzwRKyaPAiMw8?cluster=devnet)` |
| 5 | Devolución | `Devolución` | Venta eliminada del historial | `[51HzM7nGpKfSDD3wGB1hKo7PnopCHWTXPk4UBJ1iyPmB2bLR1Ph6qmqjNaue8NbdstcdKk5hzw33ueAh8JT5jmA2](https://explorer.solana.com/tx/51HzM7nGpKfSDD3wGB1hKo7PnopCHWTXPk4UBJ1iyPmB2bLR1Ph6qmqjNaue8NbdstcdKk5hzw33ueAh8JT5jmA2?cluster=devnet)` |
| 6 | Baja de cliente vacío | `Dar de baja` | Cliente sin ventas se elimina del registro | `[3MWo8SdxH5eqVaKExJx1sEhiyoCdHNSbAxuau7MnWq9NNjn7yKU2bbAULHTwdeuSaJLNoQAj74u4QvNDu6qKtLEB](https://explorer.solana.com/tx/3MWo8SdxH5eqVaKExJx1sEhiyoCdHNSbAxuau7MnWq9NNjn7yKU2bbAULHTwdeuSaJLNoQAj74u4QvNDu6qKtLEB?cluster=devnet)` |
| 7 | Wallet no autorizada | Cualquier escritura con otra wallet | `NoOwner` / 6000 | `[5NqugegNKjHPHXdJzmMgNxewS8DKB3ir9LieKJLHNeUXpoush7optXvHSM1txHQDH5iiH5A7V93RbMzxtqgdt6dG](https://explorer.solana.com/tx/5NqugegNKjHPHXdJzmMgNxewS8DKB3ir9LieKJLHNeUXpoush7optXvHSM1txHQDH5iiH5A7V93RbMzxtqgdt6dG?cluster=devnet)` (tx fallida: NoOwner 6000, `0x1770`) |
| 8 | Venta ajena | Venta con cliente fuera del registro | `ConstraintSeeds` / 2006 (cliente ajeno al registro) | `ConstraintSeeds 2006 (simulación RPC, sin firma)` |
| 9 | **Mejora: marcar pagada** | `Marcar pagada` | Badge *Pagada*, contador del cliente +1 | `[2BX92Vb5SwQ4haU53aX4Sz3r7CYfanWwoCtvUNepiMaFdXCNvPmd8L5rtWRQQtysWgqssSEhnEsCtPi2rKHmvgx7](https://explorer.solana.com/tx/2BX92Vb5SwQ4haU53aX4Sz3r7CYfanWwoCtvUNepiMaFdXCNvPmd8L5rtWRQQtysWgqssSEhnEsCtPi2rKHmvgx7?cluster=devnet)` |
| 10 | **Mejora: cobro repetido** | `Marcar pagada` otra vez | `YaPagada` / 6005 | `YaPagada 6005 (0x1775, simulación RPC, sin firma)` |
| 11 | **Mejora: monto inválido** | `Registrar venta` con 0 | `MontoInvalido` / 6004 | `MontoInvalido 6004 (simulación RPC, sin firma)` |
| 12 | Baja con ventas activas | `Dar de baja` con historial | `ClienteConVentas` / 6003 | `ClienteConVentas 6003 (simulación RPC, sin firma)` |

## Cómo se comprobó

Las firmas de las operaciones válidas están enlazadas a Explorer y se pueden abrir una por una. Para los rechazos se conservó el error del programa (o de la simulación previa) y se verificó que las cuentas del negocio quedaran igual. No se incluyeron capturas porque el curso acepta transacciones verificables, y en ellas no aparecen claves, semillas ni datos personales. `idl.json` salió del despliegue y `npm run verificar` está en verde.

## Estado inicial y resultado observado

1. **Registro:** no había negocio; se creó `Cafe Cobros Egnis` y la cuenta quedó legible en la app.
2. **Cliente:** registro sin clientes; se creó el cliente #1 con 0 cobradas.
3. **Venta válida:** cliente sin ventas; se registró una venta activa con `pagada=false`.
4. **Corregir importe:** venta activa; se cambió el monto y la venta siguió ligada al mismo cliente.
5. **Devolución:** venta activa en el historial; se cerró y desapareció de la lista.
6. **Baja vacía:** cliente sin ventas; se cerró su cuenta y el contador de IDs no retrocedió.
7. **Wallet no autorizada:** registro existente; otra wallet recibió `NoOwner` 6000 y los datos no cambiaron.
8. **Venta ajena:** cliente fuera del registro; la simulación devolvió `ConstraintSeeds` 2006 y no se creó venta.
9. **Marcar pagada:** venta pendiente; quedó como pagada y el contador del cliente subió a 1.
10. **Cobro repetido:** venta ya pagada; la simulación devolvió `YaPagada` 6005 y el contador no se movió.
11. **Monto inválido:** venta con monto 0; la simulación devolvió `MontoInvalido` 6004 y no se creó venta.
12. **Baja con ventas:** cliente con historial; la simulación devolvió `ClienteConVentas` 6003 y las cuentas quedaron intactas.

## Cierre automático

Ejecuta `npm run verificar:entrega` antes de entregar. El gate revisa Program ID, IDL real, nombre del participante, ausencia de marcadores y firmas válidas; mientras quede algún marcador sin completar, el cierre falla y el repo no debe enviarse.
