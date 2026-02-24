---
fecha_creacion: "2026-02-24"
fecha_edicion: "2026-02-24"
---

# Suposiciones e Hipótesis Testeables sobre GGAL y Opciones

A continuación se presenta un compendio de todas las suposiciones y afirmaciones realizadas a lo largo de los análisis documentados en la bitácora. Cada hipótesis incluye su fuente subyacente y un diseño general (lista de información y cálculos requeridos) para verificar empíricamente su nivel de efectividad utilizando series de tiempo de opciones y de GGAL (o su ADR).

## 1. Lateralización del Precio (Canalización y Soporte)
**Suposición:** El precio de GGAL tiende a oscilar respetando canales técnicos predecibles (túnel bajista o rango lateral) de los que demora tiempo en escapar, frecuentemente deteniéndose de cara a eventos clave externos/internos.
- **Fuentes:** 
  - `analisis_estrategias/evaluacion_estrategia_sin_ventas_libres_ggal.md`
  - `analisis_mercado/argumentos_lateralizacion_ggal_abril.md`
  - `opex/2026_02_24.md`

### Metodología de Verificación (Empírica)
- **Información necesaria:** Precios históricos diarios o intradiarios de GGAL (Apertura, Máximo, Mínimo, Cierre) a lo largo de los años.
- **Cálculos manuales/sistemáticos:**
  - **Identificar canales:** Computar algoritmos para delinear "techos" y "pisos" retrospectivos (ej. bandas como Bollinger o cálculo de regresión lineal sobre los extremos).
  - **Medir el tiempo en rango:** Calcular la cantidad promedio de ruedas operativas que el precio permanece confinado en una amplitud menor estadísticamente.
  - **Evaluar rebotes mecánicos:** Calcular el "win rate" de cada toque a la banda inferior/superior contrastando cuántas velas diarias devuelven al canal (rebote) versus cuántas inician una tendencia nueva cruzando y cerrando por fuera del margen.

---

## 2. Destrucción de Prima en Rangos Laterales (IV Crush y Theta Decay)
**Suposición:** Las lateralizaciones prolongadas provocan una caída dramática en la Volatilidad Implícita (IV) y un desgaste severo por el valor temporal (Theta), abaratando las primas aceleradamente si el precio no se desplaza. *(suposición del agente sobre la aceleración del colapso de prima)*
- **Fuentes:** 
  - `analisis_estrategias/evaluacion_estrategia_acumulacion_strangle.md`
  - `analisis_estrategias/evaluacion_estrategia_sin_ventas_libres_ggal.md`

### Metodología de Verificación (Empírica)
- **Información necesaria:** Precios históricos de cierre de opciones (primas por base), histórico del IV (Volatilidad Implícita), días al vencimiento (DTE), y precio de cierre histórico de GGAL.
- **Cálculos manuales/sistemáticos:**
  - **Aislar ventanas laterales:** Filtrar bloques temporales del activo subyacente donde la volatilidad histórica de la acción (ATR) haya sido ínfima. 
  - **Medir decaimiento de primas:** Extraer el precio de contratos "At The Money" (ATM) durante dichas ventanas y calcular el porcentaje de pérdida neta promediada diaria de los contratos de cara al vencimiento.
  - **Contrastar las griegas:** Estudiar mediante deltas diarias cuánto del abaratamiento responde en porcentaje directo al *Theta* y cuánto a variaciones bruscas de la Volatilidad Implícita de esos días (*Vega*).

---

## 3. Expansión de Volatilidad (El "Sacudón" por Compresión)
**Suposición:** Toda dilatación temporal sostenida y bajísima volatilidad ("olla a presión") es el prolegómeno directo de una expansión rápida e impetuosa en las cotizaciones (salto direccional violento), encareciendo súbitamente los componentes *long vega*.
- **Fuentes:** 
  - `analisis_estrategias/estrategia_doble_diagonal_ggal.md`
  - `analisis_mercado/analisis_alta_volatilidad_ggal.md`

### Metodología de Verificación (Empírica)
- **Información necesaria:** Histórico de volatilidades reales de GGAL en ventanas móviles de precios; Base histórica de Volatilidades Implícitas de las Opciones; calendario de balances.
- **Cálculos manuales/sistemáticos:**
  - **Detectar shocks post-compresión:** Calcular un factor de oscilación sobre 30 días, ubicando los mínimos locales de volatilidad relativa anuales. 
  - **Medir el estallido (Breakout):** Registrar la fuerza de ruptura, midiendo cuán lejos y qué desviación porcentual abarca en un solo impulso (Día 1 a Día 5) la aceleración generada tras vulnerar un rango lateral opresivo.
  - **Impacto directo en la cadena:** Auditar el salto cuantitativo explícito de las opciones "Out of the Money" (O.T.M) de meses distantes calculando si la apreciación tras un quiebre excede holgadamente la prima plana inicial.

---

## 4. Castigo a Operaciones Contra-Tendenciales (Rebotes)
**Suposición:** Acumular un instrumento alcista (como *Calls*) únicamente producto del testeo sobre una franja interior (el piso) cuando la matriz primaria traza sesgos bajistas sistemáticos, acarrea altísima probabilidad de vulneración direccional a la baja (pérdida).
- **Fuentes:** 
  - `analisis_estrategias/evaluacion_estrategia_sin_ventas_libres_ggal.md`

### Metodología de Verificación (Empírica)
- **Información necesaria:** Identificación de macro-tendencias (Medias de 50 o 200 días cruzadas descendentemente) y soportes relativos detectados a partir del gráfico diario histórico.
- **Cálculos manuales/sistemáticos:**
  - **Modelado en tendencia Bearish:** Filtrar de la base temporal solamente las jornadas etiquetadas numéricamente como bajistas (pendientes descendentes continuas). 
  - **Prueba del choque rebotable (Simulación):** Correr en simulación un *Trigger* de "Long (Compra)" cada vez que choca el presunto suelo de soporte intra-tendencia. 
  - **Ratio de destrucción (Drawdown comparado):** Computar qué porcentaje de estas adquisiciones simuladas cruzó en pérdidas irreparables tras 15 ruedas, corroborando que actuar a contra-mano debilita las probabilidades estadísticas frente a seguir en "short" el quiebre de mínimos.

---

## 5. Teoría del Máximo Dolor (Max Pain Theory) pre-Vencimiento
**Suposición:** El subyacente se comportará predispuesto a orientarse magnéticamente hacia aquel punto de anclaje (Strike) el cual, al expirar, neutralice el mayor volumen dinerario de Calls y Puts adquiridos por los tenedores retail del mercado (favoreciendo al colocador/lanzador institucional).
- **Fuentes:** 
  - `analisis_mercado/argumentos_lateralizacion_ggal_abril.md`

### Metodología de Verificación (Empírica)
- **Información necesaria:** Fechas históricas de vencimiento bimestral/trimestral (OPEX), archivo histórico del "Open Interest" (Contratos Abiertos) dividido cruzadamente entre Calls y Puts por cada Strike transado en la plataforma y el precio corriente Spot correspondiente de GGAL.
- **Cálculos manuales/sistemáticos:**
  - **Ecuación iterada del Strike Magnético:** Desplegar una sumatoria por cada nivel de ejercicio (*Strike*), computando el pago monetario forzoso del global de contratos listados si la acción terminara clavada aritméticamente en esa base exacta. El *Strike* que reduzca el balance y pague la cifra sistémicamente más baja, es el nivel final de *Max Pain*.
  - **Verificación de tracción:** Obtener la diferencia absoluta (distancia/gap porcentual) entre el valor objetivo emanado como *Max Pain* frente a la cotización final del subyacente a los 10 días previos, 5 días previos, y día final del cierre del OPEX con el objeto de ver la progresiva convergencia matemática al centro de gravedad.

---

## 6. Curva "Skew" de la Volatilidad Temporal o Sobreprecio Inminente
**Suposición:** En instancias de extrema lateralidad o shock, las opciones vinculadas al ejercicio cortoplacista se sobrevenden o sobrecompran producto de manías de urgencia (IV desbocada), habilitando la compra financiada de coberturas lejanas a valor temporal reprimido comparativamente hablando.
- **Fuentes:** 
  - `analisis_estrategias/estrategia_doble_diagonal_ggal.md`
  - `opex/2026_02_23.md`

### Metodología de Verificación (Empírica)
- **Información necesaria:** Matriz histórica que superponga primas o volatilidades implícitas en un idéntico día, desdoblado para los contratos venciendo ese mes y contratos perennizando para el vencimiento de 60, 90 y 120 días.
- **Cálculos manuales/sistemáticos:**
  - **Estructura Temporal (Term Structure):** Desarrollando empíricamente una curva matemática cruzando "Volatilidad ATM" (eje Y) frente a "Días Restantes - DTE" (eje X) a lo largo del calendario para discernir la asimetría temporal del precio.
  - **Señal de Inversión (Backwardation):** Identificar la cantidad total de períodos/días donde las volatilidades del "mes en curso" explotan en valores de >+10% a >+15% por arriba del promedio estandarizado de los seguros lejanos al vencimiento.

---

### Fuentes recomendadas
- **Natenberg, Sheldon** - *"Option Volatility & Pricing"*. (Mecánicas de evaluación empírica de probabilidades, cálculo de IV y estimación de volatilidad futura).
- **Hull, John C.** - *"Options, Futures, and Other Derivatives"*. (Base matemática estandarizada para analizar griegas y estructurar backtesting de valoración de derivados).
- **Investopedia:** Para los conceptos de [Max Pain Theory](https://www.investopedia.com/terms/m/maxpain.asp), [Volatility Skew](https://www.investopedia.com/terms/v/volatilityskew.asp), y [Theta Decay](https://www.investopedia.com/terms/t/thetadecay.asp), aportando definiciones base.
