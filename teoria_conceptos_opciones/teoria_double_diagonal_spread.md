---
fecha_creacion: "2026-02-23"
fecha_edicion: "2026-02-23"
---
# Teoría General: Double Diagonal Spread

El **Double Diagonal Spread** (o *Diagonal Strangle*) es una estrategia avanzada de opciones de cuatro patas (*legs*) que combina las características de un *Calendar Spread* (diferencia de tiempo o vencimiento) y un *Strangle* (diferencia de precios de ejecución o *strikes*). Posiciona matemáticamente al inversor para ser neutral al mercado a corto plazo (cobrando valor temporal), pero manteniéndolo cubierto o apalancado para movimientos direccionales extremos a largo plazo.

## 1. Arquitectura Teórica de la Posición

Para armar un Double Diagonal Spread, el operador debe estructurar simultáneamente (o de forma asíncrona mediante un *legging-in*) cuatro contratos distintos del mismo activo subyacente:
1. **Comprar un Call de Largo Plazo (OTM)**
2. **Vender un Call de Corto Plazo (OTM)** (Habitualmente con un strike más cercano al precio actual o idéntico)
3. **Comprar un Put de Largo Plazo (OTM)**
4. **Vender un Put de Corto Plazo (OTM)** (También con strike más cercano o idéntico)

La estructura neta final equivale a poseer un *Long Strangle* (Cuna Comprada) en el calendario lejano, financiada parcialmente por la venta ("lanzamiento en descubierto" tapado por las opciones largas) de un *Short Strangle* (Cuna Vendida) en el calendario inminente.

## 2. Motores de Ganancia (Mecánica de las Griegas)

Esta figura asimétrica está diseñada para explotar fallas teóricas u oportunidades en la estructura temporal (*Term Structure*) y la curva de volatilidad. Sus motores de rentabilidad son dos:

### A. Explotación de *Theta* (Decaimiento Temporal No Lineal)
El principio que hace funcionar esta estrategia es que **el valor extrínseco (temporal) de las opciones se degrada de forma acelerada o parabólica a medida que se acerca su expiración**. 
- Una opción que vence en 30 días pierde valor monetario por cada día que pasa a una velocidad mucho mayor (*alto Theta*) que una opción idéntica que vence en 180 días.
- Al vender la volatilidad de corto plazo, el trader cobra una prima que se evapora en su favor velozmente. Si la acción se consolida lateralmente (rango atrapado entre los *strikes* vendidos), estas opciones de corto plazo expirarán sin valor, permitiendo conservar el 100% de la prima cobrada.

### B. Beneficio por *Vega* (Expansión de Volatilidad a Futuro)
Una vez superada la expiración de la pata corta temporal, la posición se purifica en "Vega Positiva pura" (largo en opciones). 
Dado que el operador conserva las compras lejanas, un aumento contundente de la Volatilidad Implícita (IV) post-rango elevará radicalmente el precio de los seguros (Calls y Puts adquiridos). El coeficiente Vega en opciones distanciadas es numéricamente muy superior, por lo que una inyección de pánico global recompensa de forma asimétrica todo el capital residual de la estructura.

## 3. Riesgos Estructurales (Puntos de Quiebre)

Como toda estructura de crédito o débito mixto de múltiples patas, sus debilidades son focalizadas:
- **Riesgo Direccional Temprano (Explosión de *Gamma*):** Si el activo realiza un movimiento masivo (*Breakout* violento o *Crash*) **antes** de que venzan las opciones cortas, el precio perforará las barreras vendidas (entrando *In The Money* - ITM). Al faltar poco tiempo para su vencimiento, su reacción al precio (*Gamma*) se acelera agresivamente en contra del operador, forzando pérdidas en las opciones cortas que las opciones largas lentas no alcanzan a mitigar en magnitud con la misma velocidad.
- **El Letargo Perpetuo (*IV Crush* absoluto):** Si tras el vencimiento corto el mercado no rompe en la explosión esperada, la Volatilidad Implícita de la pata comprada comenzará a hundirse. Si no hay expansiones en la acción, el mismo *Theta Decay* que fue el aliado de corto plazo, se convertirá en el asesino silencioso del capital largo plazo, llevando los contratos remanentes a cero.

---

### Fuentes recomendadas
- **McMillan, Lawrence G.** - *"Options as a Strategic Investment"*. (Estudio definitivo sobre la interacción y compensación matemática de las griegas en los *Diagonal Spreads*, demostrando la superioridad estadística del cobro de *Theta No Lineal* en mercados estables limitados).
- **Investopedia:** 
  - [Diagonal Spread](https://www.investopedia.com/terms/d/diagonalspread.asp) (Desglose teórico de la fusión simultánea entre Spreads de Calendario y Spreads Verticales para operar volatilidad inter-mensual).
