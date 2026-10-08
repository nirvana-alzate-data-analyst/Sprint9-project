# Validando Hipótesis de Negocio con Pruebas Estadísticas en Experimento A/B

![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen.svg)

Este proyecto evalúa el impacto de una nueva versión de *landing page* (*Versión B*) sobre el comportamiento de compra de $40,000$ usuarios en una plataforma de e-commerce. A través de pruebas de hipótesis estadísticas (prueba $t$ de Welch, Z-test de proporciones y Chi-cuadrado $\chi^2$), el análisis determina si la nueva variante genera un incremento estadísticamente significativo en la tasa de conversión y en el gasto promedio por cliente.

---

## 📑 Tabla de Contenidos

* [📌 Resumen del Proyecto](#-resumen-del-proyecto)
* [📂 Origen de los Datos](#-origen-de-los-datos)
* [🛠️ Tecnologías y Librerías](#-tecnologías-y-librerías)
* [🌳 Estructura del Repositorio](#-estructura-del-repositorio)
* [⚙️ Instalación y Uso](#-instalación-y-uso)
* [📊 Resultados y Conclusiones](#-resultados-y-conclusiones)
* [👤 Autor y Licencia](#-autor-y-licencia)

---

## 📌 Resumen del Proyecto

El experimento A/B evaluó $40,000$ usuarios distribuidos aleatoriamente entre el $1$ y el $28$ de enero de $2026$:
* **Versión A (Control):** $n_A = 19,982$ usuarios.
* **Versión B (Prueba):** $n_B = 20,018$ usuarios.

El objetivo central es responder a las siguientes preguntas clave de negocio:
1. ¿La nueva *landing page* incrementa la tasa de conversión general?
2. ¿Existen diferencias significativas en el valor de compra ($gasto$) entre ambas versiones?
3. ¿La fuente de tráfico (`traffic_source`) o el tipo de usuario (`user_type`) influyen en la conversión?

---

## 📂 Origen de los Datos

El dataset utilizado se incluye directamente en la carpeta del proyecto:

* **Ruta local:** `datasets/landing_experiment.csv`
* **Muestra total:** $40,000$ registros únicos.
* **Diccionario de datos:**

| Columna | Tipo | Descripción | Ejemplo |
| :--- | :--- | :--- | :--- |
| `user_id` | `string` | Identificador único del usuario | `26f3052e-8500-44ea-8fff-06de65258abb` |
| `date` | `date` | Fecha de interacción ($YYYY-MM-DD$) | `2026-01-01` |
| `landing` | `string` | Variante asignada (`A` o `B`) | `A` |
| `region` | `string` | Región geográfica | `Norte`, `Centro`, `Sur` |
| `dispositivo` | `string` | Dispositivo de navegación (`Mobile`, `Desktop`) | `Mobile` |
| `traffic_source` | `string` | Canal de origen (`Organic`, `Ads`, `Email`, `Referral`) | `Email` |
| `user_type` | `string` | Tipo de usuario (`Nuevo`, `Recurrente`) | `Recurrente` |
| `converted` | `int` | Conversión de compra ($1 = \text{Sí}$, $0 = \text{No}$) | $1$ |
| `gasto` | `float` | Monto pagado en USD ($\$0.00$ si `converted = 0`) | $38.08$ |

---

## 🛠️ Tecnologías y Librerías

El desarrollo fue realizado en **Python 3.10+** dentro de un entorno **Jupyter Notebook**.

* **Procesamiento y Manipulación:** `pandas`, `numpy`
* **Inferencia Estadística:** `scipy.stats` (`ttest_ind`, `levene`, `chi2_contingency`), `statsmodels` (`proportions_ztest`)
* **Visualización de Datos:** `matplotlib`, `seaborn`

---

## 🌳 Estructura del Repositorio

```text
ab-testing-landing-experiment/
├── datasets/
│   └── landing_experiment.csv       # Dataset principal del experimento
├── notebooks/
│   └── ab_test_analysis.ipynb       # Notebook ejecutable con análisis EDA y test de hipótesis
├── outputs/
│   └── graphics/                    # Visualizaciones generadas para el informe
├── .gitignore                       # Filtros de exclusión para Git
├── LICENSE                          # Licencia del código fuente
├── README.md                        # Documentación principal del repositorio
└── requirements.txt                 # Archivo de dependencias del proyecto
```

---

## ⚙️ Instalación y Uso

Sigue estos pasos para replicar el entorno de análisis en tu equipo local:

### 1. Clonar el repositorio
```bash
git clone https://github.com/tu_usuario/ab-testing-landing-experiment.git
cd ab-testing-landing-experiment
```

### 2. Crear y activar un entorno virtual
* **En Linux / macOS:**
  ```bash
  python3 -m venv venv
  source venv/bin/activate
  ```
* **En Windows:**
  ```cmd
  python -m venv venv
  venv\Scripts\activate
  ```

### 3. Instalar dependencias
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Ejecutar los notebooks
```bash
jupyter notebook notebooks/ab_test_analysis.ipynb
```

---

## 📊 Resultados y Conclusiones

### Resumen de Pruebas de Hipótesis

| Métrica / Hipótesis | Grupo A (Control) | Grupo B (Prueba) | Test Estadístico | $p$-value | Decisión / Conclusión |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Tasa de Conversión** | $12.57\%$ | $15.96\%$ | Z-Test ($Z = -9.68$) | $3.76 \times 10^{-22}$ | **Se rechaza $H_0$**: La Versión B supera a la A con un alza relativa de $+26.9\%$ ($+3.38\%$ absoluto). |
| **Gasto Promedio** | $\$61.09$ | $\$68.75$ | Welch $t$-test ($t = -9.48$) | $3.63 \times 10^{-21}$ | **Se rechaza $H_0$**: La Versión B incrementa el ticket promedio por cliente en $+\$7.66$. |
| **Fuente de Tráfico vs. Conversión** | Máx: `Email` ($14.99\%$) | Mín: `Organic` ($13.79\%$) | Chi-Cuadrado ($\chi^2 = 8.66$) | $0.0341$ | **Se rechaza $H_0$**: La tasa de conversión está asociada al canal de adquisición. |
| **Tipo de Usuario vs. Conversión** | Nuevo ($14.36\%$) | Recurrente ($14.09\%$) | Chi-Cuadrado ($\chi^2 = 0.51$) | $0.4736$ | **No se rechaza $H_0$**: La conversión es independiente del tipo de usuario. |

### Conclusiones y Recomendaciones de Negocio

1. **Implementar la Versión B:** Desplegar la Versión B como la versión estándar del sitio web. No solo eleva la conversión en $+3.38$ puntos porcentuales, sino que también aumenta el valor promedio del carrito.
2. **Priorizar Canales Directos:** Reasignar presupuesto hacia campañas de **Email Marketing** y **Ads**, los cuales registran las tasas de conversión más elevadas ($14.99\%$ y $14.74\%$ respectivamente).
3. **Mantener una Experiencia Unificada:** No es necesario invertir recursos en adaptar la *landing page* según la condición de usuario nuevo o recurrente, dado que se comportan de manera estadísticamente equivalente ($p = 0.4736$).

---

## 👤 Autor y Licencia

* **Desarrollado por:** Analista de Datos / Equipo de Marketing Digital
* **Licencia:** Este proyecto se distribuye bajo la licencia [MIT](LICENSE). Puedes usarlo, modificarlo y distribuirlo libremente.