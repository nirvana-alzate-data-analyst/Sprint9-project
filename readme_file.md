# Proyecto 8: Validando hipótesis de negocio con pruebas estadísticas 📊

## 📊 Introducción

Eres analista de datos en el equipo de marketing digital de una empresa de e-commerce. Se ejecutó un **experimento A/B** en la página de inicio (*landing page*), comparando dos versiones (A y B) con el objetivo de mejorar la tasa de conversión y el valor económico por usuario.

La empresa necesita una decisión basada en datos para definir qué versión implementar de manera definitiva, considerando la tasa de conversión, el gasto promedio y el comportamiento por canal de tráfico y tipo de usuario.

---

## 🎯 Objetivo

Explorar, validar y analizar estadísticamente el experimento A/B para identificar diferencias significativas entre las páginas de inicio y traducir los resultados en recomendaciones estratégicas para el negocio.

### 💡 Preguntas de negocio
* ¿Existe una diferencia significativa en el gasto promedio por usuario convertido entre ambas versiones?
* ¿Qué versión de la página (A o B) genera mayor tasa de conversión?
* ¿La conversión depende de la fuente de tráfico?
* ¿El tipo de usuario (nuevo o recurrente) influye en la conversión?
* ¿Qué hallazgos o *insights* permiten optimizar la estrategia de marketing y el diseño de la *landing page*?

---

## 🎯 Aprendizaje del proyecto

Al finalizar este proyecto, serás capaz de:
1. Explorar y validar un dataset proveniente de un experimento A/B real.
2. Comparar métricas de negocio mediante pruebas estadísticas apropiadas.
3. Interpretar resultados estadísticos desde una perspectiva de negocio.
4. Visualizar resultados para respaldar conclusiones.
5. Comunicar hallazgos o *insights* de forma clara a *stakeholders* no técnicos.

---

## 📁 Dataset

El archivo `/datasets/landing_experiment.csv` contiene información de usuarios expuestos a dos versiones de la página de inicio dentro del experimento A/B.

| Columna | Tipo de dato | Descripción | Ejemplo real |
| :--- | :--- | :--- | :--- |
| `user_id` | Categórica (UUID) | Identificador único del usuario | `26f3052e-8500-44ea-8fff-06de65258abb` |
| `date` | Fecha (YYYY-MM-DD) | Fecha en la que el usuario fue expuesto a la página | `2026-01-01` |
| `landing` | Categórica | Versión de la página mostrada al usuario (`A`, `B`) | `A` |
| `region` | Categórica | Región geográfica del usuario | `Norte`, `Centro`, `Sur`, `Occidente`, `Oriente` |
| `dispositivo` | Categórica | Tipo de dispositivo utilizado por el usuario | `Mobile`, `Desktop` |
| `traffic_source` | Categórica | Canal por el que llegó el usuario | `Organic`, `Ads`, `Email`, `Referral` |
| `user_type` | Categórica | Tipo de usuario según historial previo | `Nuevo`, `Recurrente` |
| `converted` | Binaria (0/1) | Indica si el usuario realizó una conversión (compra) | `0`, `1` |
| `gasto` | Numérica (float) | Monto gastado por el usuario (`0` si no convirtió) | `38.08` |

---

## 🔍 Detalles y consideraciones importantes

* **Unidad de análisis:** Cada fila representa un usuario expuesto a una única versión de la página de inicio.
* **Grupos del experimento (`landing`):**
  * `A`: Versión de control (página A)
  * `B`: Versión de prueba (página B)
* **Variable objetivo (`converted`):**
  * `1` → El usuario realizó una compra.
  * `0` → El usuario no convirtió.
* **Manejo de la variable `gasto`:**
  * Solo tiene valores mayores a cero cuando `converted = 1`.
  * **Importante:** Filtrar correctamente al comparar gasto promedio para evitar sesgos e incluir únicamente usuarios convertidos.
* **Segmentación:** Las variables `region`, `traffic_source` y `user_type` permiten analizar la conversión por segmentos y validar efectos diferenciales.
* **Balanceo:** El experimento está balanceado entre las versiones A y B, lo que permite aplicar pruebas estadísticas con confianza.

---

## 📝 Plan de acción (Pensamiento programático)

### 🔄 Flujo general del proyecto

| Paso | Fase | Resultado para el negocio |
| :---: | :--- | :--- |
| **1** | Cargar y validar datos | Confianza en la calidad del experimento |
| **2** | Comparar gasto promedio (A vs. B) | Identificar qué página genera más valor |
| **3** | Comparar tasa de conversión (A vs. B) | Identificar la página más efectiva |
| **4** | Analizar tráfico y conversión | Optimizar inversión en canales |
| **5** | Analizar tipo de usuario y conversión | Evaluar si segmentar usuarios |
| **6** | Visualización | Incluir gráficas que respalden las conclusiones |
| **7** | Insight ejecutivo | Decisión clara para *stakeholders* |

---

## ✅ Criterios de evaluación del proyecto

* **📊 Análisis estadístico:**
  * Prueba estadística adecuada.
  * Verificación de supuestos.
  * Interpretación correcta del valor $p$ ($p$-value).

* **🧠 Razonamiento analítico:**
  * Hipótesis claras.
  * Coherencia entre pregunta, método y conclusión.
  * Identificación de limitaciones.

* **💬 Comunicación de resultados:**
  * Explicaciones claras.
  * Visualizaciones efectivas.
  * Enfoque en impacto de negocio.

* **🧾 Organización y reproducibilidad:**
  * Notebook estructurado.
  * Código claro y reproducible.
  * Comentarios precisos y útiles.