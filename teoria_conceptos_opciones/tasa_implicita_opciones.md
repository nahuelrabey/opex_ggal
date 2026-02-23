---
fecha_creacion: "2026-02-23"
fecha_edicion: "2026-02-23"
---
# Profundización: Cálculo de la Tasa Implícita en Opciones

Este documento explica cómo deducir numéricamente la **tasa de interés implícita** que el mercado secundario está asignando al valor temporal del dinero a través de los precios de las opciones (Calls y Puts).

## 1. El Fundamento Matemático: La Paridad Put-Call

Para calcular la tasa que reflejan las opciones, partimos de la fórmula de la **Paridad Put-Call europea** (aplicable razonablemente bien en la práctica diaria para opciones americanas si no hay dividendos jugosos de por medio). La ecuación fundamental que equilibra el mercado es:

> **C + [ X / (1+r)^t ] = P + S**

Donde:
- **C:** Precio (Prima) del Call.
- **P:** Precio (Prima) del Put (con idéntico Strike e idéntico Vencimiento que el Call).
- **S:** Precio Spot (Actual) de la acción subyacente en el mercado.
- **X:** Strike (Precio de Ejercicio) común de ambas opciones.
- **r:** Tasa de interés libre de riesgo (anualizada) que queremos averiguar.
- **t:** Tiempo restante hasta el vencimiento (expresado en años; ej. 30 días = 30 / 365 = 0.082).

## 2. Despejando la Tasa Implícita (r)

Lo que el mercado hace es arbitrar esta fórmula. Si tú conoces del mercado en vivo los valores de **C, P, S, X y t**, tu única incógnita es la tasa **r**. Esa es nuestra **Tasa Implícita**.

Reacomodando algebraicamente la fórmula básica para entender cuánto vale en el presente ese Strike (X):
> **Valor Presente (X) = P + S - C**

Sustituyendo el Valor Presente por la fórmula de descuento `[ X / (1+r)^t ]`:
> **X / (1+r)^t = P + S - C**

Pasando términos para despejar *(1+r)*:
> **(1+r)^t = X / ( P + S - C )**

Y finalmente, despejando la tasa **r**:
> **r = [ X / (P + S - C) ]^(1/t) - 1**

*Nota: Esta fórmula es de interés compuesto anual. Para tasas nominales simples (TNA) muy usadas localmente, el despeje directo suele usarse como `r = (X - (P + S - C)) / ((P + S - C) * (días/365))`.*

## 3. Ejemplo Práctico Numérico

Supongamos que faltan 30 días para el vencimiento (*t* = 30/365 = 0.0822 años) y observamos esto en la pizarra de cotizaciones de GGAL:
- Acción (S): USD 50
- Strike elegido (X): 50
- Prima Call (C): USD 3.50
- Prima Put (P): USD 2.60

**Paso 1: ¿Cuánto vale hoy realmente esa base (X) según las opciones?**
> Valor Presente = P + S - C
> Valor Presente = 2.60 + 50 - 3.50 = **49.10**

*(El mercado valora hoy a USD 49.10 el derecho/obligación que vencerá valiendo 50)*.

**Paso 2: Calcular el interés implícito generado en 30 días**
Diferencia = 50 - 49.10 = **0.90**.
El dinero "creció" 0.90 respecto a los 49.10 originales.
Porcentaje directo = 0.90 / 49.10 = **0.0183 (u 1.83%) en 30 días.**

**Paso 3: Anualizar la tasa (TNA simple para simplificar)**
> Tasa Anualizada = 1.83% * (365 / 30) = **22.26%**

**Conclusión:** La *Tasa Implícita* de estas opciones es del **22.26% anual**. 

## 4. ¿Para qué se usa este cálculo? (Arbitraje)
El operador compara ese **22.26%** contra la tasa real que puede conseguir en el banco o caucionando su dinero.
- Si la caución rinde un **35%**, el operador dice: *"Las opciones rinden muy poco (22.26%) comparadas con la caución. Vendo todo lo que rinda la caución (o me financio barato con opciones) y hago arbitraje"*.
- Para lograr eso, venderá un sintético y colocará el dinero generado en cauciones al 35%, ganando la diferencia casi sin riesgo.

Calcular esta tasa constantemente para todas las bases es lo que "escanea" y aprovechan los algoritmos cuantitativos (High-Frequency Trading) en microsegundos.

---

### Fuentes recomendadas
- **Hull, John C.** - *"Options, Futures, and Other Derivatives"*. (Revisa el capítulo de "Properties of Stock Options" donde desarrolla a pleno las desviaciones de la Paridad Put-Call y la deducción de dividendos y tasas).
- **Investopedia:** 
  - [Implied Interest Rate](https://www.investopedia.com/terms/i/impliedinterestrate.asp) (Cómo los mercados de divisas y derivados esconden las tasas de interés en sus diferencias de cotización entre spot y plazos futuros).
