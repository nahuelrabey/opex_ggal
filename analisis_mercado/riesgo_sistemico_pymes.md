---
fecha_creacion: "2026-02-26"
fecha_edicion: "2026-02-26"
---

# Riesgo Sistémico y Contagio Financiero por Quiebra Masiva de PyMEs

Este documento analiza la hipótesis planteada en la bitácora diaria: *"¿Pueden las quiebras que se ven en PyMEs generar una cesación de pagos que impacte a los bancos, sin necesidad de que quiebren primero las grandes empresas?"*.

## 1. El Canal Directo: Incremento de Préstamos Dudosos (NPLs)

La respuesta corta es **sí, una quiebra masiva de PyMEs impacta directamente la solvencia bancaria**.

Las PyMEs dependen en gran medida del financiamiento bancario tradicional, dado que no tienen acceso a los mercados de capitales (emisión de bonos corporativos o acciones) como las grandes corporaciones. Cuando el ecosistema PyME entra en estrés, se produce un aumento inmediato de los **Préstamos Dudosos o en Mora** (*Non-Performing Loans* - NPLs) en los balances del sector bancario.

El Fondo Monetario Internacional (FMI) modela este riesgo sistémico demostrando que la acumulación de pérdidas por créditos a PyMEs erosiona el capital bancario. Si bien el crédito de *una sola* PyME no es sistémicamente importante, la **correlación de defaults** (miles de PyMEs quebrando al mismo tiempo por un shock macroeconómico idéntico, como recesión o salto de tasas) genera un daño agregado que puede paralizar la capacidad de crédito del país entero.

FMI. "Policies to Address Corporate Distress in the Wake of the COVID-19 Pandemic". Washington, DC: International Monetary Fund, 2021. [Disponible en IMF.org](https://www.imf.org). *(Referencia macroeconómica sobre cómo el default masivo de PyMEs agota el capital del sistema bancario)*.

*(suposición del agente)*: En el caso de Argentina, para evaluar este riesgo de forma aplicada, no solo se debe mirar la tasa actual de NPLs (mora), sino el **porcentaje de la cartera comercial del banco** que está exposición directa a pequeñas y medianas empresas frente al que está en empresas corporativas grandes o títulos públicos. 

## 2. El Canal Indirecto: Contagio por Crédito Comercial (*Trade Credit Contagion*)

Existe un segundo mecanismo, aún más peligroso y rápido que el bancario, llamado **Efecto Dominó en la Cadena de Suministro** o *Trade Credit Contagion*.

Las empresas no solo se financian con bancos, sino financiándose entre sí al diferir el pago a proveedores (a 30, 60 o 90 días). Cuando una PyME quiebra, automáticamente "defaultea" sus facturas pendientes con sus proveedores (que en su mayoría son otras PyMEs). 

Ese proveedor, al no cobrar, sufre un shock de liquidez inmediato. Al no tener colchones financieros (*buffers*) grandes, se ve forzado a:
1. Dejar de pagarle a sus propios proveedores (propagando el default en la cadena).
2. Dejar de pagar sus cuotas bancarias.
3. Despedir empleados.

La literatura académica define esto como una reacción en cadena. El Banco de Pagos Internacionales (BIS) y la academia han documentado que el *trade credit* crea una red fuertemente interconectada. Una quiebra local se transmite rápidamente a toda la red, transformando un problema de un sector específico en una crisis generalizada.

Boissay, Frederic, y Reint Gropp. "Trade Credit Defaults and Liquidity Provision by Firms." Fráncfort: Banco Central Europeo, Working Paper Series, 2007. [Disponible en ECB.europa.eu o BIS.org](https://www.bis.org/publ/workfs15.pdf). *(Estudio empírico sobre cómo el default de un cliente fuerza al proveedor a no honrar sus propias deudas, propagando la cesación de pagos).*

## 3. ¿Es necesaria la quiebra de Grandes Empresas para afectar a los Bancos?

**No.** El supuesto de que la crisis debe viajar *Pequeñas -> Grandes -> Bancos* es mecánicamente incorrecto por dos razones:

1. **Topología Bancaria:** Los bancos regionales o de segundo nivel tienen carteras de préstamos altamente concentradas en PyMEs. Una quiebra masiva de PyMEs hará que estos bancos medianos quiebren o requieran rescates directos de la autoridad monetaria, inyectando riesgo sistémico (como demostró el caso de *Silicon Valley Bank*, donde los clientes no eran megacorporaciones, sino *startups* y pymes endeudadas).
2. **Las Grandes como dique de contención:** Irónicamente, las empresas grandes muchas veces "absorben" el choque cortando el crédito a las PyMEs y acumulando caja, salvándose a sí mismas pero acelerando la asfixia del sector bajo y transfiriendo el problema directamente a los bancos expuestos al *retail* comercial.

## 4. Conclusión Analítica 

Una quiebra generalizada y correlacionada de PyMEs **es motivo suficiente y autónomo** para gatillar una crisis bancaria, debido a la destrucción de los balances de la red de *crédito comercial* y a la escalada explosiva de los *Non-Performing Loans* en la banca tradicional. No se requiere la caída de corporaciones de primer nivel para que las tasas de morosidad perforen los niveles de capital regulatorio exigido y el sistema financiero se enfrente a una crisis sistémica de liquidez.

---

### Referencias

- FMI. "Policies to Address Corporate Distress in the Wake of the COVID-19 Pandemic". Washington, DC: International Monetary Fund, 2021. [Enlace al organismo](https://www.imf.org). *(Para dimensionar cómo el fracaso de pequeñas firmas sin recursos agota el capital de reserva bancario a nivel macro).*
- Boissay, Frederic, y Reint Gropp. "Trade Credit Defaults and Liquidity Provision by Firms." Fráncfort: Banco Central Europeo, Working Paper, 2007. [Enlace BIS](https://www.bis.org). *(Documento técnico indispensable para entender la mecánica empírica del contagio de red: cómo una factura impaga destruye la liquidez a varios nodos de distancia).* 
- Banco de Pagos Internacionales (BIS). "SMEs and structural vulnerabilities in the financial system". [BIS.org](https://www.bis.org). *(Para el análisis sobre la exposición riesgosa de los bancos de mediano tamaño hacia las pymes y la morosidad como factor sistémico puro).*
