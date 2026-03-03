---
fecha_creacion: "2026-02-26"
fecha_edicion: "2026-02-26"
---

# Hipótesis Verificables sobre GGAL

> Este documento cataloga todas las afirmaciones presentes en los directorios `opex/`, `analisis_mercado/` y `analisis_estrategias/` que pueden contrastarse con datos históricos de precios de GGAL, su tira de opciones y fuentes externas complementarias. Para cada hipótesis se describe el test métrico concreto a ejecutar.

---

## 1. Hipótesis sobre el Comportamiento del Subyacente (GGAL Precio)

### H-01 — Lateralización con sesgo bajista (feb-abril 2026)
**Fuente:** `opex/2026_02_24.md`, `analisis_mercado/argumentos_lateralizacion_ggal_abril.md`

> *"GGAL lateraliza entre ~$6.900 y ~$7.500 (en pesos) durante feb-abril 2026, con leve pendiente negativa."*

**Datos necesarios:** Serie de precios GGAL Daily (OHLCV) — disponible en BD propia.

**Test:**
- Ajustar regresión lineal (OLS) sobre precios de cierre en el período 01/02/2026–30/04/2026.
- Verificar: pendiente `m ≈ 0` con intervalo de confianza al 95% que incluya cero, y que el 80%+ de los cierres caiga dentro de ±1σ del ajuste.
- Calcular ratio `max-min / precio_medio` del período: si < 20%, confirma lateralización formal.

---

### H-02 — La excursión intradía de GGAL no se refleja en las primas de opciones
**Fuente:** `opex/2026_02_25.md` (observación de ChebyCheff)

> *"Una variación de $250 en el subyacente (de 6.880 a 7.130) no se vio reflejada ni potenciada en las primas Call/Put de ninguna base."*

**Datos necesarios:** Tira de opciones intradía GGAL (precios bid/ask por hora) + precios GGAL intradía 25/02/2026.

**Test:**
- Calcular el Delta teórico BSM para cada contrato al inicio de la sesión.
- Calcular la variación esperada de prima: `ΔP_esperado = Delta_BSM × ΔS`.
- Calcular la variación observada real: `ΔP_observado = prima_cierre − prima_apertura`.
- Comparar `ΔP_observado` vs `ΔP_esperado` para cada contrato. Si `ΔP_observado < ΔP_esperado` de manera sistemática (>70% contratos), las griegas BSM sobreestiman la sensibilidad real del mercado local.

---

### H-03 — El precio de GGAL tiende a gravitar hacia el Max Pain en la semana de vencimiento
**Fuente:** `analisis_mercado/argumentos_lateralizacion_ggal_abril.md`

> *"El precio del subyacente tiende a converger al Strike donde expira el mayor número de opciones sin valor (Max Pain) en los vencimientos bimestrales."*

**Datos necesarios:** Tira de opciones histórica con Open Interest (OI) por Strike para cada vencimiento + precio GGAL en los últimos 3-5 días previos a cada OPEX.

**Test:**
- Para cada vencimiento histórico disponible:
  1. Calcular Max Pain = Strike que minimiza `Σ(PUT OI × max(K−S,0) + CALL OI × max(S−K,0))` al cierre de cada sesión.
  2. Registrar el precio de cierre de GGAL en cada uno de los 5 días previos al vencimiento.
  3. Calcular la distancia porcentual `(precio − MaxPain) / precio`.
- Hipótesis confirmada si la distancia media se acorta progresivamente en los 5 días previos al vencimiento (tendencia convergente).

---

### H-04 — El Delta Hedging de los Market Makers estabiliza el rango lateral
**Fuente:** `analisis_mercado/argumentos_lateralizacion_ggal_abril.md`

> *"El proceso de Delta Hedging de los Market Makers contribuye sistemáticamente a estabilizar el precio en rangos definidos."*

**Datos necesarios:** Tira de opciones con OI y precios (para estimar Gamma neto del mercado) + precios GGAL intradía.

**Test:**
- Calcular el **Gamma Exposure neto del mercado** (GEX): `GEX = Σ(Gamma_i × OI_i × 100)` para toda la tira, diferenciando Calls y Puts.
- Clasificar cada sesión en "GEX positivo" (MM compran delta cuando baja, venden cuando sube → estabilizador) o "GEX negativo" (MM amplifican movimientos).
- Verificar si los días con GEX positivo presentan menor rango intradía `(High−Low)/Close` que los días con GEX negativo.

---

## 2. Hipótesis sobre el Comportamiento de la Volatilidad Implícita (VI)

### H-05 — La VI de GGAL se encuentra en mínimos históricos en la actualidad
**Fuente:** `opex/2026_02_26.md` (mensaje de Telegram), `analisis_estrategias/evaluacion_estrategia_acumulacion_strangle.md`

> *"Las lateralizaciones prolongadas comprimen la VI (IV Crush). En este período, VI está baja."*

**Datos necesarios:** Serie histórica de VI implícita de opciones ATM de GGAL (calculable desde precios de opciones con BSM invertido).

**Test:**
- Calcular IV implícita ATM (promedio Put y Call más cercanos al precio) para cada día disponible.
- Calcular el **IV Rank**: `IVR = (IV_actual − IV_min_52w) / (IV_max_52w − IV_min_52w) × 100`.
- Hipótesis confirmada si IVR < 30 en el período feb-2026.
- **Dato adicional necesario:** Precio de opciones ATM en tiempo real o histórico con granularidad diaria.

---

### H-06 — Bollinger Squeeze precede rupturas de volatilidad en GGAL
**Fuente:** `teoria_conceptos_opciones/identificacion_tuneles_tendencia.md` → `bollinger_squeeze_ruptura_volatilidad.md`

> *"Cuando las Bandas de Bollinger quedan completamente dentro de los Canales de Keltner, se anticipa una ruptura de volatilidad inminente."*

**Datos necesarios:** Precios OHLCV diarios de GGAL — disponible en BD.

**Test:**
- Calcular señal de Squeeze histórica: `squeeze[t] = (BB_sup < KC_sup) AND (BB_inf > KC_inf)` con parámetros `N=20, k=2, m=1.5`.
- Para cada `squeeze[t] = True`, registrar el mayor movimiento porcentual de precio en los siguientes 5/10/20 días.
- Comparar con la distribución de movimientos en días sin squeeze.
- Hipótesis confirmada si el movimiento post-squeeze es estadísticamente mayor (test t de Student o Mann-Whitney).

---

### H-07 — La VI realizada de GGAL supera habitualmente a la VI implícita pagada en opciones ATM
**Fuente:** `analisis_estrategias/evaluacion_estrategia_sin_ventas_libres_ggal.md`, `analisis_mercado/analisis_alta_volatilidad_ggal.md`

> *"GGAL es una acción altamente volátil. La estrategia de comprar opciones puede rendir positivo porque la volatilidad realizada supera la implícita."*

**Datos necesarios:** Serie histórica de precios GGAL (para calcular Volatilidad Realizada) + precios de opciones ATM históricas (para IV implícita).

**Test:**
- Calcular **Volatilidad Realizada (VR)** para cada período de 30 días: `VR = std(log_returns) × sqrt(252)`.
- Calcular **IV implícita ATM** del inicio de cada período (precio de la opción ATM más cercana al vencimiento de 30 días).
- Calcular **Variance Risk Premium (VRP)**: `VRP = IV − VR`.
- Hipótesis de Long Strangle rentable se confirma si `VRP < 0` frecuentemente (VR > IV), es decir, el mercado subestima el movimiento real de GGAL.

---

## 3. Hipótesis sobre Estrategias de Opciones

### H-08 — El "Legging-in" reduce el costo base del Strangle vs. entrada simultánea
**Fuente:** `analisis_estrategias/evaluacion_estrategia_acumulacion_strangle.md`

> *"Comprar el Call cuando la acción toca el piso y el Put cuando toca el techo resulta matemáticamente más barato que comprar ambos simultáneamente."*

**Datos necesarios:** Tira de opciones histórica GGAL + precios intradía para identificar pisos y techos del rango.

**Test:**
- Identificar ciclos de rebote del rango lateral histórico (precio toca soporte, luego resistencia).
- Simular dos estrategias:
  - `A_simultaneo`: comprar Call + Put ATM el día del soporte.
  - `A_legging`: comprar Call en el soporte, Put en la resistencia.
- Comparar el costo total (suma de primas pagadas) de A_simultaneo vs A_legging para los mismos vencimientos.
- Hipótesis confirmada si A_legging tiene costo promedio significativamente menor.

---

### H-09 — El Diagonal Debit (strikes comprado más ATM que el vendido) protege ante rupturas anticipadas
**Fuente:** `analisis_estrategias/evaluacion_setup_strikes_ggal.md`

> *"Si el precio rompe al alza hasta USD 62, el Call Julio 55 (comprado) genera más valor intrínseco que las pérdidas del Call Abril 60 (vendido)."*

**Datos necesarios:** Precios de opciones GGAL con spreads de strikes similares en cualquier período histórico.

**Test:**
- Simular el setup: Long Call K=55 Julio / Short Call K=60 Abril al precio de apertura.
- Calcular el P&L neto del spread ante distintos precios finales del subyacente al vencimiento de Abril: `S ∈ {50, 55, 58, 60, 62, 65, 70}`.
- Verificar que para `S ≥ 60`, el gain de la pata larga (Julio 55) supera la pérdida de la pata corta (Abril 60) neteadas por las primas pagadas/cobradas.

---

### H-10 — La cuna comprada (Long Strangle) es rentable si la VI es baja al armarla
**Fuente:** `opex/2026_02_26.md`, `teoria_conceptos_opciones/cuna_comprada_vi_baja.md`

> *"Con IV baja, la cuna comprada es rentable porque el costo de la prima es bajo y la expansión posterior de VI infla el valor sin necesidad de que el subyacente se mueva."*

**Datos necesarios:** Serie histórica de IV + precios de opciones OTM GGAL + precios del subyacente.

**Test (backtesting):**
- Filtrar todos los días donde `IVR < 25` (IV históricamente baja).
- En cada uno de esos días, simular la apertura de un Long Strangle (Call OTM + Put OTM a δ~0.25).
- Registrar P&L a los 15, 30 y 45 días de haberlo abierto.
- Calcular tasa de ganancia (% de trades positivos) y P&L medio.
- Hipótesis confirmada si tasa de ganancia > 50% y P&L medio > 0 al menos en alguno de los horizontes.

---

## 4. Hipótesis sobre Factores Macroeconómicos Verificables con Datos Externos

### H-11 — El ratio NPL de GGAL alcanzó pico cercano al 7% en marzo 2026
**Fuente:** `analisis_mercado/calidad_cartera_ggal.md`

> *"La gerencia de GGAL proyecta que el ratio de NPL alcance su máximo de entre 6% y 7% en marzo de 2026."*

**Datos necesarios:** Reportes trimestrales de GFG (Investor Relations) — externos, descargables de [gfgsa.com](https://www.gfgsa.com/English/Financial-Information/Financial-Statements/default.aspx).

**Test:** Verificar el ratio NPL reportado en el informe 1Q 2026 (a publicarse ~mayo 2026) contra la proyección. Cruzar con evolución del precio de GGAL en la semana post-publicación (¿el mercado castigó o premió la confirmación del pico?).

---

### H-12 — El carry trade comprime el NIM bancario y deteriora la rentabilidad de GGAL
**Fuente:** `analisis_mercado/impacto_carry_trade_balances_bancarios.md`

> *"El carry trade encarece el fondeo de depósitos pero no permite trasladar el aumento al crédito privado, comprimiendo el NIM."*

**Datos necesarios:** Tasa de política monetaria BCRA + NIM trimestral GGAL (de reportes GFG) + tasa de plazo fijo promedio del sistema (BCRA).

**Test:**
- Correlacionar `∆Tasa_referencia_BCRA` con `∆NIM_GGAL` trimestral.
- Hipótesis confirmada si la correlación es negativa (tasas más altas → NIM más comprimido).
- **Dato adicional necesario:** Serie histórica de NIM por trimestre (descargable de reportes GFG).

---

### H-13 — El precio de GGAL sube cuando las tasas reales caen (fin gradual del carry)
**Fuente:** `analisis_mercado/impacto_fin_carry_trade_ggal.md`

> *"Al caer la tasa de interés local, el denominador del DCF se achica y el VPN de GGAL sube automáticamente, anticipado meses antes de la baja efectiva."*

**Datos necesarios:** Tasa LECAP / BCRA mensual + precio GGAL mensual — ambos disponibles públicamente.

**Test:**
- Calcular `Tasa_Real = (1 + Tasa_nominal) / (1 + CER_mensual) − 1` para cada mes.
- Correlacionar `Tasa_Real_t` con `Precio_GGAL_t+3` (con lag de 3 meses para capturar la anticipación del mercado).
- Hipótesis confirmada si la correlación es negativa y estadísticamente significativa (p < 0.05).
- **Datos adicionales necesarios:** Serie CER mensual (INDEC) y precios GGAL mensuales.

---

### H-14 — GGAL exhibe estacionalidad negativa en el período mayo-octubre
**Fuente:** `analisis_mercado/efecto_sell_in_may.md`

> *"El patrón 'Sell in May and Go Away' sugiere que los retornos de mayo-octubre son inferiores a los de noviembre-abril en activos emergentes como GGAL."*

**Datos necesarios:** Serie histórica larga de precios GGAL (al menos 5 años) — disponible progresivamente en BD.

**Test:**
- Para cada año disponible, calcular el retorno semestral: `R_may_oct = (P_oct / P_apr − 1)` y `R_nov_abr = (P_abr / P_oct − 1)`.
- Comparar las distribuciones de ambos retornos (test de Wilcoxon o t de Student).
- Hipótesis confirmada si la media de `R_nov_abr` es estadísticamente superior a la media de `R_may_oct`.

---

## 5. Datos Adicionales que Potenciarían la Verificación

Los siguientes datos **no son precios de GGAL ni su tira de opciones**, pero facilitan demostrar las hipótesis anteriores:

| Dato Adicional | Hipótesis que habilita | Fuente |
|---|---|---|
| **Tasa BCRA / LECAP** (mensual) | H-12, H-13 | BCRA informe de bancos |
| **Inflación CER / IPC** (mensual) | H-12, H-13 | INDEC |
| **NPL ratio GGAL** (trimestral) | H-11, H-12 | GFG Investor Relations |
| **NIM GGAL** (trimestral) | H-12 | GFG Investor Relations |
| **Precio ADR GGAL** (en USD, NYSE) | H-13, H-14 | Yahoo Finance / Invertir Online |
| **Tipo de cambio CCL / oficial** (diario) | H-03, H-13 | BCRA / Ambito |
| **Open Interest por Strike** (histórico) | H-03, H-04 | Propia BD (tira de opciones) |
| **Volumen operado GGAL** (diario) | H-02, H-04 | Propia BD |
| **DXY** (índice dólar, diario) | H-14, contexto macro | Yahoo Finance / FRED |
| **VIX** (volatilidad global, diario) | H-06, H-07 | Yahoo Finance / FRED |
| **Índice Merval** (diario) | H-13, H-14 | Yahoo Finance / Propia BD |

---

### Referencias

- Bloomberg Línea. "Galicia prevé que el pico de morosidad llegará en marzo de 2026." [URL](https://www.bloomberglinea.com/latinoamerica/argentina/galicia-preve-pico-de-morosidad-en-marzo-de-2026/). *(Para H-11: dato de pico NPL proyectado por la propia gerencia).*
- Filippou, Ilias, Pedro Angel Garcia-Ares y Fernando Zapatero. "No Max Pain, No Max Gain." SSRN, 2022. [URL](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4140487). *(Para H-03: evidencia académica de predictibilidad del Max Pain).*
- Grupo Financiero Galicia (GFG). "Financial Statements." [URL](https://www.gfgsa.com/English/Financial-Information/Financial-Statements/default.aspx). *(Para H-11 y H-12: fuente primaria de NPL y NIM oficiales).*
- Natenberg, Sheldon. *Option Volatility and Pricing*. McGraw-Hill, 1994. [Amazon](https://www.amazon.com/Option-Volatility-Pricing-Strategies-Techniques/dp/0071818774). *(Base teórica para H-07, H-08, H-10: Variance Risk Premium y estrategias Long Vega).*
- Menthor Q. "Delta Hedging and Market Stability." 2024. [URL](https://menthorq.com/blog/delta-hedging-and-market-stability/). *(Para H-04: sustento del rol estabilizador del Gamma Exposure de Market Makers).*
