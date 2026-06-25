# nlp-resenas-banca

Análisis NLP de reseñas de clientes de banca en Trustpilot: sentimiento por tema y comparación contra el sector.

## Entorno

```bash
python3.12 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Estructura

```
nlp-resenas-banca/
├── data/               # CSV crudo (~124 MB, ignorado por Git)
├── notebooks/
│   └── analisis_resenas_banca.ipynb
├── outputs/
│   ├── figures/
│   └── tables/
├── requirements.txt
├── .gitignore
└── README.md
```
