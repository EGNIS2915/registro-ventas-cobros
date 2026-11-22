# Arquitectura y defensa — Registro de cobros

Participante: **Egnis Piliado Montaño** · Red: **Devnet** · Ruta: proyecto guiado con mejora funcional.

## Modelo de cuentas y PDAs

| Cuenta | Seeds | Datos relevantes |
| --- | --- | --- |
| `Registro` | `["registro", nombre_negocio, owner]` | `owner`, `nombre_negocio`, `clientes`, `id_counter` |
| `Cliente` | `["cliente", registro, id_cliente_le]` | `id_cliente`, `nombre`, `compras`, `historial`, `ventas_pagadas` |
| `Venta` | `["venta", cliente, sku]` | `sku`, `descripcion`, `monto`, `pagada` |

El `id_cliente` se serializa en dos bytes little-endian y el `id_counter` del registro solo avanza, nunca se reutiliza: dar de baja a un cliente no permite que otro tome su ID.

## Autoridad y pertenencia

- `owner` es un `Signer` y el `Registro` lleva `has_one = owner @ NoOwner`: otra wallet puede leer, pero no escribir.
- `NuevoCliente` exige que el `Registro` pertenezca al firmante y calcula el seed del cliente con `id_counter + 1`.
- `EliminarVenta` y `BajaCliente` usan `close = owner`, con lo que la renta vuelve a la autoridad.
- `BajaCliente` solo acepta clientes sin historial (`ClienteConVentas`) y comprueba que la cuenta siga referenciada en el registro (`NoClienteEnRegistro`).

## Aporte funcional: control de cobros

La base del bootcamp registro, cliente, venta, devolución y baja. El aporte propio cierra el ciclo de cobranza:

1. `marcar_pagada` cambia `Venta.pagada` a `true` y aumenta `Cliente.ventas_pagadas`.
2. Un segundo intento sobre la misma venta falla con `YaPagada` (6005): no se puede cobrar dos veces.
3. `hacer_devolucion` descuenta el contador si la venta ya estaba pagada, para que el resumen no quede inflado.
4. `registrar_venta` y `cambiar_monto` exigen `monto > 0` (`MontoInvalido`, 6004).
5. La UI muestra **Pagada / Pendiente** por venta y el total cobrado por cliente.

### Cómo se comprueba

| Caso | Acción | Resultado |
| --- | --- | --- |
| Cobro | `Marcar pagada` en una venta pendiente | Badge *Pagada*, contador +1, firma en Explorer |
| Doble cobro | Repetir `Marcar pagada` | Error 6005, sin segunda firma de éxito |
| Monto cero | `Registrar venta` con 0 | Error 6004, sin cuenta `Venta` creada |
| Devolución | `Devolución` de una venta pagada | Cuenta cerrada y contador descontado |
| Autoridad | Escritura con otra wallet | Error 6000 |
| Baja bloqueada | `Dar de baja` con historial | Error 6003, cliente y referencias intactos |

## Errores del programa

| Código | Nombre | Significado |
| --- | --- | --- |
| 6000 | `NoOwner` | La wallet no es autoridad del registro |
| 6001 | `NoSKU` | La venta no está en el historial del cliente |
| 6002 | `NoClienteEnRegistro` | El cliente no pertenece al registro |
| 6003 | `ClienteConVentas` | No se puede dar de baja con ventas activas |
| 6004 | `MontoInvalido` | El monto debe ser mayor a cero |
| 6005 | `YaPagada` | La venta ya fue cobrada |

## Demo de 60 segundos

1. Conectar Solflare en **Devnet** y mostrar la wallet pública (0:00–0:08).
2. `Crear registro` para `Cafe Cobros Egnis` y esperar la confirmación (0:08–0:18).
3. `Crear cliente` y `Registrar venta` con SKU `CAF01` (0:18–0:32).
4. `Marcar pagada`: resaltar el badge y el contador (0:32–0:42).
5. Repetir `Marcar pagada`: mostrar el rechazo `YaPagada` (0:42–0:52).
6. Abrir la firma en `explorer.solana.com?cluster=devnet` (0:52–1:00).

## Seguridad y alcance

El cliente comprueba el genesis de Devnet antes de firmar, conserva la firma si se pierde la confirmación y traduce los errores del programa. No se guardan semillas, claves ni `keypair.json`. El IDL entregado debe ser el exportado del despliegue; mientras `esReferencia` sea `true`, la UI bloquea escrituras a propósito.
