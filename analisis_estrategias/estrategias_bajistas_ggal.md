---
fecha_creacion: "2026-03-03"
fecha_edicion: "2026-03-03"
---

# Análisis de Estrategias Bajistas para GGAL

Ante la hipótesis de que el mercado (y en particular GGAL) tendrá un comportamiento bajista, la selección de la estrategia con opciones dependerá fuertemente del nivel de agresividad deseado y de la necesidad de cobertura contra escenarios adversos si la premisa falla.

## 1. Maximizar la Tendencia Bajista (Alta Agresividad)

Para maximizar una tendencia bajista pura direccional, la forma clásica es mediante la compra de opciones **PUT** o el armado de *Spreads de débito*.

### 1.1 Compra de un Long PUT
La compra directa de un PUT ofrece un beneficio creciente a medida que el precio del activo subyacente cae, manteniendo un riesgo máximo estrictamente limitado a la prima (prima pagada) inicial ([Investopedia: Long Put](https://www.investopedia.com/terms/l/long_put.asp)). 

**¿Cómo elegir el Strike?**
La elección del precio de ejercicio (strike) depende del balance deseado entre probabilidad de acierto, apalancamiento y mitigación de la decadencia temporal (Theta):
- **PUT In The Money (ITM):** Posee un Delta absoluto alto (ej. -0.70 a -0.80). Copia casi directamente el movimiento bajista del papel de forma lineal. Tiene el menor componente de valor extrínseco, por lo que sufre menos por el paso del tiempo comparado con los opciones ATM ([CME Group: Delta and Probabilities](https://www.cmegroup.com/education/courses/option-greeks/options-deltas-probabilities.html)). Es la forma direccional más conservadora de ir corto con opciones.
- **PUT At The Money (ATM):** Contienen el mayor valor extrínseco y la mayor curvatura (Gamma alta). Si se espera un desplome *inminente y violento*, el ATM brinda la mejor aceleración rápida de ganancias. Sin embargo, si GGAL llegara a lateralizar, será la base más duramente castigada por el Theta ([Charles Schwab: Options Theta Explained](https://www.schwab.com/learn/story/options-theta-explained)).
- **PUT Out of The Money (OTM):** Son baratos y ofrecen el mayor apalancamiento matemático porcentual en caso de un derrumbe, pero tienen una probabilidad muy baja de quedar en ganancia. Requieren un salto en el precio fuerte y rápido para alcanzar el punto de equilibrio.
- *(Suposición del agente)*: Especialmente para GGAL, cuya volatilidad implícita (IV) suele ser errática o habitualmente alta (lo que encarece los puts), ir fuertemente ITM suele ser lo más prudente al ir largo en prima, para mitigar el golpe de volatilidad si el activo cae más lento de lo pensado.

### 1.2 Bear Put Spread (Spread Bajista con Puts)
Si se desea maximizar el retorno sobre el capital invertido reduciendo el costo inicial, se implementa un **Bear Put Spread**. Consiste en comprar un PUT (generalmente ATM o levemente ITM) y vender simultáneamente otro PUT idéntico pero de un strike menor (es decir, más OTM) ([Investopedia: Bear Put Spread](https://www.investopedia.com/terms/b/bearputspread.asp)).
- **Ventaja**: Financiar parte del PUT principal con la prima del PUT vendido. Esto atenúa el drenaje del devaluado temporal (Theta) y compensa las posibles caídas bruscas de volatilidad (Vega).
- **Desventaja**: El beneficio máximo está "capeado" o truncado a la diferencia (ancho) entre los dos strikes, menos el débito pagado, sin importar si GGAL cae infinitamente por debajo del strike vendido.

---

## 2. Aprovechar Tendencia Bajista con Cobertura y Neutralidad

Si el inversor quiere aprovechar su visión bajista, pero teme equivocarse (ej: GGAL finalizando en terreno verde el día o semana de expiración por factores exógenos), la compra directa de puts es riesgosa. Aquí entran en juego estrategias que aprovechen un sesgo direccional mientras aplican **cobertura o mitigación asimétrica de riesgo**.

### 2.1 Bear Call Spread (Credit Spread Bajista)
En vez de pagar una prima para entrar al mercado especulando con la caída (débito), el inversor puede operar armando una posición que le paguen hoy a cambio de absorber algo de riesgo acotado (crédito). Un **Bear Call Spread** se forma vendiendo un CALL "cerca" del precio actual de mercado y, comprando (a modo de seguro inquebrantable) un CALL de strike superior más OTM ([Investopedia: Bear Call Spread](https://www.investopedia.com/terms/b/bearcallspread.asp)).
- **Ventaja probabilística**: El inversor gana en tres (3) de cuatro posibles escenarios (las opciones tienen una alta probabilidad de expirar sin valor relativo): GGAL cae mucho, GGAL solo baja levemente, e incluso **si GGAL se mantiene lateral / subiendo ligeramente** siempre y cuando el precio cierre por debajo de la base del CALL lanzado. A diferencia del Bear Put Spread, estas estrategias capitalizan el Theta positivo diariamente.
- **Cobertura integrada**: La compra de la opción larga (protección OTM) frena las potenciales pérdidas netas ante eventos imponderables y rebotes sorpresivos violentos ("Short squeeze" del activo), frenando toda exposición nociva de capital.

### 2.2 Put Ratio Backspread
Se trata de una estrategia pensada operativamente como una cobertura asimétrica "gratis" o altamente barata. El inversor vende 1 opción PUT con strike cercano al precio actual y con ese cobro, financia la compra de 2 o más PUTs netamente OTM ([Corporate Finance Institute: Put Ratio Backspread](https://corporatefinanceinstitute.com/resources/derivatives/put-ratio-backspread/)). 
- Si GGAL sube sorpresivamente (error de dirección de mercado), el diferencial devengado de la operación arroja un crédito inicial neto nulo o ligeramente positivo. El inversor pierde poca o incluso una suma mínima, manteniendo la prima ganada. Cobertura inquebrantable hacia el sesgo alcista.
- Si GGAL colapsa velozmente, a partir de cierto nivel de derribo inferior en breakeven, los PUT largos extra inyectan utilidades que vuelan hacia infinito de la misma forma de un simple Long PUT agresivo. 
- *Riesgo*: Padecen la zona "valle" donde GGAL llegue a caer parcialmente y posarse justo en los strikes comprados durante el punto de expiración.

---

### Fuentes recomendadas
- *Option Volatility and Pricing* (Sheldon Natenberg) — (*Sustento matemático de alto nivel para internalizar las relaciones y la selección fina del Strike cruzado vs Delta, Vega y Theta cuando se persiguen tendencias direccionales largas.*)
- [Investopedia: Long Put](https://www.investopedia.com/terms/l/long_put.asp), [Bear Put Spread](https://www.investopedia.com/terms/b/bearputspread.asp), y [Bear Call Spread](https://www.investopedia.com/terms/b/bearcallspread.asp) — (*Vías de consulta conceptual sobre arquitecturas, límites de perfiles de riesgo y bases de armado simple de opciones bajistas.*)
- [CME Group: Delta and Probabilities](https://www.cmegroup.com/education/courses/option-greeks/options-deltas-probabilities.html) — (*Artículo educativo principal usado para deducir qué Strike y probabilidad matemática real tiene la vía del Long Put en función a su tipo.*)
- [Charles Schwab: Options Theta Explained](https://www.schwab.com/learn/story/options-theta-explained) — (*Conceptos de las griegas, confirmación del mayor valor extrínseco en opciones ATM y su consecuente mayor decaimiento temporal (Theta) respecto a ITM o OTM.*)
- [Corporate Finance Institute: Put Ratio Backspread](https://corporatefinanceinstitute.com/resources/derivatives/put-ratio-backspread/) — (*Visión global de las opciones armadas asimétricamente frente a caídas explosivas combinadas con defensividad pasiva al alza.*)
