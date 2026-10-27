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

El proceso de segmentación en imágenes de Phase Contrast (PC) permite delimitar la geometría aórtica y separar las estructuras anatómicas del tejido circundante. La segmentación opera sobre dos dominios de entrada según el objetivo del análisis:

* **Magnitud Anatómica (`abs(s)`):** Trabaja con la intensidad de magnetización transversal ($|S|$). Permite delimitar la estructura real y la pared del vaso independientemente de la velocidad del flujo.
* **Fase Funcional / Velocidad (`|u|`):** Trabaja sobre el mapa de velocidades ($|u|$). Aísla exclusivamente el núcleo dinámico del flujo cancelando el tejido estático (subestimando el área aórtica cerca de la pared por efectos viscosos).

### Algoritmos de Segmentación Implementados

1. **Umbralización de Otsu (`threshold_otsu`)**
   * **Función:** Calcula automáticamente el umbral óptimo maximizando la varianza interclase del histograma de la imagen.
   * **Aplicación:** Separa el vaso aórtico hiperintenso del fondo en la imagen de magnitud, o define el nivel de corte de velocidad activa en la imagen de fase.

2. **Transformada de Distancia**
   * **Función:** Calcula la distancia euclidiana de cada píxel en primer plano respecto al borde binario más cercano.
   * **Aplicación:** Encuentra los máximos locales dentro del vaso para generar los puntos semilla (*seeds*) y marcadores internos indispensables para desacoplar el contorno aórtico.

3. **Algoritmo Watershed (Cuenca Hidrográfica)**
   * **Función:** Trata el gradiente de la imagen como una superficie topográfica e "inunda" la región desde las semillas previamente detectadas.
   * **Aplicación:** Separa la aorta de vasos adyacentes o estructuras contiguas que comparten niveles de gris o intensidades similares tras el umbralizado.

4. **Transformada de Hough (Detección de Círculos)**
   * **Función:** Transforma el espacio de bordes a un espacio paramétrico para detectar geometrías circulares u ovoides.
   * **Aplicación:** Inicializa o valida la posición del centroide y la estimación del radio aórtico antes de refinar los contornos finales.

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