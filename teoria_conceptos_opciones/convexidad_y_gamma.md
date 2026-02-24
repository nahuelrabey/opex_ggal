---
fecha_creacion: "2026-02-24"
fecha_edicion: "2026-02-24"
---

# Convexidad, Gamma y la Aceleración del Precio en Opciones

En el mundo de los derivados financieros, la **convexidad** define el beneficio estructural y asimétrico que obtienen los compradores de opciones frente a los tenedores del activo subyacente. Mientras el beneficio del subyacente puro es lineal, el rendimiento de una opción comprada es curvo o "convexo".

## 1. El Beneficio Lineal (Delta Estático)

La tenencia de acciones tradicionales exhibe un comportamiento lineal. Si posees 100 acciones de Grupo Financiero Galicia (GGAL) a $5.000:
*   Si el precio sube $100, la posición gana $10.000.
*   Si el precio baja $100, la posición pierde $10.000.

La tasa de cambio (la velocidad a la que ganas o pierdes) permanece constante e inalterable. Diremos entonces que la posición en acciones tiene un **Delta de 1.00**, y este Delta jamás se modifica sin importar cuánto varíe el precio de la acción.

## 2. El Beneficio Convexo (La ventaja estructural)

Cuando se adquiere un contrato de opción (Call o Put de frente, es decir, *Long*), la estructura de pago/riesgo deja de ser una línea recta y adopta la forma de una curva ascendente (como una sonrisa). Esta curvatura se materializa a través de la letra griega **Gamma**.

**Gamma ($\Gamma$)** mide la **tasa de cambio del Delta** por cada movimiento de un punto en el precio del activo subyacente. Dicho de otro modo, si el Delta es la "velocidad" a la que cambia la prima de tu opción, Gamma es la "aceleración" de esa velocidad.

Poseer **Gamma a favor** (Convexidad Positiva) otorga el siguiente efecto dual y asimétrico:
*   **Tracción a favor:** Si la acción se mueve direccionalmente como esperabas, Gamma provoca que tu Delta aumente. Con cada peso adicional que la acción sube, tu opción gana valor monetario **cada vez más rápido**.
*   **Frenado en contra:** Si la acción se mueve en sentido contrario al deseado, Gamma provoca que tu Delta disminuya. Con cada peso adicional que la acción cae, tu opción pierde valor monetario **cada vez más lento** (el ritmo de sangrado se frena conforme el Delta se acerca a cero).

### El Costo de la Convexidad: El Peaje de Theta
El mercado de opciones obedece a leyes de arbitraje estrictas y no regala el beneficio superior de la convexidad matemática. El "sobrecosto" o "peaje" que se abona constantemente por retener una posición convexa (Gamma positivo) se denomina **Theta ($\Theta$)** o *Time Decay* (Decadencia temporal).

Comprar opciones de compra o venta implica estar "alquilando" Convexidad a cambio de pagar una porción diaria de valor extrínseco.

## 3. ¿Cómo se calcula Gamma?

Matemáticamente, dentro del tradicional **Modelo de Black-Scholes-Merton**, Gamma es la *segunda derivada* parcial del precio de la opción (la prima) con respecto al precio del activo subyacente (Spot). Es decir, es la derivada pura de la fórmula de Delta.

La fórmula analítica de Black-Scholes para la obtención del Gamma de una opción (tanto para Calls como para Puts) europea sin pago de dividendos es:

$$ \Gamma = \frac{N'(d_1)}{S \cdot \sigma \sqrt{T}} $$

Donde:
*   **$S$**: Precio *Spot* o precio actual del activo subyacente.
*   **$\sigma$**: Volatilidad Implícita del subyacente (expresada anualmente, ej: 0.40 para 40%).
*   **$T$**: Tiempo restante hasta el vencimiento (expresado en años, ej: 30 días = 30/365).
*   **$N'(d_1)$**: Función de densidad de probabilidad de la distribución normal estándar evaluada en $d_1$.
*   **$d_1$**: Viene dado por la fórmula fundamental de Black-Scholes:
    $$ d_1 = \frac{\ln(S/K) + (r + \frac{\sigma^2}{2})T}{\sigma \sqrt{T}} $$
    *Donde $K$ es el Strike y $r$ es la tasa libre de riesgo.*

### Inferencias del Cálculo
A partir de la fórmula podemos realizar las siguientes deducciones estructurales (suposiciones del agente confirmadas por la teoría financiera general):
1.  **Gamma siempre es positivo:** Como la función de densidad $N'(x)$ es intrínsecamente positiva, y tanto el precio Spot, como la Volatilidad y el Tiempo restante son mayores o iguales a cero, la resolución de la ecuación siempre entrega un número positivo. Los compradores siempre retienen Gamma positivo.
2.  **Gamma decae con la lejanía temporal:** El término $\sqrt{T}$ en el divisor indica que, a mayor tiempo restante, el Gamma se achata. Las opciones a largo plazo (LEAPs) son perezosas y su Delta varía muy lentamente.
3.  **El riesgo direccional extremo (Explosión del Gamma):** A medida que la fecha de vencimiento se acerca al final ($T \rightarrow 0$), su denominador tiende a cero para las opciones At-The-Money (ATM), causando que la ecuación de Gamma converja hacia el infinito. Por esto, los contratos que vencen en 24hs o 48hs exhiben variaciones de prima extremadamente violentas.

---

### Fuentes recomendadas
*   *Hull, John C. "Options, Futures, and Other Derivatives"*, Capítulo "Las Letras Griegas" (Bibliografía indispensable para conocer a cabalidad el desarrollo de la ecuación analítica del Gamma bajo el modelo de Black-Scholes y sus derivados parciales).
*   *Natenberg, Sheldon. "Option Volatility and Pricing: Advanced Trading Strategies and Techniques"* (Material didáctico supremo para comprender el intercambio práctico que afronta el operador "Retail" de opciones a la hora de pagar *Theta* para lograr acumular posiciones ricas en retornos convexos o *Gamma*).
