# Proyectos En GCP

- Pipeline usando Cloud Storage, Cloud Function, Cloud Sql "Postgres", BigQuery, Databricks, PowerBi y Excel
  
- Deploy de React NextJS en Kubernetes de GCP

-----------

## Pipeline de Datos en Google Cloud Platform

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

---------------------------------------------------------------------------------------------------------------------

# Deploy de app NextJS en Kubernetes

### Herramientas utilizadas 

- NextJs
- Kubernetes
- Docker
- Yaml


#### Introducción

Este documento proporciona una guía detallada sobre el despliegue de una aplicación web desarrollada con Next.js, una biblioteca de React, en Google Kubernetes Engine (GKE) de Google Cloud Platform (GCP). Además, se explicará el concepto de despliegue, Ingress, Service y Load Balancer en Kubernetes, junto con el uso de archivos YAML para configurar estos recursos en un clúster de Kubernetes.
Despliegue de una Aplicación en Kubernetes

El despliegue en Kubernetes se refiere al proceso de implementar y ejecutar aplicaciones en un clúster de Kubernetes. Utiliza contenedores Docker para empaquetar y distribuir aplicaciones, lo que proporciona una forma eficiente y escalable de gestionar aplicaciones en la nube.
Ingress y Service en Kubernetes

Ingress es un recurso de Kubernetes que gestiona el acceso externo a los servicios dentro de un clúster de Kubernetes. Actúa como una capa de entrada que puede enrutar el tráfico HTTP y HTTPS a los servicios basados en reglas de enrutamiento definidas.

Service es otro recurso de Kubernetes que define un conjunto lógico de pods y una política de acceso a ellos. Proporciona una dirección IP y un puerto estables a través de los cuales otros servicios pueden acceder a los pods que conforman el servicio.
Load Balancer en Kubernetes

Un Load Balancer en Kubernetes es un tipo de Service que expone un servicio a través de un balanceador de carga externo que se encuentra fuera del clúster de Kubernetes. Distribuye el tráfico de red entre varios pods de un servicio para mejorar la disponibilidad y la escalabilidad.
Archivos YAML para Despliegue

En Kubernetes, la configuración se define en archivos YAML. Por lo general, se utilizan dos archivos YAML para configurar un despliegue completo: uno para definir los pods, los servicios y otros recursos, y otro para configurar el Ingress y el Load Balancer.


### Ejemplo de Archivos YAML

El siguiente es un ejemplo simplificado de dos archivos YAML utilizados para desplegar una aplicación en Kubernetes:

#### deployment.yaml: Define los pods y los servicios de la aplicación.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nextjs-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nextjs
  template:
    metadata:
      labels:
        app: nextjs
    spec:
      containers:
      - name: nextjs-container
        image: your-nextjs-image
        ports:
        - containerPort: 3000
---
apiVersion: v1
kind: Service
metadata:
  name: nextjs-service
spec:
  selector:
    app: nextjs
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3000
  type: ClusterIP
```

  ####  ingress.yaml: Define el Ingress y el Load Balancer.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nextjs-ingress
  annotations:
    kubernetes.io/ingress.class: "gce"
spec:
  rules:
  - http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: nextjs-service
            port:
              number: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nextjs-lb-service
spec:
  selector:
    app: nextjs
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
```

Con esta guía y los archivos YAML proporcionados, podrás desplegar tu aplicación de Next.js en Kubernetes de GCP de manera eficiente y escalable, aprovechando al máximo los recursos y las características de la plataforma Kubernetes.


### Video del Deployment en KUBERNETES DE GCP

[![gcp.png](https://i.postimg.cc/qvq7sXNS/gcp.png)](https://youtu.be/1uc4LFeJbdc?si=LnZzNLBJ7-gFbcJu)
