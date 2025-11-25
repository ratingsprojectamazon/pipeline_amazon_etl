# Pipeline ETL Amazon Electronics Reviews 2023

Este proyecto implementa un pipeline completo de ETL (Extract, Transform, Load) para procesar reseñas de productos electrónicos de Amazon del año 2023, utilizando Apache Spark y PySpark. El pipeline incluye desde la extracción de datos en formato JSON hasta la creación de modelos de machine learning para clasificación de sentimientos.

## 📋 Tabla de Contenidos

- [Descripción del Proyecto](#descripción-del-proyecto)
- [Arquitectura del Pipeline](#arquitectura-del-pipeline)
- [Estructura de Datos](#estructura-de-datos)
- [Instalación y Configuración](#instalación-y-configuración)
- [Uso del Pipeline](#uso-del-pipeline)
- [Capas del Data Lake](#capas-del-data-lake)
- [Modelo de Machine Learning](#modelo-de-machine-learning)
- [Resultados y Métricas](#resultados-y-métricas)

## 🎯 Descripción del Proyecto

Este pipeline ETL procesa aproximadamente **43.8 millones** de reseñas de productos electrónicos de Amazon, filtrando específicamente las del año 2023 (resultando en **1.9 millones** de registros). El objetivo principal es:

- Limpiar y estructurar los datos de reseñas
- Implementar detección de productos devueltos y sus causas
- Crear features para análisis de sentimientos
- Entrenar un modelo de clasificación binaria para predecir reseñas negativas vs positivas

## 🏗️ Arquitectura del Pipeline

El pipeline sigue una arquitectura de Data Lake con múltiples capas:

### Tecnologías Utilizadas

- **Apache Spark**: Motor de procesamiento distribuido
- **PySpark**: API de Python para Spark
- **HDFS**: Sistema de archivos distribuido
- **Parquet**: Formato de almacenamiento columnar
- **Spark ML**: Biblioteca de machine learning

## 📊 Estructura de Datos

### Schema Original
- asin: string (ID del producto)
- helpful_vote: long (votos útiles)
- images: array (imágenes del review)
- parent_asin: string (ASIN padre)
- rating: double (calificación 1-5)
- text: string (texto de la reseña)
- timestamp: long (timestamp Unix)
- title: string (título de la reseña)
- user_id: string (ID del usuario)
- verified_purchase: boolean (compra verificada)


## ⚙️ Instalación y Configuración

### Prerrequisitos

- Apache Spark 3.x
- Hadoop/HDFS configurado
- Python 3.7+
- PySpark
- Jupyter Notebook

### Configuración de Spark

```python
spark = (
    SparkSession.builder
    .appName("ETL_Amazon_Electronics_2023")
    .master("local[*]")
    .config("spark.sql.shuffle.partitions", "8")
    .config("spark.sql.files.maxPartitionBytes", str(128 * 1024 * 1024))
    .getOrCreate()
)
```
## Estructura de Directorios HDFS
```code
hdfs://localhost:9000/datalake/
├── landing/
│   └── Electronics.jsonl
├── bronze/
│   └── amazon/electronics/reviews/curated_2023/
├── silver/
│   └── amazon/electronics/reviews_clean_2023/
└── gold/
    ├── amazon/electronics/reviews_gold_features_2023/
    └── models/lr_reviews_2023_v1/
```
## 🚀 Uso del Pipeline

1. Ejecución del Pipeline Completo
El pipeline se ejecuta a través del notebook Jupyter ETL 2023 BIG DATA_2.ipynb:
```bash
jupyter notebook "ETL 2023 BIG DATA_2.ipynb"
```
