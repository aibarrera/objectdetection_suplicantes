# Detección de *Suplicantes* con YOLOv11
Fine‑tuning e inferencia de YOLOv11 sobre un corpus propio.
Trabajo realizado junto a Franco A. en contexto educativo tecnicatura en ciencia de datos (ISTEA)

## Descripción del objeto y motivación
El objeto a detectar es la escultura precolombina **“Suplicantes”** de la cultura Condorhuasi. Puede presentar variaciones en su ejecución, ya que representaban diferentes aspectos en esa cultura, pero luego de analizar se estableció que la misma forma escultórica conserva una estructura singular ("rostro" hacia arriba y volumen prismático). Por su morfología consistente en diferentes variantes y tomas (ángulos, colores, fondos, incluso desde arriba donde se aprecia el gesto suplicante), resulta un buen candidato para que el modelo lo incorpore como **clase nueva**. El modelo logró identificar correctamente **imágenes nunca vistas** con puntuaciones cercanas a **0.92** y hasta detectó una figura muy desenfocada de fondo con **0.85**.  

## Modelo
Se utilizó **YOLOv11** (Ultralytics) y, para el fine‑tuning, el tamaño **nano (yolo11n)** por su bajo costo computacional. YOLOv11m alcanza mAP superior a YOLOv8m usando ~22% menos parámetros, y la familia abarca desde 2.6M hasta 56.9M de parámetros (mAP 39.5–54.7 en COCO), pero en este TP trabajamos con **yolo11n** por rapidez de entrenamiento e inferencia.  

## Dataset
- Corpus creado y etiquetado en **Roboflow** con una única clase: `suplicante`.
- 28 imágenes originales + **aumentación** → **68 imágenes** totales.  
- Split: **train 88% (60)**, **val 7% (5)**, **test 4% (3)**.  
- Aumentaciones aplicadas: *resize*, modificación de *hue*, *saturation*, *crop*, *exposure*, *noise*, *perspective*.  

## Entrenamiento
- Se probó entrenamiento con **200** y con **1000 épocas**.  
- Optimizador: **AdamW** (selección automática).  
- Tamaño de imagen: **640**.  
- Logging y artefactos en `runs/detect/train*/`.  

## Resultados
- Métricas de validación y gráficas disponibles en `runs/detect/train*/results.png`, curvas P/R/F1 y matriz de confusión.  
- Inferencia en **test** (no visto): resultados guardados en `runs/detect/predict*`.  
- Ejemplos mostraron detecciones correctas de la clase `suplicantes` en nuevas imágenes.

## Licencia
Este dataset solo puede ser utilizado de manera académica y para investigación. Licencia libre de uso.
Todas las imágenes utilizadas pertenecen a sus autores y no fueron utilizadas con fines de lucro.

### Créditos
- Ultralytics YOLOv11.
- Roboflow para dataset y aumentación.
- Autores de las fotografías que se utilizaron para entrenar el modelo.
