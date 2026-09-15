# Segmentación de Clientes Bancarios y Análisis de Cross-Sell

Proyecto de analítica de negocio orientado a **Data Scientist / Business Analytics**: segmentación de clientes de tarjeta de crédito, definición de métricas de Activación, Uso y Retención (AUR), identificación de oportunidades de cross-sell y retención, y diseño de experimentos para validarlas.

## Contexto

Los bancos necesitan entender el comportamiento de sus clientes para decidir a quién ofrecerles productos nuevos (cross-sell) y a quién enfocar esfuerzos de retención antes de que se vayan (churn). Este proyecto simula ese análisis usando un dataset público de clientes de tarjeta de crédito.

## Dataset

[Credit Card Customers](https://www.kaggle.com/datasets/sakshigoyal7/credit-card-customers) (Kaggle) — 10,127 clientes con variables de producto (`Total_Relationship_Count`), actividad transaccional (`Total_Trans_Ct`, `Total_Trans_Amt`), crédito (`Credit_Limit`, `Avg_Utilization_Ratio`) y estado de fuga (`Attrition_Flag`).

## Metodología

1. **EDA exploratorio**: análisis de distribución de variables de uso, crédito y su relación con la fuga de clientes.
2. **Definición de métricas AUR**: mapeo de variables del dataset a Activación, Uso y Retención.
3. **Segmentación (K-Means, k=4)**: variables escaladas con `StandardScaler`, número de clusters elegido con el método del codo, perfiles validados con PCA.
4. **Impacto económico**: dimensionamiento de cada segmento en clientes y valor, estimación de riesgo por fuga y potencial de cross-sell (con supuestos de negocio documentados).
5. **Diseño de experimento**: hipótesis de control vs. tratamiento para validar acciones de retención y cross-sell antes de escalarlas.

## Segmentos identificados

| Segmento | Perfil | Clientes | Churn |
|---|---|---|---|
| Revolventes leales | Crédito bajo, alta utilización (62%), buen número de productos | 3,271 | 8.3% |
| Riesgo de fuga | Bajo enganche, pocos productos, baja utilización | 2,784 | **29.6%** |
| Alto poder adquisitivo subutilizado | Crédito alto, uso bajo, más productos | 2,877 | 15.8% |
| Alto valor, pocos productos | Mayor uso y gasto, crédito alto, pocos productos | 1,195 | **6.4%** |

## Hallazgo principal

El número de productos contratados está fuertemente ligado a la retención: el churn baja de 27% (2 productos) a 10% (6 productos). Esto define dos acciones prioritarias:

- **Retención** en el segmento de mayor fuga (29.6%), con ~$2.85M MXN en valor transaccional ya perdido (estimado).
- **Cross-sell** en el segmento de alto valor y bajo churn, con ~$2.54M MXN de ingreso potencial si aumenta su número de productos.

## Limitaciones

Los montos de impacto económico usan supuestos no verificados (ingreso estimado por producto adicional, valor anual por transaccionalidad), ante la ausencia de datos reales de rentabilidad o comisiones en el dataset público. Se declaran explícitamente en el reporte y deberían validarse con datos internos reales antes de tomar decisiones de inversión.

## Stack

Python · Pandas · Scikit-learn (KMeans, PCA, StandardScaler) · Matplotlib/Seaborn

## Contenido del repositorio

- `notebook.ipynb` — análisis completo (EDA, segmentación, impacto económico)
- `Resumen_Ejecutivo.pdf` — reporte ejecutivo de una página con hallazgos y recomendaciones

## Autor

Alan Kevin — [LinkedIn](#) · [GitHub](https://github.com/AlanKevinGZ)
