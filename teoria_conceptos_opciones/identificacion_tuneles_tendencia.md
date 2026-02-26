---
fecha_creacion: "2026-02-26"
fecha_edicion: "2026-02-26"
---

# Identificación Computacional de Túneles de Tendencia

La detección automática de túneles (canales) de tendencia o lateralización es fundamental para sistematizar estrategias de trading. A continuación, se describe un método basado en la **Regresión Lineal y Desviación Estándar**, junto con su aplicación multitemporal, y cinco métodos alternativos con sus implementaciones.

## 1. El Algoritmo: Bandas de Regresión Lineal (Linear Regression Channel)

Este método calcula una línea de tendencia central mediante el ajuste de mínimos cuadrados y proyecta bandas paralelas.

### Pasos del Algoritmo:
1.  **Selección de Datos:** Tomar un array de precios de cierre ($P$) de longitud $N$ (el "lookback period").
2.  **Cálculo de la Pendiente ($m$) e Intersecto ($b$):** Usar la fórmula de regresión lineal simple sobre el índice del tiempo ($t$):
    $$m = \frac{N\sum(tP) - \sum t \sum P}{N\sum t^2 - (\sum t)^2}$$
    $$b = \frac{\sum P - m \sum t}{N}$$
3.  **Línea Base (Trendline):** $Y_t = m \cdot t + b$.
4.  **Desviación Máxima:** Calcular el error residual máximo o la desviación estándar ($\sigma$) de los precios respecto a la línea base.
    - *Túnel Equidistante:* Se toma la mayor distancia absoluta observada entre un precio y la línea de regresión para definir el ancho del túnel.
5.  **Criterio de Categorización (suposición del agente):**
    - **Alcista:** Pendiente ($m$) positiva significativamente mayor a cero.
    - **Bajista:** Pendiente ($m$) negativa significativamente menor a cero.
    - **Lateralización:** Pendiente ($m \approx 0$) y precios oscilando dentro de un rango de $\sigma$ estrecho por un periodo prolongado.

## 2. Aplicación Multitemporal

El algoritmo debe ejecutarse de forma independiente para cada marco de tiempo (TF) para obtener una visión jerárquica:

- **Weekly (Semanal):** Identifica el túnel "macro". Sirve para determinar la dirección predominante de los ciclos económicos largos (Natenberg 1994).
- **Daily (Diario):** Identifica el túnel de mediano plazo. Es el que define la estrategia de opciones para el mes (OPEX).
- **1h (Una hora):** Identifica micro-tendencias dentro del túnel diario. Crucial para encontrar puntos de entrada/salida (timing).

*(suposición del agente)*: Un "Tunel Alcista" en 1h puede ser simplemente una corrección dentro de un "Tunel Bajista" diario. La clave computacional es validar que la posición del precio en el túnel menor esté en consonancia con los límites del túnel mayor.

## 3. Ejemplo en Pseudocódigo

```python
def detectar_tunel(precios, lookback):
    X = range(len(precios))
    m, b = linear_regression(X, precios)
    
    linea_base = [m*x + b for x in X]
    distancias = [abs(p - lb) for p, lb in zip(precios, linea_base)]
    ancho = max(distancias)
    
    if m > umbral_alcista:
        return "Túnel Alcista", ancho
    elif m < umbral_bajista:
        return "Túnel Bajista", ancho
    else:
        return "Lateralización", ancho
```

---

## 4. Métodos Alternativos para Identificar Túneles de Tendencia

### 4.1. Bandas de Bollinger

La línea central es una **Media Móvil Simple (SMA)** de $N$ períodos, y las bandas se proyectan a ±$k$ desviaciones estándar. A diferencia de la regresión lineal, la base no es una recta fija sino una media que sigue al precio en tiempo real. Las bandas se *expanden* en períodos de alta volatilidad y se *contraen* (squeeze) en períodos de baja volatilidad, señalando potenciales rupturas de rango.

Bollinger, John. *Bollinger on Bollinger Bands*. New York: McGraw-Hill, 2001. [Disponible en Google Books](https://books.google.com/books/about/Bollinger_on_Bollinger_Bands.html?id=nCT4B8yOJfAC).

```python
def bollinger(precios, N=20, k=2):
    sma = rolling_mean(precios, N)
    sigma = rolling_std(precios, N)
    banda_sup = sma + k * sigma
    banda_inf = sma - k * sigma

    ancho = banda_sup[-1] - banda_inf[-1]
    if precio_actual > sma[-1] and ancho > umbral_expansion:
        return "Túnel Alcista", ancho
    elif precio_actual < sma[-1] and ancho > umbral_expansion:
        return "Túnel Bajista", ancho
    else:
        return "Lateralización (squeeze)", ancho
```

*(suposición del agente)*: El umbral de expansión puede calibrarse como un percentil histórico del ancho de las bandas (e.g., si el ancho actual es mayor al percentil 50 de los últimos 252 días, se considera expansión).

---

### 4.2. Canales de Keltner

Los **Canales de Keltner** usan una **Media Móvil Exponencial (EMA)** como línea central y el **Average True Range (ATR)** multiplicado por un factor $m$ como ancho de banda. El ATR captura la volatilidad real del mercado incluyendo los gaps entre sesiones, volviéndose más robusto a spikes de volatilidad puntuales que la desviación estándar de Bollinger.

Keltner, Chester W. *How to Make Money in Commodities*. Kansas City: The Keltner Statistical Service, 1960. Descripción técnica secundaria en: Investopedia. "Keltner Channel." [https://www.investopedia.com/terms/k/keltnerchannel.asp](https://www.investopedia.com/terms/k/keltnerchannel.asp).

```python
def keltner(high, low, close, N=20, m=2):
    ema = exponential_moving_average(close, N)
    atr = average_true_range(high, low, close, N)
    banda_sup = ema + m * atr
    banda_inf = ema - m * atr

    if close[-1] > banda_sup[-1]:
        return "Túnel Alcista (ruptura)", atr[-1]
    elif close[-1] < banda_inf[-1]:
        return "Túnel Bajista (ruptura)", atr[-1]
    else:
        return "Lateralización", atr[-1]
```

*(suposición del agente)*: La combinación Bollinger + Keltner es especialmente útil: cuando las Bandas de Bollinger quedan completamente *dentro* de los Canales de Keltner (Bollinger Squeeze), se anticipa una ruptura de volatilidad inminente, independientemente de la dirección. → Ver análisis completo en [`bollinger_squeeze_ruptura_volatilidad.md`](./bollinger_squeeze_ruptura_volatilidad.md).

---

### 4.3. Canales de Donchian

Los **Canales de Donchian** definen las bandas como el **precio máximo y mínimo** de los últimos $N$ períodos. No existe una base estadística subyacente; el canal simplemente representa el rango histórico reciente. Si el precio rompe el máximo del canal, confirma tendencia alcista; si rompe el mínimo, tendencia bajista.

Donchian, Richard D. "Trend Following Methods in Commodity Price Analysis." *Commodity Yearbook*, 1957. Descripción técnica en: Investopedia. "Donchian Channels." [https://www.investopedia.com/terms/d/donchianchannel.asp](https://www.investopedia.com/terms/d/donchianchannel.asp).

```python
def donchian(precios_high, precios_low, N=20):
    canal_sup = max(precios_high[-N:])
    canal_inf = min(precios_low[-N:])
    medio = (canal_sup + canal_inf) / 2
    ancho = canal_sup - canal_inf

    precio_actual = precios_high[-1]  # o close[-1]
    if precio_actual >= canal_sup:
        return "Ruptura Alcista", ancho
    elif precio_actual <= canal_inf:
        return "Ruptura Bajista", ancho
    else:
        return "Dentro del canal (posible lateralización)", ancho
```

*(suposición del agente)*: Para clasificar lateralización con Donchian, puede usarse un criterio auxiliar: si `ancho < percentil_25(ancho_historico)`, el rango es estrecho y el activo se considera lateralizado.

---

### 4.4. Supertrend

El **Supertrend** calcula un nivel dinámico basado en el precio medio (`HL2 = (high + low) / 2`) ajustado por un múltiplo del ATR. El indicador "voltea" de dirección cuando el precio lo cruza, generando una señal binaria alcista/bajista sin zona de lateralización nativa.

Murenzi, Olivier. "SuperTrend Indicator: Formula and Trading Strategies." *Trading Strategy Guides*, 2021. [https://tradingstrategyguides.com/supertrend-indicator/](https://tradingstrategyguides.com/supertrend-indicator/). Descripción técnica adicional en: Investopedia. "Supertrend Indicator." [https://www.investopedia.com/supertrend-indicator-7976167](https://www.investopedia.com/supertrend-indicator-7976167).

```python
def supertrend(high, low, close, N=10, factor=3):
    atr = average_true_range(high, low, close, N)
    hl2 = [(h + l) / 2 for h, l in zip(high, low)]
    
    banda_sup = [hl + factor * a for hl, a in zip(hl2, atr)]
    banda_inf = [hl - factor * a for hl, a in zip(hl2, atr)]
    
    # Ajustar bandas (lógica de volteo al cruzar precio)
    supertrend = []
    direccion = []
    for i in range(N, len(close)):
        if close[i] > banda_sup[i-1]:
            supertrend.append(banda_inf[i])
            direccion.append("Alcista")
        else:
            supertrend.append(banda_sup[i])
            direccion.append("Bajista")
    
    return direccion[-1], supertrend[-1]
```

*(suposición del agente)*: El Supertrend es particularmente útil en el timeframe de 1h para confirmar el timing de entrada, dado que su señal binaria elimina la ambigüedad de "¿es tendencia o ruido?". Sin embargo, en mercados lateralizados genera señales falsas frecuentes (whipsaws), por lo que debe complementarse con un filtro de volatilidad como el ATR percentil.

---

### 4.5. Regresión Polinomial

En lugar de ajustar una recta ($y = mt + b$), se ajusta un **polinomio de grado 2** ($y = at^2 + bt + c$) o mayor. Esto permite capturar tendencias con curvatura visible, como aceleraciones parabólicas en burbujas o desaceleraciones en finales de tendencia. La **derivada del polinomio en el punto final** (pendiente instantánea) determina la dirección.

Murphy, John J. *Technical Analysis of the Financial Markets*. New York: New York Institute of Finance, 1999, pp. 67–72. [Disponible en Google Books](https://books.google.com/books?id=5lxzDwAAQBAJ). Implementación numérica: NumPy. "numpy.polyfit." [https://numpy.org/doc/stable/reference/generated/numpy.polyfit.html](https://numpy.org/doc/stable/reference/generated/numpy.polyfit.html).

```python
import numpy as np

def regresion_polinomial(precios, grado=2):
    X = np.arange(len(precios))
    coefs = np.polyfit(X, precios, grado)        # Ajuste polinomial
    polinomio = np.poly1d(coefs)
    
    linea_base = polinomio(X)
    derivada = np.polyder(polinomio)              # Derivada analítica
    pendiente_actual = derivada(X[-1])            # Pendiente en el último punto
    
    residuos = np.abs(np.array(precios) - linea_base)
    ancho = np.max(residuos)
    
    if pendiente_actual > umbral_alcista:
        return "Túnel Alcista (curvado)", ancho
    elif pendiente_actual < umbral_bajista:
        return "Túnel Bajista (curvado)", ancho
    else:
        return "Lateralización", ancho
```

*(suposición del agente)*: El grado 2 es generalmente suficiente. Grados mayores (≥3) tienden a sobreajustar el lookback period y producen artefactos en los extremos del intervalo (efecto Runge). Se recomienda limitar el uso a detección de fase terminal de tendencias o movimientos parabólicos evidentes.

---

## 5. Tabla Comparativa de Métodos

| Método | Base estadística | Ancho de banda | Robusto a outliers | Identifica lateralización |
|---|---|---|---|---|
| Regresión Lineal | Mínimos cuadrados | Residual / σ | ⚠️ Moderado | ✅ Sí (pendiente ≈ 0) |
| Bandas de Bollinger | SMA | Desviación estándar | ❌ No | ✅ Sí (squeeze) |
| Canales de Keltner | EMA | ATR | ✅ Sí | ✅ Sí |
| Canales de Donchian | Ninguna | Max / Min histórico | ✅ Sí | ⚠️ Parcial |
| Supertrend | EMA / ATR | ATR × factor | ✅ Sí | ❌ No (binario) |
| Regresión Polinomial | Mínimos cuadrados | Residual / σ | ❌ No | ⚠️ Parcial |

*(suposición del agente)*: Para el contexto de este proyecto (OPEX mensual sobre GGAL, análisis Weekly/Daily/1h), la combinación recomendada es: **Regresión Lineal** (Weekly/Daily para dirección macro) + **Keltner** (filtro de volatilidad robusto) + **Supertrend 1h** (timing de entrada). Bollinger puede añadirse como detector de squeeze antes de vencimientos de opciones.

---

### Referencias
- Bollinger, John. *Bollinger on Bollinger Bands*. New York: McGraw-Hill, 2001. [Google Books](https://books.google.com/books/about/Bollinger_on_Bollinger_Bands.html?id=nCT4B8yOJfAC). *(Para comprender las bandas de volatilidad basadas en desviación estándar y el concepto de squeeze).*
- Donchian, Richard D. "Trend Following Methods in Commodity Price Analysis." *Commodity Yearbook*, 1957. Descripción técnica en Investopedia: [https://www.investopedia.com/terms/d/donchianchannel.asp](https://www.investopedia.com/terms/d/donchianchannel.asp). *(Para la definición de canales basados en máximos y mínimos históricos).*
- Investopedia. "Keltner Channel." [https://www.investopedia.com/terms/k/keltnerchannel.asp](https://www.investopedia.com/terms/k/keltnerchannel.asp). *(Para la descripción técnica de los canales de Keltner y su uso del ATR como medida de volatilidad).*
- Investopedia. "Linear Regression Channel." [https://www.investopedia.com/terms/l/linearregressionchannel.asp](https://www.investopedia.com/terms/l/linearregressionchannel.asp). *(Descripción técnica y teórica del método de regresión en trading).*
- Investopedia. "Supertrend Indicator." [https://www.investopedia.com/supertrend-indicator-7976167](https://www.investopedia.com/supertrend-indicator-7976167). *(Para la implementación y lógica del Supertrend como indicador de dirección binaria).*
- Murphy, John J. *Technical Analysis of the Financial Markets*. New York: New York Institute of Finance, 1999. [Google Books](https://books.google.com/books?id=5lxzDwAAQBAJ). *(Base teórica sobre análisis técnico, tendencias y canales de precio).*
- Natenberg, Sheldon. *Option Volatility and Pricing*. New York: McGraw-Hill, 1994. *(Referencia para la comprensión de ciclos de mercado y volatilidad en distintos marcos temporales).*
- NumPy. "numpy.polyfit." [https://numpy.org/doc/stable/reference/generated/numpy.polyfit.html](https://numpy.org/doc/stable/reference/generated/numpy.polyfit.html). *(Para la implementación numérica del ajuste polinomial por mínimos cuadrados).*
