---
description: Reglas y convenciones para la escritura de archivos en el proyecto
---

# Reglas de Escritura de Documentos para Agentes

Al generar, modificar o interactuar con archivos de texto/markdown en el proyecto "Bitácora Opex", todos los agentes de Inteligencia Artificial deben adherirse estrictamente a las siguientes directrices:

## 1. Metadatos de Fechas (Frontmatter)
Todo documento nuevo o modificado debe comenzar con un bloque de metadatos YAML (Frontmatter) que contenga exclusivamente las variables `fecha_creacion` y `fecha_edicion`. Estas fechas deben representarse en formato `YYYY-MM-DD`.

**Ejemplo de implementación obligatoria:**
```yaml
---
fecha_creacion: "YYYY-MM-DD"
fecha_edicion: "YYYY-MM-DD"
---
```
*Nota: Si el agente edita un archivo ya existente, debe actualizar únicamente el valor de `fecha_edicion` al día actual.*

## 2. Respaldo y Veracidad de las Afirmaciones
El rigor técnico es fundamental en este proyecto. Al desarrollar explicaciones sobre macroeconomía, finanzas, derivados u operatoria bursátil:
- **Cada afirmación, dato o concepto crítico debe estar respaldado por una fuente** explícita o implícita comprobable (ej. fórmulas matemáticas establecidas, datos de mercado, etc.).
- **Etiqueta Obligatoria:** Si el agente realiza una afirmación que no emerge estrictamente de una fuente externa verificable, sino que es producto de su propia deducción, inferencia, lógica interna, o escenario hipotético propio, **debe marcarse en el mismo párrafo** añadiendo la etiqueta `(suposición del agente)` entre paréntesis.

## 3. Sección de Referencias al Finalizar
Para garantizar la trazabilidad del conocimiento y fomentar el aprendizaje continuo, todos los documentos deben incluir una sección de cierre obligatoria.
- Al final de cada archivo markdown se debe añadir un apartado titulado `### Fuentes recomendadas` o `### Referencias`.
- En este apartado, el agente debe enumerar libros académicos (ej. *John C. Hull*, *Sheldon Natenberg*), artículos técnicos de sitios confiables (ej. *Investopedia*, *CME Group*), o autores institucionales.
- Por cada fuente listada, se debe incorporar una cursiva o paréntesis indicando **para qué sirve exactamente esa fuente** en alusión a los temas recién abordados en el documento.
