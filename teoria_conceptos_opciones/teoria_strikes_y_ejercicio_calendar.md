---
fecha_creacion: "2026-02-23"
fecha_edicion: "2026-02-23"
---
# Profundización Teórica: Strikes y Ejercicio en Spreads Inter-Temporales

A raíz de las estrategias de rangos combinados (Abril/Julio), surgen dos dilemas fundamentales en la carpintería de las opciones: ¿se deben usar los mismos precios de ejecución (*Strikes*) para la compra y la venta? y ¿qué sucede si la pata corta explotara antes de tiempo?

## 1. Mismo Strike vs. Diferente Strike (Calendar vs. Diagonal)

Siguiendo el ejemplo práctico donde GGAL lateraliza entre 44 (Piso) y 55 (Techo):

**Escenario A: Mismo Strike (*Horizontal / Calendar Spread*)**
- *Ejemplo:* Comprás Call Julio 60 y Vendés Call Abril 60.
- *Mecánica:* Al usar el **mismo** strike, estás apostando *exclusivamente* al paso del tiempo (Theta) y a cambios en la Volatilidad Implícita inter-mensual. 
- *Pro:* Como vendés la misma base de 60, cobrás más prima de Abril porque el strike 60 está más cerca del precio actual (y del techo de 55) que un strike más alto. Al cobrar más, financiás mejor tu compra de Julio.
- *Contra:* El margen de ganancia direccional es nulo si el precio a futuro se "pasa de largo". Si en Abril la acción vale 70, lo que ganaste infinito con el Call de Julio lo perdés exactamente con el Call de Abril que vendiste. Se anulan mutuamente por encina del strike 60.

**Escenario B: Strikes Diferentes (*Diagonal Spread*)**
- *Ejemplo:* Comprás Call Julio 55 y Vendés Call Abril 65.
- *Mecánica:* Al usar un strike **diferente** (y más alejado) para la venta de corto plazo, estás dándole "espacio aéreo" a la acción para que suba sin que la opción que vendiste te empiece a lastimar financieramente.
- *Pro:* Si GGAL rompe sorpresivamente el techo de 55 en marzo, tu Call comprado de 55 para Julio se dispara de valor y entra en ganancia matemática (Gamma), mientras que tu Call vendido en Abril de 65 sigue a salvo (OTM) y perdiendo valor temporal. Ganás dinero por ambas puntas.
- *Contra:* El strike 65 en Abril está tan lejos que su prima valdrá moneditas. Financiarás muy poca parte de la compra del Call de Julio con esa venta. 

**Respuesta a tu intuición:** Sí, si coinciden en el mismo strike (60 y 60), tu potencial de ganancia máxima (Max Profit Peak) ocurre exactamente si la acción "clava" el precio de 60 en el vencimiento de Abril. Si lo supera, la ganancia **disminuye** velozmente. Por eso, en el Double Diagonal, los traders suelen comprar opciones largas un poco más cerca del dinero, y vender las opciones cortas más alejadas (ej. Comprar Jul 55, Vender Abr 60).

## 2. El "Riesgo de Ruina": ¿Qué pasa si te rompen el Strike en Abril?

La pesadilla operativa del vendedor de opciones (*Writer*) ocurre cuando la opción que vendiste de corto plazo expira *In The Money* (ITM).

Siguiendo el ejemplo (*Venta de Call Abril 60*):
Si en la semana de vencimiento de Abril, sorpresivamente se anuncia una megainversión y **GGAL se va a 70**, ocurren las siguientes reacciones en cadena si no intervienes:

1. **La Asignación Matemática (Ejercicio):** Como sos el vendedor del Call 60 de Abril, el comprador inicial ejercerá su derecho. **Estarás obligado por el mercado a venderle a él 100 acciones de GGAL a un precio de USD 60.**
2. **El Agujero Financiero:** Pero GGAL en el mercado real vale 70. Por ende, vos tendrás que comprar las acciones a 70 en el mercado y entregárselas a 60 al comprador. Estarás perdiendo 10 USD por acción.
3. **El Escudo (Rolling o Cierre):** Para evitar que el mercado ejerza tus opciones vendidas y te embargue la cuenta por vender acciones cortas, *ningún operador profesional llega al día del vencimiento con patas cortas ITM*. 
   - **La Solución Práctica:** Semanas u horas antes de la expiración de Abril, debes recomprar ("cerrar") ese Call de 60 aceptando la pérdida parcial. Para entonces, tu Call de Julio ya habrá subido estrepitosamente de precio absorbiendo la suba a 70, permitiéndote venderlo para cubrir tu pérdida en Abril y sacar tu ganancia residual.

Por lo tanto, si alguna vez tu Strike de corto plazo luce amenazado por el rally del precio subyacente, **debes cerrar la posición de Abril antes de su expiración** (recomprando la opción que vendiste originalmente) para evitar que te asigne el ejercicio en las cuentas comitentes.

---

### Fuentes recomendadas
- **Natenberg, Sheldon** - *"Option Volatility and Pricing"*. (Capítulos sobre *Assignment Risk* y la dinámica direccional delta-neutral versus delta-direccional en Spreads Temporales).
- **Investopedia:** 
  - [Early Exercise (Opciones Americanas)](https://www.investopedia.com/terms/e/earlyexercise.asp) (Para entender cuándo y por qué te podrían obligar a cumplir el contrato antes de la fecha si vendiste una pata corta muy *In-The-Money*).
