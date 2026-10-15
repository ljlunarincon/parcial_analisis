[README.md](https://github.com/user-attachments/files/33469335/README.md)
# Parcial – Análisis: Predicción de diabetes

**Autora:** Lizeth Luna
**Docente:** Ing. Carlos Carrascal
**Fecha:** 14/10/2026

> Ejercicio académico. Los modelos de este proyecto **no** deben usarse para diagnosticar pacientes ni para tomar decisiones clínicas.

## Descripción

Notebook de Google Colab que predice si un paciente tiene diabetes (clasificación binaria) usando Python, visualización de datos y redes neuronales. El trabajo sigue los seis bloques del enunciado del parcial.

## Dataset

- Fuente: [Diabetes – Kaggle (datascikhan)](https://www.kaggle.com/datasets/datascikhan/diabetes)
- Archivo: `diabetes_large_dataset.csv` (100.000 filas y 209 columnas)
- Variable objetivo: `diabetes`, construida a partir de `diabetes_type` (vale 1 si el tipo es distinto de "No Diabetes"; se usa `diabetes_status` cuando falta). Se eliminaron 42 filas sin diagnóstico, quedando 99.958 pacientes (72 % sin diabetes y 28 % con diabetes).
- El dataset **no se incluye** en este repositorio por su tamaño: debe descargarse de Kaggle.

## Archivos

| Archivo | Contenido |
| --- | --- |
| `parcial_analisis_final.ipynb` | Notebook completo con código, salidas, interpretaciones e informe |
| `README.md` | Este documento |

## Cómo ejecutarlo

1. Descargar el dataset de Kaggle (viene en un `.zip`).
2. Abrir `parcial_analisis_final.ipynb` en Google Colab (Archivo → Subir cuaderno).
3. Ejecutar todas las celdas (Entorno de ejecución → Ejecutar todo).
4. Cuando aparezca el botón de subida, cargar el `.zip` o el `.csv`.

Librerías: pandas, numpy, matplotlib, seaborn, scikit-learn y TensorFlow/Keras (ya incluidas en Colab). Semilla fija `SEED = 42` para reproducir los resultados.

## Contenido del notebook

1. **Bloque 1 – Carga e inspección:** tamaño, tipos, nulos, duplicados, variable objetivo, diccionario de datos y función de resumen.
2. **Bloque 2 – Limpieza y transformación:** valores imposibles, imputación (mediana y moda), outliers, codificación One-Hot y control de fuga de información.
3. **Bloque 3 – Análisis exploratorio:** gráficos (a) a (f) con su interpretación.
4. **Bloque 4 – Modelos tradicionales:** regresión logística y árbol de decisión.
5. **Bloque 5 – Red neuronal (Keras):** 16 y 8 neuronas con ReLU, salida sigmoide, EarlyStopping.
6. **Bloque 6 – Informe ejecutivo:** conclusión de 300 a 500 palabras, además de la pregunta de nivel alto y las respuestas del enunciado.

## Resultados principales (conjunto de prueba)

| Modelo | Accuracy | Precision | Recall | F1 | AUC |
| --- | --- | --- | --- | --- | --- |
| Regresión logística | 0,780 | 0,587 | 0,729 | 0,650 | 0,842 |
| Árbol de decisión | 0,785 | 0,608 | 0,655 | 0,630 | 0,817 |
| Red neuronal | 0,821 | 0,683 | 0,674 | 0,679 | 0,846 |

Se eligió la regresión logística entre los modelos tradicionales por su mayor recall, ya que lo más costoso es dejar pacientes con diabetes sin detectar. Con un umbral de decisión de aproximadamente 0,39 (elegido con validación cruzada, sin usar la prueba), el recall sube de 0,729 a 0,799 a costa de menor precision.

## Puntos importantes

- **Fuga de información:** la primera ejecución dio 100 % de accuracy. Se excluyeron variables que ya contenían el diagnóstico (medicamentos, complicaciones, `chronic_condition_count`, entre otras) y se agregó una auditoría automática con el AUC individual de cada variable.
- **Preprocesamiento sin filtración:** imputación, escalado y One-Hot se ajustan solo con el conjunto de entrenamiento.
- **Limitaciones:** el dataset parece sintético o con ruido (por ejemplo, 146 pacientes "sin diabetes" con HbA1c mayor de 10 %), por eso las métricas son moderadas.
