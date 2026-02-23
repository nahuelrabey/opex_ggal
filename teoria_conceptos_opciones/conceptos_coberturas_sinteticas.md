---
fecha_creacion: "2026-02-23"
fecha_edicion: "2026-02-23"
---
# Análisis de Coberturas: Venta de Calls, Compra de Puts y Futuros

A partir de tu consulta sobre el fragmento *"Vender calls para generar prima mientras se compran puts para proteger contra caídas"*, es muy importante aclarar ciertos conceptos teóricos para evitar confusiones graves en la gestión del riesgo.

## 1. "Vender calls para generar prima" y la obligación asumida
Vender (o "lanzar") una opción CALL significa que le estás otorgando a un tercero el derecho de comprar el activo a un precio determinado (strike) hasta la fecha de vencimiento. A cambio de ceder este derecho, tú (el vendedor) cobras una prima por adelantado.

**Importante:** Quien vende un CALL no está obligado a comprar, sino que **está obligado a VENDER** el activo subyacente si el comprador de la opción decide ejercer su derecho (lo cual ocurrirá si el precio de mercado supera el precio de ejercicio acordado). 
- Si no posees las acciones (lanzamiento en descubierto o *naked call*), tu riesgo en caso de que el activo suba fuertemente es **teóricamente ilimitado**, ya que deberás salir a comprar las acciones más caras en el mercado para poder enviarlas al comprador al precio strike pactado que es menor.

## 2. Compra de PUTS y la aclaración sobre la cobertura
Hay un error conceptual clave en la afirmación *"Comprar PUTS me da un precio fijo de compra"*.
- Comprar un **CALL** te otorga el derecho (a un precio fijo) para **COMPRAR**.
- Comprar un **PUT** te otorga el derecho (a un precio fijo) para **VENDER**.

Si compras un PUT con strike en 200, te aseguras el derecho a vender el activo a 200 dólares/pesos, limitando tu pérdida sin importar cuánto caiga el mercado.

**Análisis de tu escenario planteado (Comprar PUT 200 + Vender CALL 230):**
Preguntas si la compra del PUT 200 es la cobertura frente a la venta del CALL 230, creyendo que la pérdida se limita a 30 (la diferencia entre strikes). **La respuesta matemática es NO.**

Ambas opciones en esta combinación concreta (conocida en finanzas como *Risk Reversal* bajista o *Sintético Corto*) te dejan expuesto a un riesgo de subida:
- **Si el precio cae por debajo de 200:** Empiezas a ganar dinero con el PUT comprado porque tienes derecho a vender caro cuando el mercado está barato. El CALL vendido expira sin valor a tu favor (conservas la prima).
- **Si el precio sube por encima de 230:** El PUT expirará sin valor, lo perdiste. El grave problema es frente al CALL vendido: al estar obligado a vender a 230 algo que está subiendo sin techo en el mercado libre, **tu pérdida ante subidas al alza es ilimitada**. ¡El PUT comprado protege contra movimientos bajistas, no protege frente a la subida que castiga al CALL vendido!

**¿Cómo funciona la verdadera estrategia entonces? (Estrategia "*Collar*")**
El fragmento original asume implícitamente que **ya tienes comprado el activo subyacente** (es decir, tienes una cartera con acciones de GGAL, compradas digamos a 210). 
En este contexto real, la operatoria funciona así:
1. Compras el **PUT 200**: Este es tu verdadero seguro. Limita al máximo tus pérdidas en tus **acciones** si el mercado se desploma. Garantiza que siempre podrás salir a 200.
2. Vendes el **CALL 230**: Como **ya tienes las acciones**, estás cubierto al alza (Covered Call). Si el precio sube a 250, el comprador del call te las quitará a 230 entregándote el activo físico. Pierdes la oportunidad de vender a más, pero no tienes pérdidas abstractas libres. Esta venta se hace porque la prima cobrada por ceder tu derecho de ganancia ilimitada sirve para **financiar y pagar** el PUT seguro que compraste.

Por eso el texto dice: *"vender calls para generar prima mientras se compran puts para proteger contra caídas"* --> **Se busca proteger a las acciones de la caída gratuita con el PUT; mientras el CALL vendido simplemente funciona como modo financiamiento y define un techo.** 

## 3. ¿Cómo podría ser útil la venta de futuros en este caso?
La venta de futuros de acciones (ej. GGAL/AB25) es otra herramienta directa e independiente para cobertura.

- Un **Futuro vendido (Corta en futuro)** es un compromiso legal estandarizado institucionalmente para VENDER el activo a un precio fijado hoy. 
- **Utilidad frente a Opciones y "Gaps Bajistas":** A diferencia del PUT que sufre la pérdida de valor por el paso de los días (*time decay*) y requiere pagos constantes de prima muy atados a la distorsión de la Volatilidad Implícita (IV), un Futuro tiene un movimiento de **Delta -1**.
- Esto significa que por cada peso que caiga la acción en el segmento contado debido a un *gap violento* pre-apertura tras malas noticias (donde los tradicionales *Stop Loss* fallan porque abren esquivando las órdenes límites), el futuro vendido en simultáneo recupera el equivalente casi perfecto (pesos ganados de un lado se restan en la otra), logrando congelar las pérdidas de tu posición a través de lo que se llama una **cobertura simétrica o delta-neutral**.

---

### Fuentes recomendadas
- **Hull, John C.** - *"Options, Futures, and Other Derivatives"*. (Libro académico insignia universal. Aborda las obligaciones contractuales, la estructuración limitante de carteras de tipo Collar, y la aritmética del hedge management con futuros indexados).
- **Investopedia**:
  - [Collar Option Strategy](https://www.investopedia.com/terms/c/collar.asp) (Describe precisamente el setup analizado: Acción + Compra Put + Venta Call).
  - [Naked Call](https://www.investopedia.com/terms/n/nakedcall.asp) (Para comprender el riesgo ilimitado al vendedor cuando omite adquirir protección con un Call de strike superior o con acciones poseídas netamente en su portafolio).
- **Mercados Locales y Tutoriales (BYMA/Matba Rofex)**: Puedes ubicar los manuales oficiales operativos de Rofex referentes a coberturas cruzadas (Hedge), explicando claramente por qué las posiciones en contraposición en futuros actúan atajando gaps overnight donde los inversores no pueden operar activamente.
