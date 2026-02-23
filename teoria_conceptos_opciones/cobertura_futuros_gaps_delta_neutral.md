---
fecha_creacion: "2026-02-23"
fecha_edicion: "2026-02-23"
---
# Profundización: Cobertura con Futuros, Gaps y Delta-Neutralidad

Este documento amplía el concepto de utilizar la venta de futuros como una herramienta de cobertura, específicamente frente a escenarios de *gaps* violentos del mercado y cómo se logra una posición **simétrica o delta-neutral**.

## 1. El Problema de los Gaps y la Falla del Stop-Loss

Un **gap** (brecha o hueco) ocurre cuando el precio de apertura de un activo es significativamente distinto (mayor o menor) al precio de cierre del día anterior, sin que haya habido operaciones intermedias en esos niveles de precios. 

**¿Por qué suceden los gaps bajistas?**
Suelen darse por noticias negativas inesperadas publicadas con el mercado cerrado (ej. fines de semana, *after-market* o *pre-market*). Cuando el mercado abre, la abrumadora presión vendedora hace que el primer precio operado sea muy inferior al cierre anterior.

**La falla del Stop-Loss tradicional:**
Muchos inversores creen estar protegidos al colocar una orden *Stop-Loss* (ej. "vender mis acciones de GGAL si el precio cae de USD 45"). 
Sin embargo, un Stop-Loss se convierte en una **orden de mercado** una vez que se toca el precio de activación. Si GGAL cierra a USD 48 y, tras una mala noticia, abre al día siguiente directamente en USD 40 (un gap bajista):
- El Stop-Loss se activa porque el precio cayó por debajo de 45.
- Al ser una orden de mercado, buscará el mejor precio disponible *en ese momento*.
- Terminarás vendiendo tus acciones a USD 40 (o peor), asumiendo una pérdida mucho mayor a la planeada. **El Stop-Loss no garantiza el precio de ejecución en caso de gaps.**

## 2. La Solución: Venta de Futuros (Short Futures)

Un contrato de futuros obliga a las partes a comprar o vender un activo en una fecha futura a un precio pactado hoy. 
Si tienes una cartera de acciones (posición larga o *long*) y quieres protegerla de una caída, puedes **vender (ponerse corto o *short*) contratos de futuros** equivalentes sobre ese mismo activo o su índice de referencia.

### ¿Cómo protege contra el gap?
A diferencia del Stop-Loss, la ganancia o pérdida en un contrato de futuros es una liquidación matemática basada en la diferencia de precios. 
- Si compraste GGAL a USD 48 y vendiste un futuro de GGAL a USD 48 (simplificando la tasa de interés implícita).
- Si al día siguiente GGAL abre con un gap en USD 40.
- Tus acciones perdieron USD 8 por acción.
- Sin embargo, tu contrato de futuros vendido ahora vale USD 40. Como tú tienes el compromiso de vender a 48 algo que en el mercado vale 40, tu posición corta en futuros tiene una ganancia de USD 8 por acción.
- **Resultado Neto:** La pérdida en las acciones (-8) se anula con la ganancia en el futuro (+8). **Tu pérdida por el gap fue congelada perfectamente.**

## 3. Cobertura Simétrica y "Delta-Neutral"

Este efecto de anulación se conoce en finanzas como cobertura simétrica o portafolio **Delta-Neutral**.

**¿Qué es Delta?**
Es una "griega" que mide cuánto cambia el valor de un derivado por cada unidad ($1) que cambia el activo subyacente.
- Una acción comprada tiene un Delta de **+1.0** (si la acción sube $1, ganas $1).
- Un futuro vendido tiene un Delta de **-1.0** (si el subyacente sube $1, pierdes $1 en el futuro; si cae $1, ganas $1).

**Logrando la Delta-Neutralidad:**
Al sumar ambos deltas en tu cartera: `(+1.0) + (-1.0) = 0`.
Tu posición total tiene un **Delta 0**. Esto significa que es **inmune** a los movimientos direccionales del precio. No importa si GGAL se desploma un 50% de la noche a la mañana (un gap extremo); el valor de tu portafolio no cambiará porque las ganancias del futuro absorberán las pérdidas de la acción peso por peso.

### Ventajas de esta cobertura:
1. **No hay "Time Decay" (Theta):** A diferencia de las opciones (Puts), los futuros no pierden valor simplemente por el paso del tiempo. No hay un "costo de seguro" o prima inicial fuerte que pagar (solo se debe gestionar el margen de garantía).
2. **Independencia de la Volatilidad Implícita (Vega):** Las opciones se encarecen brutalmente antes de eventos de riesgo (balances, elecciones) debido a la alta demanda por protección. Los futuros operan direccionalmente y no sufren esta "inflación" de primas por miedo.
3. **Simetría perfecta para desarmar riesgo:** Es la forma más barata y eficiente de "apagar" tu exposición al mercado temporalmente (ej. durante un fin de semana largo con incertidumbre) sin tener que vender y luego recomprar tus acciones subyacentes (evitando así comisiones dobles de *trading* o implicancias impositivas).

### Desventajas o riesgos a considerar:
- **Costo de Oportunidad (Subida simétrica):** Al igual que congela las pérdidas, congela las ganancias. Si la acción sube con un gap alcista, ganarás en la acción pero perderás lo mismo en el contrato de futuros.
- **Riesgo de Margen (Margin Call):** Las diferencias de futuros se liquidan diariamente (*Mark-to-Market*). Si el mercado sube, el broker te exigirá depositar más dinero (garantías) para cubrir las pérdidas de tu posición corta en futuros, aunque tus acciones estén subiendo (un problema de liquidez, no de insolvencia).

---

### Fuentes recomendadas
- **CME Group - Education:** [Hedging with Futures](https://www.cmegroup.com/education/courses/introduction-to-futures/hedging-with-futures.html) (Explica el concepto de cobertura simétrica para portafolios de acciones).
- **Investopedia:** 
  - [Delta Neutral](https://www.investopedia.com/terms/d/deltaneutral.asp) (Definición matemática y aplicación práctica en el armado de carteras).
  - [Gap Risks](https://www.investopedia.com/terms/g/gap.asp) (Los riesgos del gap de mercado y por qué las órdenes limitadas y *stops* son vulnerables a ellos).
- **Hull, John C.** - *"Options, Futures, and Other Derivatives"*. (Capítulos dedicados a "Hedging Strategies Using Futures", donde especifica el cálculo matemático del ratio de cobertura y los riesgos de base).
