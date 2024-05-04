# Pipeline de Datos en Google Cloud Platform

Este repositorio contiene la descripción y la implementación de un pipeline de datos desarrollado en Google Cloud Platform (GCP). El objetivo principal de este pipeline es facilitar la ingesta, procesamiento y análisis de datos de manera eficiente y escalable.

## Descripción del Pipeline

### 0. Sistema operativo y coneccion con GCP
Todo inicia en una funcion hecha con Python 3.12.3 subiendo un archivo a Cloud Storage para detonar el pipeline, esta union a GCP fue hecha con Google Cli que fue configurado en Debian 12.5


#### El pipeline sigue un flujo de trabajo desde el almacenamiento en la nube hasta la visualización y análisis de datos. Está compuesto por los siguientes componentes principales:
### 1. Cloud Storage

El proceso comienza con el almacenamiento de datos en Google Cloud Storage (GCS). Aquí se almacenan diversos tipos de datos en formato bruto, como archivos CSV, JSON, o parquet, entre otros. Este almacenamiento proporciona escalabilidad, durabilidad y acceso rápido a los datos.
### 2. Cloud Functions

Una vez que se cargan nuevos datos en Cloud Storage, se activa una Cloud Function en respuesta a un evento de inserción de archivos. Esta función sirve como un disparador que inicia el proceso de procesamiento de datos. Su función principal es ejecutar un script que procesa y transforma los datos según las necesidades del negocio.
### 3. Cloud SQL (PostgreSQL 15)

Los datos procesados se insertan en una base de datos relacional en Cloud SQL. En este caso, utilizamos PostgreSQL 15 como el motor de base de datos. Cloud SQL ofrece alta disponibilidad, seguridad y escalabilidad automática, lo que lo hace ideal para almacenar datos estructurados.
### 4. BigQuery

Además de almacenar los datos en Cloud SQL, también se carga una copia de los datos procesados en BigQuery. BigQuery es un servicio de almacenamiento de datos y análisis de Google Cloud que permite ejecutar consultas SQL rápidas sobre grandes conjuntos de datos. Esto facilita el análisis de datos a gran escala y la generación de insights.
### 5. Consulta desde Databricks

Los datos almacenados en Cloud SQL se pueden consultar y analizar directamente desde Databricks. Databricks es una plataforma de análisis y procesamiento de datos en la nube que ofrece un entorno colaborativo para ejecutar código PySpark, SQL y otros tipos de análisis avanzados.
### 6. Visualización en Power BI y Excel

Finalmente, los datos procesados también se pueden visualizar y analizar en herramientas de Business Intelligence como Power BI y Excel. Estas herramientas permiten crear informes interactivos, paneles de control y visualizaciones personalizadas para ayudar a tomar decisiones informadas basadas en los datos.

#### Arquitectura del Pipeline

El siguiente diagrama ilustra la arquitectura del pipeline:

[![read.png](https://i.postimg.cc/h46wrmDT/read.png)](https://postimg.cc/XXKQNpyY)

## Video del Funcionamiento del pipeline de GCP

https://youtu.be/qiM0WIaLKiY?si=8y_mE9sBzK-4xd6a

[![Comprehensive Markdown Crash Course](https://i.postimg.cc/RFjRcc70/Sin-t-tulo-2.png)](https://youtu.be/qiM0WIaLKiY?si=8y_mE9sBzK-4xd6a "Pipeline Daniel")
