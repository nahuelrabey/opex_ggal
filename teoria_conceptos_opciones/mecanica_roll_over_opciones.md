---
fecha_creacion: "2026-02-23"
fecha_edicion: "2026-02-23"
---
# Teoría y Práctica: Mecánica y Costos del "Roll Over"

Cuando un operador vende opciones (la pata "corta" de un Diagonal Spread o Strangle) y la acción subyacente realiza un movimiento violento en su contra, rompiendo el *Strike* vendido antes del vencimiento, la posición entra en zona crítica (Riesgo de Asignación). 

Para evitar el ejercicio forzoso y ganar tiempo para que su tesis original se cumpla, el operador profesional acude a una maniobra defensiva esencial: el **Roll Over** (o "rolar" la posición).

## 1. ¿Qué significa hacer un Roll Over?

"Rolar" una opción no es una operación mágica ni un botón único en la plataforma del bróker. Es, de hecho, **la ejecución simultánea de dos órdenes combinadas**:
1. **Buy to Close (Recomprar):** Comprar la misma opción que habías vendido originalmente para cerrar esa posición con pérdida contable consolidada.
2. **Sell to Open (Vender Nuevo):** Vender una nueva opción del mismo subyacente, pero con una fecha de expiración más lejana (y habitualmente un Strike distinto) para volver a cobrar prima.

El objetivo del Roll Over es utilizar el dinero fresco que cobramos en el Paso 2 para pagar (o subsidiar) la pérdida de la recompra dolorosa del Paso 1, ganando meses adicionales de tiempo.

## 2. Tipos de Roll Over y sus Costos

Imaginemos que vendiste un CALL de Abril Strike 60 por $2,00. Súbitamente, un "TACO trade" de buenas noticias dispara GGAL a 65 en Marzo. Tu Call vendido ahora vale $8,00 y estás perdiendo $6,00. Faltan semanas para Abril y te van a ejercer. 

Existen tres formas de Rolar para apagar este incendio, clasificadas según su **Costo Neto (Flujo de Caja)**:

### A. Roll por Débito (Costoso - Sangría de Capital)
- **Mecánica:** Recomprás tu Call de Abril 60 (pagás -$8,00) y vendés un Call de Junio 70 (cobrás +$5,00). 
- **Flujo de Caja:** Pones **-$3,00 de tu bolsillo** para realizar la maniobra.
- **Análisis:** Estás comprando paz mental al alejar fuertemente el Strike fuera de peligro (hacia 70), pero estás inyectando dinero fresco al mercado. El spread te cobra un peaje, reduciendo tu ganancia neta final o agrandando tu pérdida.

### B. Roll a Precio Cero (Break-Even)
- **Mecánica:** Buscas en la cadena de opciones (*Option Chain*) una venta futura que valga exactamente lo que tenés que pagar hoy. Recomprás tu Call de Abril 60 (-$8,00) y vendés un Call de Junio Strike 66 por (+$8,00).
- **Flujo de Caja:** Movimiento de $0.
- **Análisis:** Cerraste el riesgo inminente de Abril y pateaste el problema a Junio sin sacar un peso de la cuenta, ampliando un poco el radio de protección del Strike (de 60 a 66).

### C. Roll por Crédito (Ideal - El Santo Grial Defensivo)
- **Mecánica:** Recomprás el Call Abril 60 (-$8,00), pero te vas tan lejos en el tiempo (Ej. Call Agosto 65) que la nueva opción, cargada de meses de *Theta* y *Vega*, vale muchísimo. La vendés cobrando (+$10,00).
- **Flujo de Caja:** Literalmente **cobrás +$2,00** por arreglar tu error.
- **Análisis:** El mercado te paga por extender tu agonía direccional gracias a la sobretasa del Valor Temporal lejano. Resolviste la amenaza inminente de Abril, mejoraste tu Strike de Defensa (pasaste de 60 a 65), y encima te quedó crédito libre. Este es el Roll Over obligatorio para los lanzadores de crisis.

## 3. El Costo Oculto: El Costo de Oportunidad y el Margen

Aunque el "Roll por Crédito" suene a dinero gratis, el Roll Over impone costos duros:

1. **Atrapamiento del Capital (Margin Tie-up):** Al rolar la posición vendida a meses o años vista (ej. de Abril a Octubre), tu bróker seguirá bloqueándote las garantías o acciones retenidas como margen durante todo ese semestre adicional. Capital que no podes usar para tradear otras oportunidades emergentes.
2. **Efecto Bola de Nieve (*Whipsaw* Extremo):** Si rolas a un Strike más alto por crédito hacia Agosto, y GGAL sigue subiendo irracionalmente a 85 para Julio, tu nueva posición vendida volverá a causarte pérdidas masivas. Estarás en un ciclo perpetuo de perseguir al mercado, perdiendo lentamente en cada "Roll" hasta que tu cuenta sea marginada.
3. **Pérdida de la "Cuna" (Skewing the Spread):** Si estabas en un *Double Diagonal* esperando un rango, y por salvar pata alcista la rolas eternamente hacia arriba, se destruye la simetría original de la estrategia. Dejás de ganar por oscilación lateral para convertirte simplemente en un administrador de salvamento de pérdidas.

### Conclusión Estratégica
El Roll Over es un extintor de incendios: fundamental para que no se te queme la casa (Asignación/Ejercicio ITM), pero muy costoso si se usa recurrentemente porque inmoviliza capital y aniquila la rentabilidad teórica de la estrategia inicial. 

---

### Fuentes recomendadas
- **Taleb, Nassim Nicholas** - *"Dynamic Hedging: Managing Vanilla and Exotic Options"*. (Sobre la falacia de rolar perpetuamente opciones vendidas para enmascarar pérdidas direccionales frente a movimientos extermos).
- **Investopedia:** 
  - [Roll Forward](https://www.investopedia.com/terms/r/rollforward.asp) (Mecánica de cerrar posiciones cercanas para abrir contratos con fecha de vencimiento posterior).
