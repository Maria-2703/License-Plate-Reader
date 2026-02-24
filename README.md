# 🚗 Mini-Proyecto de Computer Vision (OpenCV)  
## Lectura didáctica de una matrícula UK (amarilla) **sin OCR**

Este mini-proyecto implementa un **pipeline clásico de Computer Vision** para detectar y reconocer los caracteres de una matrícula trasera del Reino Unido (amarilla) **sin utilizar OCR ni modelos preentrenados**.

El objetivo es **didáctico**: combinar múltiples técnicas tradicionales de visión por computador para construir un sistema funcional paso a paso.

---

## 🎯 Objetivo

Construir un pipeline que combine varias técnicas clásicas de CV para:

- Detectar la región amarilla (matrícula)
- Limpiar la imagen con morfología
- Segmentar los caracteres
- Reconocerlos mediante *template matching*
- Devolver la predicción final

⚠️ No pretende ser un sistema robusto listo para producción.

---

## 🧠 Pipeline Implementado

El flujo completo del sistema es:

1. **Carga de imagen**
   - Desde archivo local o URL
   - Conversión a formato adecuado (BGR/RGB)

2. **Normalización y redimensionado**
   - Conversión de valores de píxel
   - Preparación para K-Means

3. **Segmentación por color (K-Means)**
   - Agrupación de píxeles en *k clusters*
   - Selección del cluster más cercano al amarillo
   - Creación de máscara binaria

4. **Binarización y limpieza**
   - Conversión a escala de grises
   - Threshold binario
   - Aplicación de morfología (erode/dilate)

5. **Localización de la matrícula**
   - Bounding box sobre píxeles no negros
   - Recorte automático

6. **Segmentación de caracteres**
   - Proyección vertical (suma de columnas)
   - Detección de regiones con píxeles activos

7. **Reconocimiento por plantillas**
   - Generación de templates con `cv2.putText`
   - Comparación con `cv2.matchTemplate`
   - Selección por mayor correlación

8. **Predicción final**
   - Concatenación de caracteres reconocidos

---

## 🛠️ Tecnologías Utilizadas

- OpenCV
- NumPy
- Matplotlib
- Requests (opcional, para cargar imágenes desde URL)