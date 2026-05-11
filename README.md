# Análisis Multidimensional de Impacto Ambiental: Sector Manufacturing (ecoinvent)

Este repositorio contiene el desarrollo y los resultados de un análisis multidimensional avanzado aplicado a los procesos de la carpeta de "Manufacturing" (Manufactura) de la base de datos ecoinvent. El objetivo es visualizar y categorizar la similitud entre diferentes procesos industriales basándose en sus perfiles de impacto ambiental.

## Descripción del Proyecto

El análisis aborda la complejidad de los datos de Inventario de Ciclo de Vida (LCA) mediante técnicas de aprendizaje no supervisado. Dado que un proceso de manufactura puede evaluarse a través de decenas de categorías de impacto ambiental, la visualización directa es imposible. Este proyecto utiliza una combinación de PCA (Análisis de Componentes Principales) y t-SNE (t-distributed Stochastic Neighbor Embedding) para reducir la dimensionalidad y facilitar la interpretación de los datos.

## Metodología

### 1. Fuente de Datos
Los datos fueron extraídos de la base de datos ecoinvent, específicamente de la sección de procesos de manufactura. Estos procesos incluyen desde la producción de componentes electrónicos hasta el mecanizado de metales y ensamblaje de maquinaria.

### 2. Método de Evaluación de Impacto (LCIA)
Se aplicó el método **ReCiPe Midpoint (H)**. 
- **Nivel Midpoint:** Proporciona un mayor detalle analítico al evaluar impactos en etapas tempranas de la cadena de causalidad (ej. cambio climático, toxicidad humana, formación de material particulado).
- **Perspectiva Hierarchist (H):** Basada en el consenso científico y periodos de tiempo estándar (ej. 100 años para el potencial de calentamiento global).

### 3. Técnicas de Reducción de Dimensionalidad
Para procesar las múltiples dimensiones de ReCiPe Midpoint, se ejecutó un flujo de trabajo en dos etapas:

- **PCA (Principal Component Analysis):** Utilizado inicialmente para reducir el ruido y retener la mayor parte de la varianza de los datos. Esto permite simplificar la estructura de correlación entre categorías de impacto que suelen estar vinculadas (como el consumo de energía y las emisiones de CO2).
- **t-SNE (t-distributed Stochastic Neighbor Embedding):** Aplicado sobre los componentes principales para proyectar los datos en un plano bidimensional. A diferencia de PCA, t-SNE es una técnica no lineal que sobresale en la conservación de la estructura local, permitiendo que procesos con perfiles de impacto muy similares se agrupen visualmente en "clusters".

## Interpretación de la Visualización

El gráfico generado (t-SNE Dimensión 1 vs Dimensión 2) revela la formación de distintos grupos representados por colores:

- **Clusters de Color:** Cada grupo de puntos representa procesos que comparten una "firma ambiental" similar. Por ejemplo, procesos intensivos en químicos tienden a agruparse lejos de procesos puramente mecánicos.
- **Centroides (Estrellas):** Las estrellas en el gráfico marcan los puntos representativos o centros de gravedad de cada cluster identificado. Estos sirven para identificar el perfil promedio de impacto de esa familia de procesos.
- **Similitud Global:** La cercanía entre puntos en el mapa indica que, tras considerar todas las categorías de impacto de ReCiPe Midpoint H, dichos procesos tienen comportamientos ambientales análogos.

## Aplicaciones

- **Identificación de Outliers:** Detección de procesos con impactos inusualmente altos o bajos dentro de su categoría.
- **Simplificación de Inventarios:** Posibilidad de utilizar procesos "proxy" para representar grupos de manufactura similares.
- **Análisis Comparativo:** Evaluación rápida de cómo se posiciona un nuevo proceso frente a los estándares de la industria en ecoinvent.

## Requisitos Técnicos

Para replicar este análisis, se requiere el uso de librerías de análisis de datos como:
- Python (Pandas, Scikit-learn) 
- Acceso a la base de datos ecoinvent.
- Software de evaluación de ciclo de vida (OpenLCA y herramientas personalizadas en Python).
