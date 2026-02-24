---
fecha_creacion: "2026-02-23"
fecha_edicion: "2026-02-23"
---
# Estrategia Macro Aplicada: El "Double Diagonal Spread" (GGAL Abr/Jul)

La premisa táctica planteada de **"aprovechar la lateralización hasta abril, mientras construyo un escenario de alta volatilidad para julio"** es quizás la lectura más sofisticada posible para el actual contexto de compresión (olla a presión) en GGAL.

Para monetizar este doble escenario –lateral a corto plazo, explosivo a largo plazo– operando exclusivamente los rebotes (pisos y techos) del rango, la estructura óptima a construir en el mercado se denomina **Double Diagonal Spread** (o *Diagonal Strangle*). *(Para comprender las mecánicas contables atemporales y las matemáticas detrás de esta matriz de cuatro patas, ver la [Teoría Fundamental del Double Diagonal Spread](../teoria_conceptos_opciones/teoria_double_diagonal_spread.md))*

## 1. La Arquitectura de la Estrategia (Mecánica Doble)

Un *Double Diagonal* permite jugar a dos bandas temporales distintas al mismo tiempo, combinando un spread de tiempo (*Calendar*) con un spread de precio (*Strangle*). 

> **Aclaración sobre Strikes:** La elección entre usar el *mismo* Strike (Calendar puro) o Strikes *distanciados* (Diagonal) define la agresividad de la posición. Usar misos Strikes maximiza el cobro de prima pero acota las ganancias si ocurre un desvío brusco del ADR. Para un desglose matemático sobre esto, ver: [Diferencias entre Strikes y Riesgo de Ejercicio](../teoria_conceptos_opciones/teoria_strikes_y_ejercicio_calendar.md).

**Paso A: Operar el "Piso" (Soporte del Rango)**
Cuando GGAL cae de precio y toca el piso del rango lateral esta semana:
1. **Compramos un CALL de JULIO** OTM (Out of The Money, ej. Base alta a futuro). Al ser un contrato lejano, estamos acumulando la pata alcista para la explosión futura, aprovechando que al tocar el piso, los Calls están rematados de precio.
2. **Vendemos un CALL de ABRIL** OTM (Base cercana al techo del rango). Como la acción rebotó en el piso, sabemos que le costará romper el techo antes de abril. Cobramos esta prima carísima para financiar nuestra compra de julio y atrapar el valor tiempo (*Theta Decay*).

**Paso B: Operar el "Techo" (Resistencia del Rango)**
Días después, cuando la acción sube y se estampa contra el techo de la lateralización:
1. **Compramos un PUT de JULIO** OTM (Base baja a futuro). Como hay euforia por el rebote, los Puts se desplomaron. Compramos "seguros contra cisnes negros" regalados para acumular la pata bajista de la explosión futura.
2. **Vendemos un PUT de ABRIL** OTM (Base cercana al piso del rango). Nos pagan fortunas por este seguro de caída a corto plazo. Como sabemos que el piso es fuerte hasta abril (efecto balanza institucional), cobramos esta prima también.

## 2. Los Flujos de Caja (Por qué esto es una obra de arte financiera)

Al finalizar ambos *legging-in* (entradas por patas en el piso y en el techo), la cartera de opciones queda armada así:
- **Corto Plazo (Abril):** Tienes un *Short Strangle* o Cuna Vendida (Calls y Puts vendidos). Mientras GGAL rebote estúpidamente entre el piso y el techo de acá a abril, ambas opciones perdén valor todos los días por el paso del reloj (*Theta Decay*). Al llegar el vencimiento de abril, ambas expiran sin valor. Te quedas con el 100% de la prima cobrada por venderlas.
- **Largo Plazo (Julio):** Tienes un *Long Strangle* (Calls y Puts comprados). **¡Magia financiera!** La prima que cobraste por vender las opciones de abril ha financiado (e incluso abaratado a cero) el costo de haber comprado tus seguros para julio.

Llega Mayo, las opciones de abril desaparecieron dejándote ganancia limpia. Ahora estás posicionado "gratis" con Puts y Calls comprados para Julio. Si el acuerdo arancelario de Trump o la morosidad del Galicia explotan, tu estructura de largo plazo captura la suba de la volatilidad (Expansión de *Vega*) y el movimiento direccional sin límite (*Gamma/Delta*).

## 3. Consideraciones de Riesgo del "Double Diagonal"
A pesar de su ingeniería perfecta, ninguna estrategia es a prueba de balas:
- **Rotura Anticipada Constatada:** La premisa fundamental para no quebrar es que tenés razón sobre que **abril es la fecha bisagra** ("Wait and See" de los *Earnings*). Si la explosión de volatilidad ocurre en **marzo** rompiendo violentamente el techo, los Calls de abril que *vendiste* van a empezar a causarte pérdidas masivas de capital antes de que puedas compensarlas por completo. Requieren un manejo activo (cerrar las opciones cortas de abril ante rotura confirmada de resistencia con cierre diario).

### Conclusión Estratégica
Esta maniobra no es para novatos: requiere gestionar cuatro "patas" distintas y operar inteligentemente ejecutando órdenes contrarias en soportes y resistencias. Un evento fundamental a monitorear como Vendedor (Lanzador) en derivados es **no llegar nunca al vencimiento** si tus contratos de Abril de corto plazo han sido vulnerados o superados por el mercado (*pasaron In-The-Money*); bajo riesgo de sufrir un Ejercicio Forzoso sobre tu cuenta (ver [Riesgo de Ruina por Ejercicio](../teoria_conceptos_opciones/teoria_strikes_y_ejercicio_calendar.md)). Es el reflejo táctico matemático exacto a tu lectura del mercado actual pero demanda control estricto del *Stop Loss* u órdenes defensivas inter-mes *(Para entender la mecánica, beneficios y costos ocultos de salvar posiciones pateándolas al futuro, ver: [Mecánica y Costos del Roll Over](../teoria_conceptos_opciones/mecanica_roll_over_opciones.md))*.

---

### Fuentes recomendadas
- **McMillan, Lawrence G.** - *"Options as a Strategic Investment"*. (La biblia de las estrategias cruzadas, con un capítulo profundo sobre el *Diagonal Calendar Spread* dictando cómo el "volatility skew" abarata las opciones de largo plazo frente a los vencimientos inminentes).
- **Investopedia:** 
  - [Diagonal Spread](https://www.investopedia.com/terms/d/diagonalspread.asp) (Para entender la combinación híbrida entre el factor temporal de calendario y la separación de precios de ejecución *Strikes*).
