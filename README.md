# 🌳 Proyecto de Machine Learning No Supervisado: Deforestación en Argentina (2001–2020)  
**Grupo 11**

### Integrantes:
- Cruz Nicole  
- Ulloa Melina  

---

## 1. 📘 Introducción

La deforestación es uno de los principales desafíos ambientales en Argentina. El avance sobre bosques nativos genera pérdida de biodiversidad, contribuye al cambio climático y pone en riesgo a comunidades locales.

En este trabajo, aplicamos **aprendizaje automático no supervisado** para detectar **agrupamientos (clusters)** de regiones argentinas con comportamientos similares de deforestación entre los años **2001 y 2020**. 

A diferencia del aprendizaje supervisado, en este caso **no se usan etiquetas previas**, sino que se dejan que los datos se agrupen naturalmente en función de sus características.

El objetivo fue encontrar patrones ocultos que ayuden a:

✅ Identificar zonas con alta, media o baja deforestación  
✅ Analizar comportamientos comunes entre provincias  
✅ Aportar evidencia útil para políticas públicas y conservación  

---

## 2. 📊 Dataset utilizado

### 2.1 Fuente de datos

El dataset fue obtenido desde la plataforma [**Trase**](https://trase.earth/open-data/datasets/spatial-metrics-argentina-territorial-deforestation), una base abierta de datos ambientales.  
Se utilizó un archivo en formato `.csv` con información territorial y temporal sobre deforestación en Argentina.

### 2.2 Estructura del dataset original

- Filas: 2.381  
- Columnas principales:
  - year (año)
  - country (país)
  - region (departamento)
  - parent_region (provincia)
  - deforestation_hectares (hectáreas deforestadas)
  - Varias columnas con códigos territoriales (eliminadas por irrelevancia para el análisis)

---

## 3. 🔄 Metodología aplicada

### 3.1 Limpieza y preparación

- Eliminación de columnas innecesarias: se descartaron IDs que no aportaban valor analítico (códigos de país, provincia y región).
- Renombrado de columnas al español para facilitar la lectura.
- Verificación de datos nulos y duplicados: no se detectaron.
- Conversión de tipos de datos para asegurar compatibilidad con los modelos.

### 3.2 Agrupamiento de datos por provincia

Se construyó un nuevo dataset por **provincia**, calculando para cada una:

- `total_deforestation`: Total acumulado de hectáreas deforestadas (2001–2020)  
- `mean_deforestation`: Promedio anual de deforestación  
- `years_count`: Cantidad de años con datos registrados  

Estos valores resumen el comportamiento de cada región a lo largo del tiempo.

---

## 4. 🤖 Modelo de Clustering (No Supervisado)

### 4.1 Algoritmo seleccionado

Se aplicó el algoritmo **KMeans** con `n_clusters = 3`, luego de observar el gráfico del **método del codo** para elegir la cantidad óptima de grupos.

### 4.2 Normalización de datos

Los datos fueron **escalados** usando `StandardScaler` para evitar que las diferencias de magnitudes entre variables afecten el agrupamiento.

### 4.3 Aplicación del modelo

Cada provincia fue clasificada dentro de uno de los tres grupos (clusters) en función de su nivel y comportamiento de deforestación.

---

## 5. 📈 Visualización y análisis de los clusters

Se identificaron **tres clusters bien diferenciados**:

### 🔸 Cluster 0 — Bajo impacto  
- Promedio anual: ~899 hectáreas  
- Total: ~108.000 hectáreas  
- Años con datos: 714  
📌 Regiones con deforestación baja pero monitoreo constante.

### 🔸 Cluster 1 — Alto impacto sostenido  
- Promedio anual: ~4.435 hectáreas  
- Total: ~2.3 millones de hectáreas  
- Años con datos: 540  
📌 Zonas con deforestación severa y persistente. Probables casos: **Chaco, Santiago del Estero, Salta**.

### 🔸 Cluster 2 — Alto impacto pero con menor historial  
- Promedio anual: ~4.710 hectáreas  
- Total: ~1.15 millones de hectáreas  
- Años con datos: 293  
📌 Regiones con deforestación intensa pero menor registro histórico (monitoreo reciente o menos estable).

---

## 6. 📍 Hallazgos clave

- Las provincias del norte concentran la mayor parte de la deforestación acumulada.
- Existen diferencias claras entre regiones con alta intensidad reciente y otras con impacto constante a lo largo del tiempo.
- Las agrupaciones detectadas por el modelo permiten **enfocar acciones de mitigación** en función del perfil territorial.

---

## 7. 🌱 Conclusiones y posibles mejoras

Este trabajo demostró cómo el **aprendizaje no supervisado** puede detectar patrones significativos en problemas ambientales sin necesidad de etiquetas previas.

🧠 La creación de clusters aportó valor al identificar **tipos de comportamiento** frente a la deforestación:

- Regiones críticas con pérdida constante
- Regiones emergentes con impacto reciente
- Regiones con baja deforestación

📌 Posibles mejoras futuras:

- Incorporar variables climáticas o socioeconómicas  
- Usar modelos como DBSCAN o Agglomerative Clustering  
- Aplicar reducción de dimensionalidad (PCA) para mejorar visualización  
- Incluir imágenes satelitales (NDVI) o mapas  

