**Responsables**

- [Dr. Manuel Guerrero Salinas](https://investigadores.uaslp.mx/InvestigadorProfile/EC8AAA%3D%3D)
- [Dra. Eréndida Cristina Mancilla González](https://investigadores.uaslp.mx/InvestigadorProfile/JC8AAA%3D%3D)


**Universidad Autónoma de San Luis Potosí
Laboratorio de Experimentación visual (LEM)**

<img src="/imagenes/logos.png" alt="" width="400">


## Estudios de Saliencia

Los estudios de saliencia se centran en identificar y resaltar las áreas de una imagen que captan más la atención visual, conocidas como regiones salientes. Estos estudios son fundamentales en campos como la visión por computadora, la compresión de imágenes, la segmentación y el reconocimiento de objetos, ya que ayudan a enfocar el procesamiento en las partes más relevantes de la imagen. La saliencia puede definirse a partir de distintas características visuales como el contraste de color, la orientación, la intensidad luminosa o diferencias texturales. Los algoritmos de saliencia buscan emular cómo el sistema visual humano detecta automáticamente los objetos y las áreas de interés en una escena compleja.



## Modelo Utilizado

En este caso, se utiliza el método de Histogram-based Contrast en conjunto con la técnica StaticSaliencySpectralResidual proporcionada por la biblioteca OpenCV. Este modelo se basa en el enfoque de saliencia espectral residual, que fue propuesto por Xiaodi Hou y Liqing Zhang en 2007.

**Descripción del Modelo**

El modelo StaticSaliencySpectralResidual analiza la imagen en el dominio de la frecuencia para detectar regiones salientes. El proceso implica:

1. Transformada de Fourier: Se aplica la Transformada de Fourier a la imagen para obtener su representación en el dominio de la frecuencia.
2. Cálculo del Residual Espectral: Se calcula el residuo del espectro logarítmico, es decir, la diferencia entre el espectro logarítmico original y un espectro logarítmico local suavizado. Este residuo resalta las irregularidades en el espectro que suelen corresponder a características salientes en la imagen.
3. Transformada Inversa: Se realiza la Transformada Inversa de Fourier sobre el residuo para volver al dominio espacial, generando así un mapa de saliencia que indica la probabilidad de que cada píxel pertenezca a una región saliente.
4. Normalización y Post-Procesamiento: El mapa resultante se normaliza y, opcionalmente, se puede aplicar un umbral u otros ajustes para mejorar la visualización del heatmap de saliencia.

El método Histogram-based Contrast se enfoca específicamente en comparar histogramas locales de intensidades para resaltar diferencias significativas que denoten saliencia.

**Parámetros del Modelo**

El modelo StaticSaliencySpectralResidual_create en OpenCV es una implementación estándar que no requiere especificar manualmente una gran cantidad de parámetros para su ejecución básica. Sin embargo, dentro del proceso de saliencia hay ciertos aspectos y parámetros intrínsecos:

1. Escalado y Normalización: Internamente, el modelo escala y normaliza el mapa de saliencia para convertir los valores flotantes en un rango adecuado (normalmente [0, 255]) para visualización.
2. Selección del Mapa de Saliencia: El parámetro success indica si la computación del mapa de saliencia fue exitosa. Aunque no se ajustan manualmente, es importante manejarlos en el código para confirmar que el proceso se completó correctamente.
3. Aplicación del Colormap: Se utiliza cv2.applyColorMap para generar un heatmap con distintos colores basados en los valores de saliencia. Aquí, se puede elegir entre varios mapas de colores (por ejemplo, COLORMAP_JET, COLORMAP_HOT, etc.) según la preferencia visual.
4. Ajuste del Tamaño de la Imagen: Previo al análisis, es posible ajustar el tamaño de la imagen para mejorar el rendimiento, aunque este parámetro no se especifica directamente en el modelo de saliencia, sino que se puede manejar antes de pasar la imagen al modelo.

---
## Instrucciones de Uso

**1. Preparación del Entorno:**

- Asegúrate de tener instalado OpenCV con los módulos contrib (opencv-contrib-python), junto con numpy y matplotlib.
- Utiliza !pip install opencv-contrib-python para instalar las dependencias necesarias.

**2. Carga de la Imagen:**

- Sube la imagen que deseas procesar. En Google Colab, usa la herramienta files.upload() para cargar la imagen deseada al entorno.
- Lee la imagen usando cv2.imread() asegurándote de que la imagen se cargó correctamente.

**3. Cálculo del Heatmap de Saliencia:**
- Crea el objeto de saliencia:

```
saliency = cv2.saliency.StaticSaliencySpectralResidual_create()
```

- Computa el mapa de saliencia:

```
(success, saliencyMap) = saliency.computeSaliency(image)
```

- Convierte y procesa el mapa para su visualización:

```
saliencyMap = (saliencyMap * 255).astype("uint8")
heatmap = cv2.applyColorMap(saliencyMap, cv2.COLORMAP_JET)
```

**4. Visualización:**

- Convierte la imagen original y el heatmap al espacio de color RGB para visualizarlos con Matplotlib.
Utiliza plt.subplots() para crear una figura con dos subplots: uno para la imagen original y otro para el heatmap.
-Añade títulos y una barra de color al heatmap para interpretar la intensidad de saliencia.
-Muestra la figura y, opcionalmente, guarda la imagen combinada.

**5. Salida y Descarga:**

- Después de ejecutar el script, verás la imagen original y el heatmap saliente lado a lado.
- El script puede guardar la figura combinada y ofrecer la opción de descargarla.

Estos pasos permiten aplicar y visualizar el análisis de saliencia en cualquier imagen, facilitando la comprensión de las áreas que captan mayor atención visual.

---

Puedes acceder al notebook aquí: [saliency_heatmap.ipynb](saliency_heatmap.ipynb)


---

## Ejemplos


![ejemplo1](images/original_y_heatmap_saliency1.png)
Fig. 1. Páginas 38 y 39 de la revista Matiz Gráfico del Diseño Internacional. Fuente: Matiz Gráfico del Diseño Internacional, 1997.

![ejemplo2](images/original_y_heatmap_saliency2.png)
Fig 2. Páginas 28 y 29 de la revista Matiz Gráfico del Diseño Internacional.
Fuente: Matiz Gráfico del Diseño Internacional, 1997.
