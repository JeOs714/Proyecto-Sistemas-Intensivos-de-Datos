# OceanWatch Analytics — Entrega 1

**MINE 4213 · Sistemas Intensivos de Datos · Universidad de los Andes · 2026-20**

**Equipo:** Santiago Palacios - Jesus Ospino - Miguel Benavides

Exploración, preguntas de negocio y almacenamiento óptimo del tráfico marítimo
AIS de NOAA (1–7 de junio de 2023, ~150 M de posiciones).

## Entorno

- **Databricks Free Edition** (cómputo *serverless*). Sin `cache()` ni `persist()`: no están disponibles en serverless. Cada acción vuelve a leer desde el almacenamiento.
- H3 con las funciones nativas de Databricks (`h3_longlatash3`, resolución 8).

## Estructura

- `01_ingesta_ais.py`: descarga de NOAA con reintentos y verificación, descompresión en el Volume y lectura con esquema explícito.
- `02_exploracion_calidad.py`: perfil del corpus y tablero de problemas de calidad.
- `03_queries.ipynb`: las 5 preguntas de negocio (3.a–3.e).
- `04_almacenamiento.py`: CSV vs Parquet vs Delta, `partitionBy` vs `CLUSTER BY`, archivos leídos y efecto de `OPTIMIZE`.
- `05_gobernanza`: catálogo y esquemas propios en Unity Catalog, con comentarios y metadatos.

## Cómo ejecutar

1. Correr los notebooks **en orden**: `01 → 02 → 03 → 04 → 05`.
2. Antes del `03`, subir **a mano** el CSV del [World Port Index](https://www.kaggle.com/datasets/mexwell/world-port-index) (`UpdatedPub150.csv`) a `/Volumes/workspace/default/oceanwatch/raw/csv/`. Lo usan las consultas 3.d y 3.e.

## Bitácora

| clase | tema | pieza que aportó al proyecto | dónde |
|---|---|---|---|
| Semana 5 | Práctica de Spark: lo que cambia con datos grandes | Ingesta con esquema explícito, agregaciones en una pasada, ventanas (`lag`), joins, aproximaciones, lectura del plan | `01`, `02`, `03` |
| Semana 6 | Formatos de almacenamiento | Parquet vs Delta, `partitionBy` vs `CLUSTER BY`, *data skipping*, `OPTIMIZE`, *time travel* | `04` |
| Semana 7 | Gobernanza de datos | Catálogo y esquemas propios en Unity Catalog; comentarios y metadatos en las tablas | `05` |
