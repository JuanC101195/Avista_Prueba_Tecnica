# Prueba técnica: demanda transaccional por terminal y operación

Análisis exploratorio y pronóstico diario (1 al 15 de junio de 2017) de la demanda por operación en 5 terminales, con 4 meses de transacciones (31 de enero a 31 de mayo de 2017).

[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/JuanC101195/Avista_Prueba_Tecnica/blob/main/notebook/analisis_prediccion.ipynb)

En Colab el cuaderno pide subir `data_01.txt` si no lo encuentra (los datos no se incluyen en el repo).

## Cómo correrlo

```
pip install pandas numpy matplotlib scikit-learn statsmodels nbconvert ipykernel
cd notebook
jupyter nbconvert --to notebook --execute --inplace analisis_prediccion.ipynb
```

El cuaderno se demora unos minutos (validación con cuatro cortes y reentrenamiento final). Fue probado con Python 3.14.

## Estructura

```
notebook/analisis_prediccion.ipynb  todo el análisis y el modelo, con salidas
outputs/                          figuras, predicciones_15dias.csv, metricas_validacion.csv, resumen.json
informe_ejecutivo.docx            informe para la entidad
docs/arquitectura/arquitectura.html   diagrama del flujo del análisis (archify)
```

## Resultado en una línea

Modelo elegido: mezcla de regresión de Poisson con calendario y gradient boosting. En la ventana de prueba (17 al 31 de mayo) tiene WAPE 0,32 contra 0,45 del mejor método simple (promedio por día de la semana).
