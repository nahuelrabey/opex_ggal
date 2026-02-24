# Ajustes en Contratos de Opciones GGAL - Febrero 2026

## Resumen de la Situación
Durante el mes de febrero de 2026, el Grupo Financiero Galicia (GGAL) distribuyó dividendos, lo cual motivó ajustes automáticos por parte de BYMA en las opciones negociadas. Cuando una acción entra a cotizar "ex-cupón" (ex-dividendo), los mercados de derivados ajustan proporcionalmente los *strikes* (precios de ejercicio) de las opciones vigentes para mantener la equidad.
Consecuentemente, **las letras y números del símbolo (ticker) del contrato también se modifican** para reflejar este cambio en el precio de ejercicio y marcar la serie como ajustada.

## Datos del Evento Corporativo (Dividendos)
Diferentes fuentes confirman el pago de dividendos en esta ventana:
- **Fecha ex-dividendo (Corte de cupón):** Cerca del 2 y 6 de febrero de 2026.
- **Fecha de pago:** 9 y 11 de febrero de 2026.
- **Montos aproximados reportados:** ARS 24.57 por acción local y USD ~0.145 por ADR.

## Impacto en Símbolos y Strikes (Vencimiento Feb 2026)
- Al realizarse el corte del cupón, BYMA emite circulares informativas bajo el asunto **"Opciones Ex cupón Grupo Financiero Galicia"** o actualización de "Series de Opciones" (con vencimiento al 20 de febrero de 2026).
- **El problema de la ingesta de datos:** Debido a esta alteración del símbolo, tu base de datos o script que espera el viejo *ticker* (previo al ajuste del dividendo de principios de mes) ha dejado de recibir datos, puesto que en BYMA esos contratos pasaron a transarse bajo el nuevo símbolo ajustado y el nuevo strike descontado.

## Enlaces Específicos y Fuentes de Consulta
1. **BYMA - Comunicados Oficiales:** Este tipo de ajustes se publican en comunicados oficiales en la semana del ajuste.
   - [Buscador de Comunicados BYMA](https://www.byma.com.ar/comunicados/) (Para chequear la circular exacta de los primeros días de febrero con el listado de nuevos símbolos frente a los viejos).
   - [BYMA Data - Opciones](https://bymadata.com.ar/#/derivatives)
2. **Información de Dividendos (Febrero 2026):**
   - [StockEvents - GGAL Dividend Info](https://stockevents.app/en/stocks/BCBA/GGAL)
   - [MarketScreener - Calendario GGAL](https://www.marketscreener.com/quote/stock/GRUPO-FINANCIERO-GALICIA--6397022/calendar/)
