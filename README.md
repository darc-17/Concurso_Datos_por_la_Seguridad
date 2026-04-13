# Victimización y percepción de seguridad empresarial en corredores de obra urbana

![Python](https://img.shields.io/badge/Python-3.11-3776AB?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-2.x-150458?logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.3-F7931E?logo=scikit-learn&logoColor=white)
![statsmodels](https://img.shields.io/badge/statsmodels-0.14-4EACD8?logoColor=white)
![geopandas](https://img.shields.io/badge/geopandas-0.13-139C5A?logoColor=white)

> Proyecto **finalista** del DATAJAM Datos por la Seguridad 2026 — Cámara de Comercio de Bogotá.  
> Reto 2: Seguridad y Obras Públicas · Pitch ante jueces: 25 de abril de 2026.

---

## Problema

Las obras de transporte público en Bogotá —Primera Línea del Metro y corredor Calle 13— transforman la dinámica de seguridad de los establecimientos comerciales aledaños. Este proyecto analiza cómo las condiciones del entorno construido se asocian con la victimización y la percepción de deterioro en seguridad empresarial, y si estas relaciones varían por tramo y tipo de empresa.

---

## Datos

| Fuente | Descripción | Período |
|--------|-------------|---------|
| Encuesta de Corredores Estratégicos (ECE) | 2 021 establecimientos · 19 tramos de obra · 312 variables | 2024 |
| Encuesta de Percepción y Victimización (EPV) | Percepción ciudadana, Bogotá y Cundinamarca | 2021–2025 |
| Encuesta de Clima de Negocios (ECN) | Módulo de riesgos empresariales | 2020–2024 |
| Datos espaciales | GIS Catastro Bogotá · cobertura TransMilenio / Metro | 2024 |

Todas las fuentes son propiedad de la Cámara de Comercio de Bogotá y no están incluidas en este repositorio.

---

## Metodología

1. **Limpieza y EDA** — tratamiento de valores nulos (4 % de observaciones removidas), análisis descriptivo por corredor y tamaño de empresa (`pandas`, `seaborn`, `plotly`).
2. **Regresión Logit** — cuatro especificaciones por variable dependiente (*percepción de deterioro* y *victimización*), con y sin efectos fijos de tramo. Errores estándar HC1. Métricas reportadas: Odds Ratios con IC 95 %, test VIF para multicolinealidad (`statsmodels`).
3. **Modelo de Probabilidad Lineal (OLS)** — efectos marginales en puntos porcentuales para interpretabilidad directa (`statsmodels`, `linearmodels`).
4. **PCA + K-Means** — reducción a 10 componentes principales (87,4 % de varianza explicada); segmentación en *k = 3* clústeres seleccionados por Silhouette Score (0,1693), Davies-Bouldin (1,5749) y Calinski-Harabasz (`scikit-learn`).
5. **Análisis espacial** — mapas georreferenciados de perfiles de riesgo por tramo (`geopandas`, `folium`, `contextily`).

---

## Hallazgos principales

- **Entorno urbano como predictor clave:** la presencia de habitantes de calle duplica la probabilidad de percibir deterioro en seguridad (OR = 2,03); la satisfacción con el entorno la reduce a la mitad (OR = 0,51).
- **Efecto de victimización:** haber sido víctima de un delito incrementa la probabilidad de percibir empeoramiento en +14 puntos porcentuales (OR = 1,82).
- **Heterogeneidad espacial:** el Tramo 16 registra una probabilidad de inseguridad 4,56 veces mayor que el Tramo 1 — lo que invalida intervenciones homogéneas en el corredor.
- **Hipótesis refutada:** el tamaño de empresa no explica significativamente la percepción de seguridad; la victimización afecta tanto a micro como a grandes empresas.
- **Tres perfiles de clúster:** *Zona Estable* (alta satisfacción, baja victimización), *Zona Crítica* (victimización 90 %, deterioro percibido 68 %) y *Zona Corporativa* (empresas grandes, alta victimización objetiva con percepción normalizada).

---

## Estructura del repositorio

```
├── Código Anádima.ipynb            # Análisis completo: EDA, modelos, clustering, mapas
├── Informe Final Data Anádima.pdf  # Documento de hallazgos y recomendaciones de política
├── requirements.txt                # Dependencias del entorno Python
├── Reglamento.pdf                  # Bases del DATAJAM 2026
└── visualizaciones/                # 15 gráficos exportados (PNG)
```

---

## Cómo ejecutar el proyecto

```bash
# 1. Clonar el repositorio
git clone https://github.com/<usuario>/Concurso_Datos_por_la_Seguridad.git
cd Concurso_Datos_por_la_Seguridad

# 2. Crear entorno e instalar dependencias
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt

# 3. Abrir el notebook
jupyter notebook "Código Anádima.ipynb"
```

> **Nota:** Los datos originales (ECE, EPV, ECN) son propiedad de la Cámara de Comercio de Bogotá y no están incluidos en este repositorio. El notebook requiere acceso a los archivos de datos para ejecutarse completamente.

---

*Equipo Data Anádima — Ana Sofia Sánchez, David Rodríguez, Michelt Guarin · Tutor: Santiago Neira · Universidad de los Andes · 2026.*
