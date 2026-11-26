# Entrega-2
# Clasificación Automatizada de Patologías Oculares mediante Aprendizaje Profundo (ODIR-5K)

Proyecto de visión por computador para la detección y clasificación multiclase de 8 categorías diagnósticas a partir de imágenes de fondo de ojo (retinografías) utilizando Redes Neuronales Convolucionales (CNN) y Transferencia de Aprendizaje (*Transfer Learning*) en PyTorch.

---

## 🎥 Video de Presentación
* **Enlace en YouTube:** [Ver presentación del proyecto en YouTube](https://youtu.be/mw9VS1npqQY)

---

## 📁 Estructura del Repositorio

Los cuadernos están numerados secuencialmente y son autocontenidos para su ejecución directa en **Google Colaboratory**:

* `01 - exploracion_de_datos.ipynb`: Análisis exploratorio (EDA), verificación de integridad de las 6.392 imágenes y análisis del desbalance de clases.
* `02 - preprocesado_y_validacion.ipynb`: Limpieza de etiquetas por ojo individual, partición sin fuga de datos agrupada por paciente (`GroupKFold`), cálculo de pesos inversos por clase y *Data Augmentation*.
* `03 - arquitectura_linea_base_scratch.ipynb`: Entrenamiento y evaluación de la arquitectura de línea base **ResNet-18 desde cero** (*from scratch*).
* `04 - iteracion_transfer_learning.ipynb`: Iteraciones con **Transfer Learning** preentrenado en ImageNet utilizando los *backbones* **ResNet-50** y **DenseNet-121**.
* `05 - evaluacion_final_y_sesgos.ipynb`: Comparación cuantitativa entre iteraciones, matriz de confusión normalizada y auditoría de sesgos por metadatos EXIF y variables demográficas (sexo y edad).
* `06 - visualizacion_muestras_clases.ipynb`: Visualización clínica comparativa con ejemplos representativos de cada una de las 8 categorías diagnósticas.
* `ENTREGA1.PDF`: Documento técnico correspondiente a la primera entrega del proyecto.
* `INFORME_PROYECTO.PDF`: Informe científico ejecutivo final en formato IEEE.

---

## 💾 Obtención y Disponibilidad de los Datos

El conjunto de datos utilizado es **ODIR-5K** (*Ocular Disease Intelligent Recognition*), compuesto por 6.392 imágenes de fondo de ojo distribuidas en 8 clases (`N`, `D`, `G`, `C`, `A`, `H`, `M`, `O`).

### Cómo hacer disponibles los datos para ejecutar los cuadernos en Google Colab:
1. **Fuente original:** El dataset público puede descargarse desde la plataforma oficial de la competencia [ODIR-2019 Grand Challenge](https://www.kaggle.com/code/gpreda/ocular-disease-recognition-eda) o mediante su distribución estructurada con imágenes preprocesadas (`full_df.csv` y carpeta `preprocessed_images/`).
2. **Configuración en Google Drive:** Para reproducir directamente los cuadernos en Google Colab sin modificar las rutas:
   * Descarga o agrega la carpeta `BaseDatos` (que contiene `full_df.csv` y la subcarpeta `preprocessed_images/`) a la raíz de tu Google Drive (`MyDrive/BaseDatos`).
   * *(Opcional - Enlace de acceso directo a la carpeta estructurada: [Enlace a carpeta BaseDatos en Drive](https://drive.google.com/drive/folders/13MifQaSbUobyFUg_WrW0tJYTArZyXrtk?usp=drive_link)*.
3. **Ejecución en Colab:**
   * Abre cualquiera de los cuadernos `.ipynb` en Google Colab.
   * Activa la aceleración por hardware: **Entorno de ejecución $\rightarrow$ Cambiar tipo de entorno de ejecución $\rightarrow$ T4 GPU**.
   * Ejecuta las celdas en orden secuencial (`01` $\rightarrow$ `02` $\rightarrow$ `03` $\rightarrow$ `04` $\rightarrow$ `05`). El Cuaderno `02` genera el archivo maestro `df_procesado_folds.csv` consumido por los modelos posteriores.

---

## 📊 Resumen de Resultados Principales

| Modelo / Estrategia | Accuracy Global | Precision Macro | Recall Macro | F1-Score Macro |
| :--- | :---: | :---: | :---: | :---: |
| **ResNet-18 (Desde Cero / Scratch)** | 0.3600 | 0.2500 | 0.3380 | 0.2464 |
| **ResNet-50 (Transfer Learning)** | 0.5000 | 0.4800 | 0.6218 | 0.5155 |
| **DenseNet-121 (Transfer Learning)** | **0.5600** | **0.5100** | **0.6499** | **0.5505** |
