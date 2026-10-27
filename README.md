![Banner](imagenes/MRI.png)

# Laboratorio de Imágenes - Magíster en Física Médica UC

Este repositorio contiene el material, guías de laboratorio e itinerario para las sesiones prácticas del curso de **Laboratorio de Imágenes**, dictado en el **Magíster en Física Médica de la Pontificia Universidad Católica de Chile (UC)**. El diseño curricular y el desarrollo de los entornos computacionales han sido creados por **Pamela Franco**.

El curso está orientado a estudiantes de posgrado en física médica y disciplinas afines, abordando el procesamiento, la reconstrucción, la caracterización microestructural y el análisis computacional de imágenes médicas (con énfasis en Resonancia Magnética) desde una perspectiva formal, física y cuantitativa en Python.

---

## Acceso Directo a los Laboratorios (Google Colab)

Haz clic en los botones de la tabla para abrir directamente los cuadernos interactivos en Google Colab:

| Clase / Laboratorio | Botón de Acceso |
| :--- | :--- |
| **Práctico 1:** Registro de Imágenes Médicas y Fusión Multimodal (`registration.ipynb`) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pamelaFranco/Laboratorio-Imagenes/blob/main/codigos/registration.ipynb) |
| **Práctico 2:** Segmentación Anatómica y Funcional (`segmentation.ipynb`) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pamelaFranco/Laboratorio-Imagenes/blob/main/codigos/segmentation.ipynb) |

---

## Estructura Teórica y Contenidos del Curso

El programa abarca segmentación y registro en MRI:


## 1. Registro de Imágenes Médicas y Fusión Multimodal
- **Modelado geométrico y coordenadas físicas:** Uso de matrices homogéneas afines de $4 \times 4$ ($SFORM/QFORM$) para mapear el espacio discreto de vóxeles $(i, j, k)$ al espacio físico contiguo en milímetros $(x, y, z)$ según convenciones anatómicas como RAS o LPS.
- **Parámetros de adquisición e interpolación:** Integración de secuencias anatómicas isotrópicas de alta resolución (T1 FSPGR 3D de $0.94 \times 0.94 \times 1.20\text{ mm}^3$) con secuencias de difusión (DTI EPI con 25 direcciones no colineales y $b = 1000\text{ s/mm}^2$) mediante re-muestreo por interpolación (`nilearn.image.resample_to_img`) a vóxeles de $2 \times 2 \times 2\text{ mm}^3$.
- **Transformaciones espaciales rígidas y afines:** Corrección del movimiento del paciente mediante matrices rígidas de 6 grados de libertad (rotaciones compuestas $R = R_z(\gamma) R_y(\beta) R_x(\alpha)$ y vector de traslación $T$) y transformaciones afines de 12 grados de libertad para ajustar escalado y cizallamiento (*shear*).
- **Corrección de distorsión EPI y referencia anatómica:** Corrección de artefactos por susceptibilidad magnética en interfaces aire-hueso de secuencias EPI utilizando el volumen T1 FSPGR como referencia anatómica (*Gold Standard*) y alineando sobre la Comisura Anterior (AC) como origen coordenado.
- **Control de calidad visual y evaluación de alineación:** Validación del registro multimodal mediante superposición de bordes (`add_edges`) y visualización en damero (*checkerboard*) entre los mapas de Fracción de Anisotropía (FA) y la imagen T1 con contraste.

## 2. Segmentación Anatómica y Caracterización Tisular
- **Caracterización clínica de sustancia blanca:** Fusión de mapas DTI (FA) sobre anatomía T1 para clasificar el compromiso tumoral en gliomas en tres patrones clínicos: desplazamiento de tractos, edema vasogénico e infiltración/destrucción de fibras.
- **Procesamiento mediante umbralización adaptativa:** Aplicación de algoritmos de umbralización (Otsu) y filtrado morfológico para la separación de tejidos blandos y estructuras vasculares.
- **Detección de fronteras y segmentación por *Watershed*:** Uso de la Transformada de Distancia Euclidiana (EDT) combinada con el algoritmo de cuenca hidrográfica (*watershed*) para la delimitación precisa de contornos tisulares complejos.

---

## Requisitos e Instalación Local

Para ejecutar los cuadernos de manera local en tu equipo, clona el repositorio e instala las dependencias necesarias:

```bash
git clone [https://github.com/pamelaFranco/Laboratorio-Imagenes.git](https://github.com/pamelaFranco/Laboratorio-Imagenes.git)
cd Laboratorio-Imagenes/codigos
pip install numpy scipy matplotlib opencv-python pydicom SimpleITK pyradiomics torch torchvision
```

---

## License

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)