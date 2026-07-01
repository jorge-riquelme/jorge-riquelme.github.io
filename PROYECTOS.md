# Proyectos por Panel

Este documento resume, por panel, el contexto, el problema abordado y la solución implementada. Indico si el caso contiene dashboard, esquema o visualización.

## Panel: Data Analysis & Auditing

- **Disaggregated Failure Rate Analysis**
  - Contexto: Análisis de tasas de fracaso agregadas que ocultaban factores subyacentes.
  - Problema: Las tasas reportadas eran agregadas; no permitían identificar condiciones de riesgo.
  - Cómo lo resolví: Construí un dataset multi-dimensional (Demografía, Engagement, Soporte), realicé clustering, correlación y regresión, y presenté promedios por métrica.
  - Contiene: visualización (gráficos de tasa de fallas por métrica).

- **Retention Dataset Audit & ETL Transformation**
  - Contexto: Dataset en formato wide (semestres codificados en nombres de columnas) incompatible con BI dinámico.
  - Problema: Imposible filtrar por semestre sin 18 medidas estáticas.
  - Cómo lo resolví: Unpivot (wide→long) con Python y creación de dimensiones vía foreign keys; quedó listo para Power BI.
  - Contiene: transformación ETL y dataset listo para dashboard.

- **Cohort Attribution Audit**
  - Contexto: Cohortes institucionales y de programa mezcladas, sesgando métricas de retención.
  - Problema: Transferencias internas inflaban rendimiento aparente de programas.
  - Cómo lo resolví: Propuse arquitectura de atomicidad (IDs duales, flags de origen, seniority por créditos).
  - Contiene: hallazgos y arquitectura (audit).

- **From Audit to Implementation: Atomic Journey**
  - Contexto: Implementación práctica del audit anterior mediante pipeline de flags.
  - Problema: Datos transaccionales planos no distinguían eventos (transfer, repetición, salida).
  - Cómo lo resolví: Pipeline que preserva registros y añade 8 flags booleanos que reconstruyen la trayectoria estudiantil; Power BI sobre la capa de flags.
  - Contiene: dashboard Power BI en vivo y arquitectura de flags.

## Panel: Cross-Industry / Commercial

- **Adidas US — Sales & Pricing Analysis**
  - Contexto: Dataset público de Kaggle sobre ventas Adidas (2020–2021).
  - Problema: Falta de marco analítico y visión de precios/márgenes por canal.
  - Cómo lo resolví: Estructuré preguntas de negocio y construí un reporte Power BI interactivo con páginas de margen, geografía y producto.
  - Contiene: dashboard Power BI (embed).

- **Factory OEE & Downtime**
  - Contexto: Dataset de mantenimiento predictivo reorientado a OEE y eficiencia operativa.
  - Problema: No había diagnóstico claro de dónde se perdía efectividad (Availability/Performance/Quality).
  - Cómo lo resolví: Dashboard de pérdida por causa, SPC y simulación de mejoras hasta alcanzar estándar manufacturero.
  - Contiene: dashboard Power BI y análisis de causas.

- **Olist B2B Sales Funnel**
  - Contexto: Tablas públicas Olist transformadas en análisis de funnel B2B.
  - Problema: Datos parciales (solo MQLs y deals cerrados) limitan denominadores para tasas de conversión.
  - Cómo lo resolví: Diseñé un star schema, respeté límites de la data y presenté análisis de volumen vs conversión y carga por reps.
  - Contiene: dashboard Power BI y lógica de funnel.

## Panel: Education Domain

- **Early Alert System (EWS)**
  - Contexto: Arquitectura integral (Constellation Schema) para alertas tempranas y reporting multidominio.
  - Problema: Silos de datos y falta de identidad administrativa impiden análisis equitativo y accionable.
  - Cómo lo resolví: Diseñé un Data Mart multidimensional (histórico, real-time, forecast) y un sistema de alertas/ETL que alimenta Power BI.
  - Contiene: esquema (Constellation Schema), diagrama y dashboard de alertas.

## Panel: Visualization & Dashboards

- **Student Retention Analysis (Iteraciones)**
  - Contexto: Migración de reportes estáticos a dashboards interactivos (retención por cohorte).
  - Problema: Visuales estáticos impedían comparación y acción rápida; transferencias distorsionaban métricas.
  - Cómo lo resolví: Conservé la lógica fila=cohorte/columna=semestre y añadí matrices interactivas, heatmaps Deneb y flow summaries en Power BI.
  - Contiene: visualizaciones (Deneb/Vega), Power BI matrix y dashboard operativo.

- **Academic Standing Transition Matrix**
  - Contexto: Medir si las alertas/intervenciones cambiaron trayectorias académicas.
  - Problema: Falta de métricas que muestren movimiento entre estados.
  - Cómo lo resolví: Transformación a matriz de transiciones (previo→actual) y heatmap/Sankey para medir impacto.
  - Contiene: visualización (heatmap, Sankey) y dataset transformado.

- **Comprehensive Program Report / SEM / Explorations**
  - Contexto: De documentos estáticos a dashboards de Program Review y SEM.
  - Problema: Reportes descriptivos sin marco analítico ni interactividad.
  - Cómo lo resolví: Plantillas Power BI con métricas dinámicas (market position, conversion, demand/capacity) y visualizaciones Deneb para casos complejos.
  - Contiene: dashboards, Deneb visuals y plantillas reutilizables.

---

Si quieres, adapto el tono/longitud por proyecto o genero versiones listas para LinkedIn/Behance.
