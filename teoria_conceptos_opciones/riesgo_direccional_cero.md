---
fecha_creacion: "2026-02-23"
fecha_edicion: "2026-02-23"
---
# Profundización: Riesgo Direccional Cero y Arbitraje (Reversal / Conversion)

Este documento amplía el concepto de tener un **riesgo direccional CERO** cuando se combina una posición en opciones sintéticas con el activo subyacente.

## 1. ¿Qué significa que el "Riesgo Direccional es CERO"?

En el mundo del trading, el **riesgo direccional** es la exposición que tiene tu cartera a los movimientos de precio de mercado de un activo. 
- Si compras una acción pura, tienes riesgo direccional alcista (ganas si sube, pierdes si baja).
- Si vendes una acción en corto, tienes riesgo direccional bajista (ganas si cae, pierdes si sube).

Tener **Riesgo Direccional CERO** significa que la estructura que armaste es **inmune matemáticamente** a las subidas o bajadas del precio del activo (lo que también se conoce como posición *Delta-Neutral* de forma estática y definitiva hasta el vencimiento). No importa si el precio de GGAL se desploma a la mitad o se multiplica por tres; el valor monetario final de tu posición combinada no cambiará como consecuencia exclusiva de ese movimiento de precio.

## 2. ¿Por qué ocurre esto en este caso?

Recordemos la estructura mencionada: 
> "Compras un Call y vendes un Put (Sintética Larga) y simultáneamente vendes la Acción real (Short) o vendes un Futuro"

Esta estructura se llama **Reverse Conversion** (o *Reversal*). Veamos paso a paso cómo los movimientos se anulan perfectamente entre sí, asumiendo que las opciones tienen el mismo precio *strike* (ej. USD 200) y la misma fecha de vencimiento.

### Desglose de piezas:
1. **Sintética Larga (Comprar Call 200 + Vender Put 200):** Esto replica matemáticamente el comportamiento exacto de tener comprada 1 acción. 
   - *Su Delta combinado es +1.0.*
2. **Short Action / Short Future (Vender la Acción real o Futuro a 200):** Esto genera dinero cuando la acción cae y pierde cuando sube.
   - *Su Delta es -1.0.*

### Escenarios de anulación al vencimiento:
Supongamos que armamos esta estructura y mantenemos todas las piezas hasta el día de expiración de las opciones.

**Escenario A: GGAL se dispara a USD 300**
- **Qué pasa con tus opciones:** Ejerces el **Call** que compraste. Tienes el derecho intocable a comprar GGAL a USD 200. Como en bolsa vale 300, **ganas USD 100**. El **Put** que vendiste expira sin valor porque a nadie le interesa ejercer el derecho de venderte a 200 algo que en mercado vale 300 (tu riesgo ahí fue nulo).
- **Qué pasa con tu Acción/Futuro Vendido:** Al estar en corto ("apostando a la baja") desde USD 200 y el precio subir libremente a 300, **pierdes USD 100**.
- **Resultado Neto:** Ganancia de +USD 100 (Opciones) sumada a la pérdida de -USD 100 (Acción) = **USD 0**. El fuerte movimiento direccional alcista de la acción fue neutralizado al 100%.

**Escenario B: GGAL se desploma a USD 100**
- **Qué pasa con tus opciones:** El **Call** que compraste expira sin valor (obviamente no ejercerás el derecho a comprar a 200 algo que ahora vale 100). Pero el **Put** que vendiste sí te obligará a actuar: el comprador del Put ejercerá su derecho y te obligará a comprarle sus GGAL a USD 200. Si compras a 200 algo que en mercado vale 100, **pierdes USD 100**.
- **Qué pasa con tu Acción/Futuro Vendido:** Al estar en corto desde USD 200 y el mercado desplomarse a 100, puedes recomprar todo más barato y consolidar una ganancia por la diferencia. **Ganas USD 100**.
- **Resultado Neto:** Pérdida de -USD 100 (Opciones) sumada a la ganancia de +USD 100 (Acción) = **USD 0**. La estrepitosa caída de GGAL fue contrarrestada milimétricamente.

### Entonces, si siempre da USD 0 de movimiento en precio, ¿para qué se hace?
Debido a imperfecciones temporales del mercado, pánico, o presiones de flujo por grandes coberturas institucionales, los precios **iniciales de armado** de las piezas individuales (*Call*, *Put*, *Futuro*) no siempre se alinean perfectamente. 

En situaciones donde los Puts están anormalmente sobrevalorados por miedo (alta volatilidad implícita en la caída), el operador puede cobrar tanta prima cara vendiendo el Put y vendiendo el Futuro que supera holgadamente lo que gasta comprando el Call. 
Esto genera un **crédito neto inicial**. Como acabamos de demostrar matemáticamente que el riesgo por el movimiento del precio fue blindado y es CERO, ese crédito de dinero te lo quedas sin sufrir estrés alguno por hacia dónde vaya la acción. Ese flujo de caja retenido en el tiempo te arroja una **tasa de interés implícita** (prácticamente libre de riesgo soberano). 
Si esa tasa lograda armando las cuatro patas excede a la tasa estándar del mercado (ej. cauciones bursátiles o letras del tesoro), los agentes financieros armarán la estructura de "Reverse Conversion" o "Conversion" masivamente para "imprimir" esa rentabilidad sin asumir riesgos del mercado accionario.

---

### Fuentes recomendadas
- **Natenberg, Sheldon** - *"Option Volatility and Pricing"*. (Explica las estrategias de conversión y reversión como operaciones de puro arbitraje de tasas de interés, detallando matemáticamente el riesgo cero sobre el subyacente).
- **Investopedia:** 
  - [Reverse Conversion](https://www.investopedia.com/terms/r/reverseconversion.asp) (Para entender la mecánica paso a paso de vender un put, comprar un call y ponerse corto en la acción para capturar ineficiencias de opciones sin riesgo direccional).
