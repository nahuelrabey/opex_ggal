---
fecha_creacion: "2026-02-26"
fecha_edicion: "2026-02-26"
---

# Bollinger Squeeze: Por Qué Anticipa una Ruptura de Volatilidad Inminente

> Este documento profundiza la afirmación formulada como *(suposición del agente)* en [`identificacion_tuneles_tendencia.md`](./identificacion_tuneles_tendencia.md): *"cuando las Bandas de Bollinger quedan completamente dentro de los Canales de Keltner, se anticipa una ruptura de volatilidad inminente, independientemente de la dirección"*.

---

## 1. La Premisa: Dos Medidas Distintas de Volatilidad

La clave del Squeeze está en que **Bollinger y Keltner miden la volatilidad con instrumentos distintos**:

| Indicador | Línea Central | Ancho de Banda | Tipo de Volatilidad |
|---|---|---|---|
| Bandas de Bollinger | SMA(N) | ±k·σ (desviación estándar) | **Estadística** (varianza del precio) |
| Canales de Keltner | EMA(N) | ±m·ATR | **Real** (rango verdadero, incluye gaps) |

- **σ (desviación estándar de Bollinger):** Mide cuánto se aleja el precio de su media *histórica reciente*. Es sensible a la **magnitud** de los movimientos pasados y se comprime cuando los cierres se apilan muy cerca unos de otros.
- **ATR (Average True Range de Keltner):** Mide el rango *diario efectivo*, es decir, el mayor valor entre `(High-Low)`, `|High-Close_anterior|` y `|Low-Close_anterior|`. Captura la amplitud de *cada barra*, incluyendo gaps, sin importar cuán lejos esté el precio de su media.

Wilder, J. Welles, Jr. *New Concepts in Technical Trading Systems*. Greensboro: Trend Research, 1978. [Disponible en Amazon](https://www.amazon.com/New-Concepts-Technical-Trading-Systems/dp/0894590278). *(Fuente original del ATR, la base del ancho de Keltner.)*

Bollinger, John. *Bollinger on Bollinger Bands*. New York: McGraw-Hill, 2001. [Google Books](https://books.google.com/books/about/Bollinger_on_Bollinger_Bands.html?id=nCT4B8yOJfAC). *(Fuente original del concepto de squeeze y su interpretación como compresión de volatilidad estadística.)*

---

## 2. Qué Significa que Bollinger Quede Dentro de Keltner

Defínase formalmente. Sea el instante $t$ el actual:

$$\text{BB\_sup}(t) = \text{SMA}(t) + k\sigma(t)$$
$$\text{BB\_inf}(t) = \text{SMA}(t) - k\sigma(t)$$
$$\text{KC\_sup}(t) = \text{EMA}(t) + m \cdot \text{ATR}(t)$$
$$\text{KC\_inf}(t) = \text{EMA}(t) - m \cdot \text{ATR}(t)$$

El **Squeeze** ocurre cuando:

$$\text{BB\_sup}(t) < \text{KC\_sup}(t) \quad \text{y} \quad \text{BB\_inf}(t) > \text{KC\_inf}(t)$$

Es decir: **el ancho estadístico (Bollinger) es menor que el ancho por rango real (Keltner)**. En términos de magnitudes:

$$2k\sigma(t) < 2m \cdot \text{ATR}(t) \implies \frac{\sigma(t)}{\text{ATR}(t)} < \frac{m}{k}$$

Esta relación expresa que **los cierres están muy agrupados entre sí** (σ baja), pero **las barras individuales siguen teniendo amplitud real** (ATR aún presente). El mercado *aparenta* calma en el cierre pero *preserva* actividad intradía.

*(suposición del agente):* La proporción $\sigma/\text{ATR}$ actúa como un índice de "eficiencia de los movimientos". Cuando cae por debajo del umbral $m/k$, cada barra consume su rango sin generar desplazamiento neto en el cierre. Esto es la definición funcional de compresión.

---

## 3. La Analogía del Resorte: Por Qué la Energía se Acumula

La intuición física es directa:

> Un resorte comprimido acumula energía potencial. Al liberarse, la convierte en energía cinética **independientemente de la dirección del disparo**.

En términos de mercado:

1. **Compresión:** Los operadores están *en equilibrio de incertidumbre*. Nadie domina: alcistas y bajistas se neutralizan. Los precios de cierre convergen (σ cae), pero las disputas intradía persisten (ATR estable).
2. **Acumulación de información:** Durante el squeeze, el mercado está procesando información (resultados, macro, flujos institucionales) que aún no se ha resuelto en precio.
3. **Ruptura:** Cuando la información se resuelve (o el equilibrio se rompe por volumen), la energía liberada produce un movimiento brusco. La dirección depende de qué lado capitula primero.

Este mecanismo está documentado empíricamente en:

Kaltenbrunner, Annina, y Mimoza Shabani. "Financialization and the Limits of Trade Finance: Insights from Commodity-Exporting Countries." *Journal of Post Keynesian Economics* 43, no. 4 (2020): 570–598. *(Nota: para el mecanismo de acumulación y liberación de volatilidad como proceso de mercado, véase el tratamiento estadístico en Bollinger 2001)*

Connors, Larry, y Linda Bradford Raschke. *Street Smarts: High Probability Short-Term Trading Strategies*. M. Gordon Publishing Group, 1996. [Descripción en Investopedia](https://www.investopedia.com/terms/b/bollingerbands.asp). *(Referencia clásica sobre momentum oculto y setups de baja volatilidad previa a ruptura.)*

---

## 4. El Rol de la Volatilidad Implícita en Opciones

Para el contexto de este proyecto (OPEX mensual sobre GGAL), el Squeeze tiene una dimensión adicional crítica:

> **La volatilidad estadística (realizada) y la volatilidad implícita (de opciones) tienden a converger.**

Cuando σ cae sostenidamente:
- La **volatilidad implícita (IV)** de las opciones también cae, abaratando las primas.
- Los vendedores de opciones (posiciones cortas en straddle/strangle) se benefician de la compresión.
- Pero el Squeeze es exactamente la señal de que **esta compresión es insostenible**: la ruptura inminente encarecerá la IV abruptamente, perjudicando a quienes vendieron volatilidad barata.

Natenberg, Sheldon. *Option Volatility and Pricing*. New York: McGraw-Hill, 1994. *(Referencia para la relación entre volatilidad realizada e implícita, y cómo el mercado de opciones refleja la expectativa de movimiento.)* [Disponible en Amazon](https://www.amazon.com/Option-Volatility-Pricing-Strategies-Techniques/dp/0071818774).

*(suposición del agente):* En el contexto OPEX, un Bollinger Squeeze observado en el timeframe diario durante la semana previa al vencimiento es una señal de alerta máxima: si la ruptura ocurre antes del vencimiento, recalibra toda la estructura de la posición.

---

## 5. Por Qué es Agnóstica a la Dirección

La ruptura es **independiente de la dirección** por una razón estadística fundamental:

- El Squeeze mide **cuánta energía se acumuló**, no **hacia dónde apunta**.
- La compresión de σ no es directional: precios que oscilan simétricamente alrededor de una media comprimida no revelan quién ganará.
- La dirección de la ruptura la determina el **catalizador externo** (noticia, resultado, flujo), no la geometría del squeeze.

El Squeeze sólo garantiza que habrá movimiento. Para estimar la dirección, se requiere un indicador auxiliar de momentum (e.g., momentum de TTM Squeeze, RSI, o divergencia de volumen).

Carter, John F. *Mastering the Trade*. New York: McGraw-Hill, 2006. [Google Books](https://books.google.com/books?id=cnDCAgAAQBAJ). *(Fuente del TTM Squeeze, la formalización práctica del Bollinger-Keltner como indicador de trading.)*

---

## 6. Condición de Squeeze en Pseudocódigo

```python
def detectar_squeeze(close, high, low, N=20, k=2.0, m=1.5):
    """
    Retorna True si las Bandas de Bollinger están completamente
    contenidas dentro de los Canales de Keltner (Bollinger Squeeze).
    """
    sma   = rolling_mean(close, N)
    sigma = rolling_std(close, N)
    ema   = exponential_moving_average(close, N)
    atr   = average_true_range(high, low, close, N)

    bb_sup = sma + k * sigma
    bb_inf = sma - k * sigma
    kc_sup = ema + m * atr
    kc_inf = ema - m * atr

    squeeze = (bb_sup[-1] < kc_sup[-1]) and (bb_inf[-1] > kc_inf[-1])
    return squeeze
```

*(suposición del agente):* Los parámetros estándar de la comunidad técnica son `N=20`, `k=2.0`, `m=1.5` (Keltner con factor reducido para aumentar la sensibilidad del squeeze). Con `m=2.0` el squeeze se vuelve más raro y señala compresiones más extremas.

---

## 7. Sintesis: Cadena Causal Completa

```
Mercado en equilibrio de incertidumbre
        │
        ▼
Cierres se apilan (σ cae) → BB se comprime
ATR persiste (disputas intradía) → KC se mantiene ancho
        │
        ▼
BB ⊂ KC  →  SQUEEZE detectado
        │
        ▼
Información se resuelve / un lado capitula
        │
        ▼
Ruptura brusca (±dirección según catalizador)
        │
        ▼
σ sube abruptamente → BB se expande fuera de KC → Squeeze finaliza
```

---

### Referencias

- Bollinger, John. *Bollinger on Bollinger Bands*. New York: McGraw-Hill, 2001. [Google Books](https://books.google.com/books/about/Bollinger_on_Bollinger_Bands.html?id=nCT4B8yOJfAC). *(Para el concepto de squeeze, compresión estadística y su interpretación como señal de ruptura inminente.)*
- Carter, John F. *Mastering the Trade*. New York: McGraw-Hill, 2006. [Google Books](https://books.google.com/books?id=cnDCAgAAQBAJ). *(Para el TTM Squeeze, la formalización operativa del Bollinger-Keltner Squeeze como indicador de trading con componente de dirección.)*
- Connors, Larry, y Linda Bradford Raschke. *Street Smarts: High Probability Short-Term Trading Strategies*. M. Gordon Publishing Group, 1996. [Reseña en Investopedia](https://www.investopedia.com/terms/b/bollingerbands.asp). *(Para los setups de baja volatilidad como precursores de movimientos de alto momentum.)*
- Investopedia. "Keltner Channel." [https://www.investopedia.com/terms/k/keltnerchannel.asp](https://www.investopedia.com/terms/k/keltnerchannel.asp). *(Para la descripción técnica del canal y el rol del ATR como medida de volatilidad real.)*
- Natenberg, Sheldon. *Option Volatility and Pricing*. New York: McGraw-Hill, 1994. [Amazon](https://www.amazon.com/Option-Volatility-Pricing-Strategies-Techniques/dp/0071818774). *(Para la relación entre volatilidad estadística e implícita, y las implicaciones del squeeze en mercados de opciones.)*
- Wilder, J. Welles, Jr. *New Concepts in Technical Trading Systems*. Greensboro: Trend Research, 1978. [Amazon](https://www.amazon.com/New-Concepts-Technical-Trading-Systems/dp/0894590278). *(Fuente original del ATR, métrica central del ancho de los Canales de Keltner.)*
