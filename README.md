![Banner](imagenes/MRI.png)

# Laboratorio de Imágenes - Magíster en Física Médica UC

Este repositorio contiene el material, guías de laboratorio e itinerario para las sesiones prácticas del curso de **Laboratorio de Imágenes**, dictado en el **Magíster en Física Médica de la Pontificia Universidad Católica de Chile (UC)**. El diseño curricular y el desarrollo de los entornos computacionales han sido creados por **Pamela Franco**.

El curso está orientado a estudiantes de posgrado en física médica y disciplinas afines, abordando el procesamiento, la reconstrucción, la caracterización microestructural y el análisis computacional de imágenes médicas (con énfasis en Resonancia Magnética) desde una perspectiva formal, física y cuantitativa en Python.

---

## Acceso Directo a los Laboratorios (Google Colab)

Haz clic en los botones de la tabla para abrir directamente los cuadernos interactivos en Google Colab:

| Clase / Laboratorio | Botón de Acceso |
| :--- | :--- |
| **Práctico 1:** Adquisición y Reconstrucción en el Espacio $k$ (`EspacioK.ipynb`) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pamelaFranco/Laboratorio-Imagenes/blob/main/codigos/EspacioK.ipynb) |
| **Práctico 2:** Simulación de Secuencias de Resonancia Magnética (`simulador_secuencias.ipynb`) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pamelaFranco/Laboratorio-Imagenes/blob/main/codigos/simulador_secuencias.ipynb) |
| **Práctico 3:** Registro de Imágenes Médicas y Fusión Multimodal (`registration.ipynb`) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pamelaFranco/Laboratorio-Imagenes/blob/main/codigos/registration.ipynb) |
| **Práctico 4:** Segmentación Anatómica y Funcional (`segmentation.ipynb`) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pamelaFranco/Laboratorio-Imagenes/blob/main/codigos/segmentation.ipynb) |
| **Práctico 5:** Imágenes de Tensores de Difusión y Mapas Cuantitativos (`DTI_mapas_difusion.ipynb`) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pamelaFranco/Laboratorio-Imagenes/blob/main/codigos/DTI_mapas_difusion.ipynb) |
| **Práctico 6:** Extracción de Características Radiómicas (`radiomics.ipynb`) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pamelaFranco/Laboratorio-Imagenes/blob/main/codigos/radiomics.ipynb) |
| **Práctico 7:** Clasificación y Diagnóstico Avanzado de Gliomas (`Glioma_classification.ipynb`) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pamelaFranco/Laboratorio-Imagenes/blob/main/codigos/Glioma_classification.ipynb) |

---

## Estructura Teórica y Contenidos del Curso

El programa abarca desde la física fundamental de formación de imágenes en Resonancia Magnética (RM) hasta técnicas de inteligencia artificial y radiómica aplicadas al diagnóstico neuro-oncológico:

### 1. Reconstrucción y Muestreo en el Espacio $k$
- Mapeo de la señal RMN mediante gradientes de campo magnético.
- Dominio de frecuencias espaciales y Transformada de Fourier 2D.
- Submuestreo, artefactos de *aliasing*, filtrado de frecuencias y reconstrucción de imágenes.

### 2. Simulación de Secuencias de Resonancia Magnética
- Modelamiento matemático de los tiempos de relajación tisular ($T_1$, $T_2$ y $T_2^*$).
- Ecuaciones de Bloch para secuencias clásicas (*Spin Echo*, *Gradient Echo*).
- Manipulación de tiempo de repetición ($\text{TR}$), tiempo de eco ($\text{TE}$) y ángulo de inclinación (*flip angle*) para generación de contraste tisular.

### 3. Registro de Imágenes Médicas y Fusión Multimodal
- Matrices de transformación espacial ($SFORM/QFORM$), coordenadas físicas y re-muestreo por interpolación.
- Evaluación de algoritmos de alineación rígidos, afines y difeomórficos no lineales (**SyN**).
- Corrección de distorsiones por susceptibilidad magnética (EPI) y fusión limpia T1 vs DTI (FA) para preservación anatómica.

### 4. Segmentación Anatómica y Funcional
- Algoritmos de umbralización adaptativa (Otsu) y filtrado morfológico.
- Transformada de Distancia Euclidiana (EDT) y segmentación por *Watershed*.
- Separación de estructuras vasculares y de tejidos blandos en imágenes médicas.

### 5. Tensores de Difusión (DTI) y Microestructura
- Física del movimiento browniano de moléculas de agua en tejidos biológicos.
- Estimación del tensor de difusión a partir de gradientes de codificación.
- Cálculo de métricas cuantitativas microestructurales: Anisotropía Fraccionada ($\text{FA}$), Difusividad Media ($\text{MD}$), Axial ($\text{AD}$) y Radial ($\text{RD}$).

### 6. Radiómica y Biomarcadores Cuantitativos
- Extracción de características fenotípicas de alto rendimiento a partir de regiones de interés (ROI).
- Descriptores de forma, intensidad de primer orden y matrices de textura de segundo orden ($\text{GLCM}$, $\text{GLRLM}$, $\text{GLSZM}$).
- Estandarización de características radiómicas para análisis de soporte a la decisión clínica.

### 7. Aprendizaje Profundo y Clasificación Neuro-Oncológica (Gliomas)
- Procesamiento de imágenes volumétricas multimodales (T1, T1-CE, T2, FLAIR).
- Clasificación de tumores cerebrales (gliomas de alto y bajo grado) mediante arquitecturas avanzadas de Deep Learning.
- Evaluación del rendimiento mediante métricas de validación clínica ($\text{Accuracy}$, $\text{AUC-ROC}$, $\text{F1-score}$).


## Requisitos e Instalación Local

Para ejecutar los cuadernos de manera local en tu equipo, clona el repositorio e instala las dependencias necesarias:

```bash
git clone [https://github.com/pamelaFranco/Laboratorio-Imagenes.git](https://github.com/pamelaFranco/Laboratorio-Imagenes.git)
cd Laboratorio-Imagenes/codigos
pip install numpy scipy matplotlib opencv-python pydicom SimpleITK pyradiomics torch torchvision
```


> **Nota:** Para los cuadernos de DTI, Radiómica y Clasificación de Gliomas, se recomienda el uso de Google Colab con aceleración por GPU.
---

## License

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)