# Computer_Vision_Neuronal_Network_Refrigerators
Este proyecto implementa un pipeline de extremo a extremo, utilizando arquitecturas de vanguardia como YOLOv11 y procesamiento distribuido en Databricks, para extraer, procesar y analizar miles de imágenes e identificar productos, niveles de llenado en puntos de ventas.



Sistema Inteligente de Auditoría de Activos: Detección y Análisis de Inventario en Neveras
📋 Descripción del Proyecto
Este proyecto implementa un pipeline de extremo a extremo (End-to-End) diseñado para automatizar la auditoría visual de activos (neveras y botellas) en puntos de venta. Utilizando arquitecturas de vanguardia como YOLOv11 y procesamiento distribuido en Databricks, el sistema es capaz de extraer, procesar y analizar miles de imágenes para identificar productos, niveles de llenado y cumplimiento de planogramas.

🛠️ Stack Tecnológico
Entorno de Ejecución: Databricks (Spark Runtime).

Lenguajes: Python, PySpark.

Visión Artificial: YOLOv11s (Ultralytics), OpenCV, TensorFlow.

Procesamiento de Datos: Pandas, SQL (Spark SQL).

Infraestructura: Google Cloud Storage (Ingesta de imágenes).

🏗️ Arquitectura del Pipeline
1. Extracción de Datos y Descarga Paralela
El proceso comienza con la ingesta de metadatos desde archivos Excel/Delta tables. Para optimizar el tiempo de descarga, se implementó un sistema de ThreadPoolExecutor con 32 hilos concurrentes, permitiendo la descarga masiva de imágenes desde buckets de almacenamiento hacia el sistema de archivos local del clúster.

2. Detección de Objetos con YOLOv11s
Se utiliza la versión YOLOv11 Small (Yv11s) para equilibrar la precisión y la velocidad de inferencia. El modelo está configurado para:

Identificar activos (neveras) y su contenido (botellas).

Generar cajas delimitadoras (Bounding Boxes) con métricas de confianza.

Extraer coordenadas (x1, y1, x2, y2) para análisis espacial posterior.

3. Análisis Avanzado de Imágenes
Tras la detección, el sistema realiza un post-procesamiento que incluye:

Cálculo de Color Promedio (RGB): Análisis cromático de las detecciones para clasificación secundaria o identificación de marcas.

Clasificación de Inventario: Uso de modelos CNN complementarios para distinguir tipos de botellas y skus específicos.

Consolidación en DataFrames: Los resultados se estructuran en tablas finales que incluyen la llave del activo, clase detectada, nivel de confianza y promedio RGB.

🚀 Características Principales
Escalabilidad: Diseñado para ejecutarse en clústeres de Databricks, permitiendo procesar volúmenes masivos de imágenes mediante Spark.

Robustez: Manejo de errores durante la descarga y logs detallados de ejecución.

Precisión: Implementación de la última versión de YOLO (v11) para una detección superior en condiciones de iluminación variables dentro de locales comerciales.

📊 Visualización de Resultados
El proyecto genera un DataFrame final listo para ser consumido por herramientas de BI (Power BI/Tableau), conteniendo:

Conteo de botellas por activo.

Nivel de confianza de la detección.

Análisis de color dominante por detección.

Cómo usar este repositorio
Configuración de Databricks: Importar los notebooks en un workspace de Databricks.

Instalación de Dependencias: Ejecutar las celdas de %pip install para configurar ultralytics, opencv-python-headless y tensorflow.

Ejecución del Pipeline:

Extracción Imágenes.ipynb: Para la descarga masiva.

CNN Neveras - Yv11s.ipynb: Para la inferencia y análisis de objetos.





Copyright & License: All rights reserved. This code is for portfolio demonstration purposes only. Redistribution or commercial use is strictly prohibited.
