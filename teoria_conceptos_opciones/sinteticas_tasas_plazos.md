---
fecha_creacion: "2026-02-23"
fecha_edicion: "2026-02-23"
---
# Profundización: Sintéticas, Tasas de Interés y Plazos (Put-Call Parity)

A partir de tu consulta sobre el fragmento: *"usando sintéticas (combinación de call/put para replicar posiciones) para descontar desajustes de plazos y tasas"*, vamos a desglosar cómo interactúan las opciones con el valor del dinero en el tiempo y por qué los grandes operadores usan "sintéticas" para arbitrar estas ineficiencias.

## 1. ¿Qué es una Posición Sintética?

Las opciones Call y Put de un mismo activo (ej. GGAL), mismo *strike* (precio de ejercicio) y misma fecha de vencimiento, están matemáticamente atadas al precio de la acción subyacente. Esta relación permite "fabricar" (sintetizar) el comportamiento de un activo usando derivados.

- **Acción Sintética Comprada (Synthetic Long):** Comprar un CALL + Vender un PUT (mismo strike y vencimiento).
  - *Resultado:* Si la acción sube, ganas con el Call. Si baja, pierdes con el Put vendido. El gráfico de ganancias/pérdidas es idéntico a tener comprada la acción real.
- **Acción Sintética Vendida (Synthetic Short):** Comprar un PUT + Vender un CALL (mismo strike y vencimiento).
  - *Resultado:* Ganas si la acción cae (por el Put) y pierdes si sube (por el Call vendido). Es idéntico a estar vendido en corto (*short selling*) en la acción real.

**¿Por qué crear una acción con opciones en lugar de comprar la acción real?**
Por el apalancamiento y el capital retenido. Armar una sintética requiere mucho menos capital inicial líquido que comprar 100 acciones físicas. El capital que no usaste lo puedes colocar a devengar una **tasa de interés** (ej. en cauciones o fondos).

## 2. El "Desajuste de Tasas" y la Paridad Put-Call

La base matemática que rige esto se llama **Paridad Put-Call** (*Put-Call Parity*). La fórmula teórica es:

> **Call + Valor Presente del Strike = Put + Precio de la Acción**

El concepto de **Valor Presente** entra en juego porque el *strike* se pagará en el futuro (al vencimiento). Para saber cuánto vale hoy, hay que descontarle la **tasa de interés libre de riesgo** (ej. tasa de caución) proporcional a los **plazos** (días que faltan para el vencimiento).

### Arbitraje de Tasas Implícitas
En mercados volátiles o con restricciones macroeconómicas (como el argentino histórico de tasas o cepos), los precios de los Calls y Puts en el mercado real se "desalinean" de la fórmula teórica.

- Cuando compras un Call y vendes un Put (Sintética Larga) y simultáneamente vendes la Acción real (Short) o vendes un Futuro, tu riesgo direccional es **CERO**. *(Para una explicación detallada de por qué matemáticamente el riesgo se anula, ver [Riesgo Direccional Cero y Arbitraje](riesgo_direccional_cero.md))*
- Lo único que queda en esa ecuación es la diferencia entre la **Tasa Implícita** de las opciones y la **Tasa de Interés real del mercado**. *(Para aprender a calcular este dato matemático vital que arbitran los algoritmos, ver [Cálculo de la Tasa Implícita](tasa_implicita_opciones.md))*
- **Descontar desajustes de tasas:** Los operadores detectan si las opciones están "asumiendo" una tasa muy alta o muy baja en comparación con cauciones o bonos. Si el mercado de opciones asume una tasa del 40% anual, pero en el mercado monetario puedes conseguir fondos al 30%, usarás posiciones sintéticas combinadas para embolsarte ese desajuste (arbitraje de tasas o *reverse conversion*). 

## 3. El "Desajuste de Plazos" (Term Structure)

Los mercados de opciones tienen distintos vencimientos (ej. febrero 2026, marzo 2026, abril 2026). La expectativa de tasas y de volatilidad no es igual para todos los meses. 

- Un operador puede ver liquidez inusual o "flujos inusuales en puts de marzo", lo que altera el precio relativo de la base de marzo frente a, por ejemplo, febrero.
- Usando **Sintéticas de calendario** (o *Calendar Spreads* / armar sintéticas en diferentes meses), un operador puede vender la sintética del mes donde la tasa/volatilidad está "cara" y comprar la del mes donde está "barata". 
- Se aísla el activo subyacente (GGAL no importa si sube o baja) y el operador literalmente está operando la "Curva de Tasas" o "Curva de Volatilidad" temporal entre meses.

### Conclusión sobre el fragmento:
El texto se refería a inversores sofisticados (o algoritmos institucionales) que detectan que los Puts de cierto strike están sobrevalorados o desalineados respecto a la tasa de interés debido a pánico o coberturas grandes en un plazo específico (ej. marzo). 
Al armar "sintéticas", aíslan el movimiento direccional de GGAL para dedicarse a capturar y "descontar" (arbitrar a riesgo cero o bajo riesgo) esa diferencia de tasas de interés o esa expectativa temporal deformada entre dos fechas de vencimiento.

---

### Fuentes recomendadas
- **Hull, John C.** - *"Options, Futures, and Other Derivatives"*. (Capítulos sobre Paridad Put-Call y estrategias de arbitraje: Conversiones y Reversiones).
- **Investopedia:** 
  - [Put-Call Parity](https://www.investopedia.com/terms/p/putcallparity.asp) (Fundamento matemático de por qué las tasas de interés dictan la relación y fijación de precios entre puts y calls del mismo strike).
  - [Synthetic Position](https://www.investopedia.com/terms/s/synthetic.asp) (Cómo los traders replican activos alterando su flujo de caja y financiamiento).
