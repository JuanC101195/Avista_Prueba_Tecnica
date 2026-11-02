# Prueba técnica: demanda transaccional por terminal y operación

Análisis exploratorio y pronóstico diario (1 al 15 de junio de 2017) de la demanda por operación en 5 terminales, con 4 meses de transacciones (31 de enero a 31 de mayo de 2017).

[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/JuanC101195/Avista_Prueba_Tecnica/blob/main/notebook/analisis_prediccion.ipynb)

El cuaderno tiene dos partes: la Parte 1 es lo que pide la prueba (5 terminales x 5 operaciones) y la Parte 2 es una ampliación a todas las series. En Colab pide subir `data_01.txt` si no lo encuentra (los datos no se incluyen en el repo).

## Cómo correrlo

```
pip install pandas numpy matplotlib scikit-learn statsmodels nbconvert ipykernel
cd notebook
jupyter nbconvert --to notebook --execute --inplace analisis_prediccion.ipynb
```

El cuaderno se demora unos minutos entre las dos partes (validación con cuatro cortes y reentrenamiento final). Lo probé con Python 3.14.

## Estructura

```
notebook/analisis_prediccion.ipynb  todo el análisis y el modelo (Parte 1 y Parte 2), con salidas
outputs/                          figuras, predicciones_15dias.csv, metricas_validacion.csv, resumen.json y los ext_*
```

## Resultado en una línea

Modelo elegido: mezcla de regresión de Poisson con calendario y gradient boosting. En la ventana de prueba (17 al 31 de mayo) tiene WAPE 0,32 contra 0,45 del mejor método simple (promedio por día de la semana).

## Extensión

La Parte 2 del mismo cuaderno (`notebook/analisis_prediccion.ipynb`) repite el enfoque sobre las 47 x 46 combinaciones de terminal y operación, no solo las 25 del 5x5. Las separa en viables, ralas e inactivas, aplica el mismo modelo a las viables y un método simple a las ralas, y valida con los mismos cuatro cortes (WAPE 0,37 por serie viable contra 0,48 del baseline; 0,30 por terminal y 0,20 por operación al sumar series).
Solo las series con 10 o más transacciones por día me parecen confiables a nivel individual.
Las salidas están en `outputs/` con el prefijo `ext_`: `ext_predicciones_15dias_todas.csv`, `ext_pronostico_por_terminal.csv`, `ext_pronostico_por_operacion.csv`, `ext_metricas_por_segmento.csv` y las figuras `ext_fig*.png`. La Parte 2 corre en menos de un minuto.
