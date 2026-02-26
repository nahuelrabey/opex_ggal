---
fecha_creacion: "2026-02-26"
fecha_edicion: "2026-02-26"
---

# Análisis: Cuna Comprada (Long Strangle) con Volatilidad Implícita Baja

Este documento profundiza sobre la afirmación de índole operativa: *"Con VI baja (volatilidad implícita), la cuna comprada es rentable"*, formulada en los comentarios de mercado.

## 1. Mecánica de la Cuna Comprada (Long Strangle)

Una **cuna comprada** o *long strangle* es una estrategia de opciones no direccional que consiste en comprar simultáneamente una opción de compra (Call) *Out-of-the-Money* (OTM) y una opción de venta (Put) OTM, ambas con la misma fecha de vencimiento.

- **Riesgo:** Limitado al costo total de las primas pagadas.
- **Beneficio:** Teóricamente ilimitado ante movimientos violentos en cualquier dirección.
- **El perfil de Griegas:**
  - **Delta:** Neutral inicial (al estructurarse simétricamente).
  - **Gamma:** Positiva (el Delta aumenta a medida que el precio se mueve a favor).
  - **Vega:** Positiva (la posición se beneficia de un aumento en la volatilidad implícita).
  - **Theta:** Negativa (la posición pierde valor por el desgaste del paso del tiempo).

Hull, John C. *Options, Futures, and Other Derivatives*. 10ma ed. Pearson, 2017. [Disponible en Amazon](https://www.amazon.com/Options-Futures-Other-Derivatives-10th/dp/013447208X). *(Para el perfil estructural y de pago del Long Strangle).*

## 2. El Impacto de una Volatilidad Implícita (VI) Baja

La afirmación sugiere que un entorno de VI baja hace que la estrategia sea rentable o altamente favorable. Esto se debe a dos grandes ventajas teóricas:

### 2.1. Opciones Baratas y Breakevens Estrechos
La volatilidad implícita es el determinante principal del valor extrínseco. Cuando la VI es baja, las opciones Call y Put OTM están comparativamente baratas.
Al gastar poco capital, el riesgo máximo es menor y los puntos de equilibrio (*breakeven points*) se ubican más cerca del precio actual del subyacente. El activo necesita realizar un desplazamiento menor para que la estrategia adquiera valor intrínseco al vencimiento.

### 2.2. Vega Positiva y Reversión a la Media
La volatilidad financiera exhibe un comportamiento estadístico recurrente: **tiende a revertir a la media**.
Si la VI se encuentra en mínimos históricos (ej. *IV Rank* por debajo del 20%), existe una alta probabilidad estadística de que sufra una expansión. Dado que la cuna comprada tiene **Vega positiva**, si la VI general del mercado sube, el precio de ambas opciones se inflará automáticamente. En este escenario, el operador puede desarmar la estructura con ganancias *incluso si el precio del activo subyacente apenas se movió*.

Natenberg, Sheldon. *Option Volatility and Pricing*. New York: McGraw-Hill, 1994. [Disponible en Amazon](https://www.amazon.com/Option-Volatility-Pricing-Strategies-Techniques/dp/0071818774). *(Para las características de reversión a la media de la volatilidad y la expansión de la VI en opciones con Vega positiva).*

## 3. ¿Es Siempre Rentable? (La Trampa del Theta)

Pese a lo favorable de configurar el trade, la afirmación *"es rentable"* como decreto absoluto es **falsa e incompleta**. La compra sistemática de *strangles* ciegos suele ser destructiva para las cuentas por los siguientes argumentos:

1. **La VI baja puede ser el reflejo de la calma genuina:** Que la VI esté baja no significa que vaya a subir a corto plazo. El mercado de opciones puede estar cotizando de manera correcta un periodo prolongado de lateralización, sin eventos (*catalizadores*) en el horizonte.
2. **El constante desgaste del tiempo (Theta Decay):** Si el subyacente se queda inmóvil y la VI tampoco sufre el rebote especulado, el paso del tiempo (*Theta*) consumirá implacablemente el valor extrínseco de ambas patas. Este desgaste acelera su trituración especialmente en el último mes y medio previo al vencimiento (en curvas de Theta no lineales).
3. **La Condición Estricta de Rentabilidad:** Una cuna comprada sólo resulta rentable si la **volatilidad realizada** subsiguiente del activo es superior a la **volatilidad implícita** que se pagó al armar la estructura; alternativamente, si una expansión súbita de volatilidad permite salir de la posición antes de que el Theta destruya el capital.

*(suposición del agente)*: Ejecutar cunas sin filtro es ineficiente. Las mejores cunas compradas requieren complementos confirmatorios; por ejemplo, ejecutarlas únicamente cuando una VI baja (medida por IV Rank) coincide con un patrón clásico de compresión técnica como el *Bollinger Squeeze* (ver `bollinger_squeeze_ruptura_volatilidad.md`), anticipando así el catalizador exacto de la inminente expansión de volatilidad.

## 4. Conclusión

La reformulación rigurosa del comentario del foro es:
**"Con VI históricamente baja, la cuna comprada presenta una relación riesgo-beneficio asimétrica muy atractiva y perfiles de exposición óptimos frente a *shocks* sorpresivos, pero la estrategia resultará perdedora a menos que la volatilidad realmente efectuada supere el precio pagado o se suscite un repunte abrupto del pánico antes del vencimiento."**

---

### Referencias

- Hull, John C. *Options, Futures, and Other Derivatives*. 10ma ed. Pearson, 2017. [Amazon](https://www.amazon.com/Options-Futures-Other-Derivatives-10th/dp/013447208X). *(Principal fundamento sobre estrategias de volatilidad bidireccional, perfiles P&L y la erosión temporal).*
- Natenberg, Sheldon. *Option Volatility and Pricing*. New York: McGraw-Hill, 1994. [Amazon](https://www.amazon.com/Option-Volatility-Pricing-Strategies-Techniques/dp/0071818774). *(Documentación canónica sobre cómo el trader valora y explota los desvíos probabilísticos de la VI, la asimetría de Vega y el ciclo de la volatilidad).*
