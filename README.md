# JURISIN 2026 - Guia de contenidos

Este README resume lo que hay en la carpeta `JURISIN 2026` (root del repo local) para que cualquier integrante del equipo pueda saber donde esta cada recurso y reutilizarlo sin explorar manualmente. Todas las rutas se dan relativas a `JURISIN 2026` y los nombres se mantienen en ingles cuando son parte del dataset original. La carpeta mas activa hoy es `Version 2`, por eso tiene una seccion mas detallada.

## Resumen rapido en la raiz

| Elemento | Tipo | Ubicacion | Descripcion |
| --- | --- | --- | --- |
| `Drafts/` | Carpeta | `Drafts` | Borradores y entregables preliminares del manuscrito (PDF y ZIP) usados para marketing interno. |
| `Version 1/` | Carpeta | `Version 1` | Primera iteracion de notebooks y del prototipo `gray-areas-app`; conserva el historial completo de ejecuciones (`runs/`) y codigo fuente en `src/`. |
| `Version 2/` | Carpeta | `Version 2` | Entorno mas reciente de experimentos, graficos y modelos; contiene resultados consolidados y archivos auxiliares. |
| `jurisin2026 Submission 20.pdf` | Archivo | raiz | Version enviada del paper (20 de marzo 2026); usarla como referencia editorial. |
| `technical_appendix.pdf` | Archivo | raiz | Apendice tecnico con detalles metodologicos para reviewers. |

### Detalle de `Drafts/`
- `A Computational Framework to Uncover Gray Areas in Tax Legislation.pdf`: poster preliminar.
- `draft1.zip`: paquete con figuras y texto de la primera version colega.
- `draft2.pdf`: segundo borrador del paper.
- `Elicit - Tax Law Complexity and compliance.pdf`: export de notas de investigacion de Elicit.

### Detalle de `Version 1/`
- Notebooks raiz (`00_Loopholes.ipynb`, `01_Loopholes.ipynb`, `Complexity Index.ipynb`, `Embeddings comparison.ipynb`, `Robustez.ipynb`): analisis exploratorios originales.
- `gray-areas-app/`: contiene datos de entrada (`data/`), ejemplos (`sample_dataset*.csv`), textos UI (`copy/`), ejecuciones (`runs/` con subcarpetas `debug_*`, `run_*` y archivos `metrics.json`, `manifest.json`, etc.) y el codigo de la app (`src/`, `shared/`, `viewer/`, `theme/`).
- `Images/`: concentrado de graficos exportados (matrices de confusion, boxplots, distribuciones); incluye subcarpetas `Boxplot` y `confmat2` para variantes cromaticas.
- `related-work-review/Related_Work_Final.md`: resumen del estado del arte.
- `temp/`: archivos temporales como `requirements.txt` y resultados intermedios.

## Version 2 (detalle ampliado)

### Archivos en la raiz de `Version 2`
- `.gitconfig`: preferencias de git solo para esta carpeta (se ignora en otros equipos).
- `results.ipynb`: notebook maestro con celdas para sumarizar metricas y exportar tablas en la nueva version.
- `paper_figures/`: hub central de figuras camera-ready y notebooks de produccion para el paper.

### Subcarpetas y archivos

#### `paper_figures/`
- `notebooks/`: notebooks finales usados para generar figuras listas para paper.
  - `paper_scatter_plots.ipynb`
  - `paper_kde_plots.ipynb`
  - `paper_confmat_mel2.ipynb`
  - `paper_complexity_quadrants.ipynb`
  - `paper_complexity_boxplots.ipynb`
  - `paper_class_distribution.ipynb`
- `scatter/`: exports del bloque scatter UMAP (individuales, panel y `paper_scatter_export_log.csv`) en PNG/SVG/PDF.
- `kde/`: exports KDE UMAP por indicador (variantes `with_title` y `without_title`) + log CSV en PNG/SVG/PDF.
- `confmat_mel2/`: matrices de confusion MEL2 por indicador + panel 5 indicadores + log CSV en PNG/SVG/PDF.
- `complexity/`: figuras de complejidad/riesgo (opcion dual-panel, opcion hexbin, paneles separados, boxplots por indicador y metadatos) en PNG/SVG/PDF.
- `distribution/`: grafico `paper_distribution_articles_by_class` + archivos auxiliares (`__counts.csv`, `__metadata.csv`) en PNG/SVG/PDF.

#### `complexity/`
- `boxplot_complexity_active__all_categories.png`: boxplot que combina todas las dimensiones activas del indice.
- `boxplot_complexity__{Target}.png` (Completeness, Differential_Regime, Discretionality, Interpretability, Relevance): graficos por dimension.
- `boxplot_data__complexity_active__{Target}.csv`: datos agregados que alimentan cada boxplot.
- `boxplot_risk_by_complexity.png`: compara puntajes de riesgo vs. complejidad media.
- `quadrants_complexity_vs_risk.png`: grafica de cuadrantes para clasificar articulos por riesgo/indice.

#### `Embeddings/`
- `mel_embeddings.npy`: matriz de embeddings del modelo MEL para Version 2.
- `mel_umap_2d.csv`: proyeccion UMAP 2D con coordenadas y metadatos necesarios para graficar.

#### `kde umap/`
- `kde_data__{dimension}.csv` (5 dimensiones + `risk_score`): densidades estimadas para cada categoria.
- `kde_mel_umap__{dimension}.png` y `kde_mel_umap__risk_score_gt_4_5.png`: visualizaciones KDE en el plano UMAP por dimension y para articulos con riesgo > 4.5.

#### `LegalBERT/`
- `model_legalbert_logreg__{Target}.joblib`: modelos Logistic Regression entrenados sobre embeddings de Legal-BERT.
- `preds_legalbert__{Target}.csv`: predicciones por documento.
- `report_legalbert__{Target}.csv`: precision/recall/F1 para train/test.
- `confmat_legalbert__{Target}.csv`: matrices de confusion.
- `summary_legalbert__all_targets.csv`: resumen tabular multi-objetivo.
- `results_legalbert__all_targets.txt`: log human-readable con hiperparametros y scores.

#### `LegalElectra/`
- Estructura equivalente a `LegalBERT` pero usando embeddings Legal-ELECTRA (los archivos conservan el prefijo `legalbert` aunque las corridas provienen de Electra).

#### `MEL 2/`
- `mel_embeddings.npy`: embeddings actualizados tras ajustes de limpieza.
- `model_mel_logreg__{Target}.joblib`, `preds_mel__{Target}.csv`, `report_mel__{Target}.csv`, `confmat_mel__{Target}.csv`: modelos Logistic Regression y salidas para cada dimension.
- `results_mel__all_targets.txt` y `summary_mel__all_targets.csv`: resumen textual/tabular general.
- `split_ids_mel__{Target}__train.csv` y `...__test.csv`: divisiones exactas usadas en entrenamiento/validacion.

#### `MEL1/`
- Misma estructura que `MEL 2` pero corresponde al primer barrido de experimentos MEL; util para comparar drift entre corridas.

#### `others/`
- `distribution_by_class.pdf`: grafico de balance de clases.
- `Gemini_3.xlsx`, `gemini_final_comparison_updated.xlsx`: experimentos de LLM Gemini para etiquetas y comparacion.
- `GPT-5-2.csv.xls`, `GPT-5.2.csv.xls`, `GPT-5_2.csv.xls`, `GPT-5.2.xlsx`: resultados descargados de GPT-5.2 con diferentes formatos.
- `law_article_spanish_text.xlsx`: tabla con articulos completos en espanol.
- `scatter_mel_umap__Completeness.pdf`: version en PDF del scatter 2D.
- `LLM/spanish_text_only.csv`: dataset depurado que contiene solo texto de articulos para prompts.

#### `outputs/`
- `base_with_risk_score_and_perturbations.csv`: dataset consolidado con puntaje de riesgo y variantes perturbadas.
- `df_llm_annotated.csv`: anotaciones provenientes de LLM.
- `mel_embeddings*.npy`: embeddings base, con reordenamientos de frases (`__phrase_reorder`) y reemplazos de sinonimos al 10% (`__syn_replace_10pct`).
- `model_mel_logreg__{Target}.joblib`, `tfidf_logreg_model.joblib`: modelos finales MEL y TF-IDF.
- `preds_mel__{Target}.csv` y `preds_mel__{Target}__test_syn_phr.csv`: predicciones regulares y sobre conjuntos perturbados (sinonimos + reordenamiento).
- `report_mel__{Target}.csv`, `confmat_mel__{Target}.csv`: reportes y matrices para cada objetivo.
- `split_ids_mel__{Target}__train.csv` / `__test.csv`: indices de particion.
- `summary_mel__all_targets.csv` y `results_mel__all_targets.txt`: resumen general.

#### `Scatter mel umap/`
- `scatter_data__{dimension}.csv` y `scatter_data__gray_rule_allbin0_or_interp1.csv`: datos XY y reglas de color para cada grafico.
- `scatter_mel_umap__{dimension}.png` y `scatter_mel_umap__gray_rule_allbin0_or_interp1.png`: imagenes PNG.
- `pdf_plots/`: mismos graficos exportados a PDF para prensa.

#### `sensitivity/`
- `base_with_risk_score_and_perturbations.csv`: copia con el subconjunto utilizado para pruebas de robustez (sirve para rastrear experimentos sin tocar `outputs/`).

#### `TFIDF/`
- `model_tfidf_logreg__{Target}.joblib`: modelos TF-IDF + LogReg.
- `preds__{Target}.csv`, `report__{Target}.csv`, `confmat__{Target}.csv`: salidas por dimension.
- `summary__all_targets.csv` y `results__all_targets.txt`: resumen global TF-IDF.

## Como usar este README
1. Revisa la tabla inicial para identificar en que carpeta esta el recurso que necesitas.
2. Ve directo a la seccion `Version 2` si vas a continuar experimentos o generar figuras nuevas.
3. Si necesitas reproducir corridas antiguas, consulta `Version 1` y en especial `gray-areas-app/src` para scripts.
4. Actualiza este README cuando se agreguen nuevas corridas o indicadores; manteniendo el mismo formato evitamos perdida de contexto.
