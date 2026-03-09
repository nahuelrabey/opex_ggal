---
description: Reglas para la extracción y organización de información técnica desde artículos o notas.
---

# Workflow: Extracción de Información de Notas

Este procedimiento define cómo organizar de forma estandarizada la información extraída de artículos financieros, reportes de consultoras o notas de prensa para su integración en la Bitácora Opex.

## 1. Estructura del Documento
Todo archivo de apunte extraído debe seguir este orden de secciones:

### 1.1. Metadatos (Frontmatter)
Seguir estrictamente el formato de `fecha_creacion` y `fecha_edicion` definido en [escritura_archivos.md](file:///c:/Users/nahue/Desktop/bitacora_opex/.agents/workflows/escritura_archivos.md).

### 1.2. Encabezado y Link de Lectura
Título descriptivo (H1) seguido de "Apunte de lectura: [Título](URL)".

### 1.3. Sección de Apuntes
Resumen estructurado de la información técnica. Se prefiere el uso de subtítulos (H3) y listas de puntos (*bullets*) para facilitar la lectura rápida de datos macroeconómicos o financieros.

### 1.4. Sección de Entidades
Sección dedicada a identificar los actores clave citados en la nota.
- **Consultoras/Instituciones:** Registrar nombres de firmas (ej. JP Morgan, Quantum Finanzas, Fundación Mediterránea).
- **Personas:** Registrar nombres de economistas, analistas o funcionarios citados (ej. Luis Caputo, analistas de Neix).

> [!TIP]
> Si se identifica una nueva consultora o institución relevante, se debe actualizar el archivo central `directorio_entidades.md` con el nombre de la firma y el tipo de informes que provee. Esto servirá como base de datos para futuras consultas de reportes.

### 1.5. Sección de Referencias / Fuentes Recomendadas
Cierre del documento con las fuentes en formato Chicago y enlaces directos, detallando la utilidad de cada fuente según las reglas generales del proyecto.

## 2. Rigor en Datos Numéricos
Al extraer cifras (tasas de interés, porcentajes de mora, puntos básicos):
- Mantener la exactitud decimal del texto original.
- Citar el periodo específico al que corresponden los datos.
- Marcar como `(suposición del agente)` cualquier interpretación que no esté explícitamente en el texto.

## 3. Actualización de Meta-Análisis
Tras completar la extracción de datos y la organización de la información, se debe proceder según la directiva general de actualización de [meta_analisis_usuario](file:///c:/Users/nahue/Desktop/bitacora_opex/meta_analisis_usuario) definida en [escritura_archivos.md](file:///c:/Users/nahue/Desktop/bitacora_opex/.agents/workflows/escritura_archivos.md).
