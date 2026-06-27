# Análisis NLP de reseñas de clientes bancarios — Trustpilot UK

Análisis de sentimiento y topic modeling sobre reseñas públicas de Trustpilot UK del sector bancario. Se compara **HSBC** contra un pool de 9 competidores para identificar en qué temas la experiencia del cliente es mejor o peor que el sector, y se traducen los hallazgos en recomendaciones para dirección.

## Hallazgos principales

| Tema | HSBC neg | Pool neg | Diferencia |
|------|----------|----------|------------|
| App y banca digital | 80.0% | 43.1% | **+36.9 pp** ⚠️ |
| Atención al cliente | 78.3% | 74.2% | +4.1 pp |
| Experiencia general | 66.7% | 69.5% | −2.9 pp |
| Tarjetas y transferencias | 66.7% | 77.5% | −10.8 pp ✓ |
| Cuenta y fraude | 60.0% | 88.1% | **−28.1 pp** ✓ |
| Atención presencial | 27.3% | 32.9% | −5.6 pp ✓ |

**Historia central:** la app deficiente deriva clientes al canal de voz, saturando atención al cliente — el 47 % de las reseñas de HSBC se concentran en estos dos temas.

## Dataset

- **Fuente:** Trustpilot Reviews (123 k reseñas · 1.680 empresas · UK)
- **Muestra de trabajo:** 1.000 reseñas — 100 HSBC + 100 × 9 competidores
- **Dataset crudo (124 MB):** no incluido en el repositorio (`.gitignore`)
- **Dataset procesado (2 MB):** `data/processed/reviews_banca_hsbc_pool.csv`

## Stack técnico

Python 3.12 · `transformers` (nlptown BERT multilingual) · `scikit-learn` (TF-IDF, NMF) · `sentence-transformers` (similitud coseno) · `pandas` · `seaborn` · `matplotlib`

## Cómo ejecutar

```bash
python3.12 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Abrir `notebooks/analisis_reseñas_banca.ipynb` y ejecutar las celdas en orden.

> **Nota:** las secciones 1 y 2 requieren el CSV crudo (`data/trustpilot-reviews-123k.csv`).
> Las secciones 3 a 8 funcionan con el dataset procesado incluido en el repositorio.

## Estructura del análisis

| Sección | Descripción |
|---------|-------------|
| 1. EDA | Demostración de la estratificación artificial de estrellas |
| 2. Empresa y pool | HSBC como target · 9 competidores por similitud coseno |
| 3. Limpieza de texto | Versión ligera (sentimiento) y pesada (topics) |
| 4. Sentimiento | `nlptown/bert-base-multilingual-uncased-sentiment` (1–5) |
| 5. Temas (NMF) | TF-IDF + NMF · K=8 temas interpretables de negocio |
| 6. Cruce tema × sentimiento | Diferencias de negatividad por tema vs. pool |
| 7. Visualizaciones | 4 gráficos para audiencia no técnica |
| 8. Conclusiones | Hipótesis contrastadas · recomendaciones · limitaciones |

## Estructura del repositorio

```
nlp-resenas-banca/
├── data/
│   └── processed/
│       └── reviews_banca_hsbc_pool.csv   # 1.000 reseñas (2 MB)
├── notebooks/
│   └── analisis_reseñas_banca.ipynb      # notebook principal (entregable)
├── outputs/
│   └── figures/                          # 10 visualizaciones
│       ├── eda_sesgo_estrellas.png
│       ├── pool_similitud_coseno.png
│       ├── eda_longitud_texto.png
│       ├── sentimiento_distribucion_nlptown.png
│       ├── sentimiento_por_empresa.png
│       ├── negatividad_por_tema.png
│       ├── g1_tono_global.png
│       ├── g2_volumen_por_tema.png
│       ├── g3_heatmap_negatividad.png
│       └── g4_cuadrante_prioridad.png
├── requirements.txt
└── README.md
```
