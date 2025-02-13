# Tercera Semana

###### Georgina Salcido Valenzuela

#### Sesgo cognitivo

> Errores sistemáticos en el pensamiento que ocurren cuando las personas procesan e interpretan información en el mundo que los rodea.

Estos sesgos pueden afectar las decisiónes y juicios que hacemos, a menudo de manera consciente.

- En el aprendizaje automático, los sesgos cognitivos pueden manifestarse en los datos utilizados para entrenar modelos, lo que puede llevar a resultados sesgados o injustos.

**La escencia del Aprendizaje Automático**

El Aprendizaje Automático necesita de la exitencia de patrones, 

Se basa en identificar patrones en los datos, sin embargo, si los datos contienen sesgos, estos sesgos pueden ser aprendidos yperpetuados por los modelos de AA.

El AA depende de los datos disponibles, y si estos datos están sesgados, el modelo reflejará esos sesgos.

*Ejemplo: Si un sistema de préstamos esá entrenado con datos históricos que discriminan contra ciertos grupos étnicos, el modelo puede continuar negando préstamos a esos grupos de manera injusta.*

**Formas de mitigar el sesgo en el AA**

- *Diversidad en los datos:* Asegurarse de que los datos de entrenamiento sean represnetativos de todas las poblaciones y grupos afectados por el modelo.

- *Transparencia y auditoria:* Implementar mecanismos para auditar y explicar las decisiones tomadas por los modelos de AA, lo que permite identificar y corregir sesgos.

- *Evaluación contínua:* Monitorear el desempeño del modelo en diferentes grupos demográficos para detectar y corregir sesgos a lo largo del tiempo.

Los sesgos cognitivos no soloa fectan el AA, sino también nuestras decisiones diarias, desde la eleccion de productos hasta la interpretación de noticias.



---

#### Regresión lineal

Para la regresión lineal tenemos un conjunto de datos de entrenamiento, que consiste en un conjunto de ejemplos. Cada ejemplo consiste en un input $x$ y un input $y$.

| $x$ | $y$ |
|:---:|:---:|
| 1   | 1   |
| 2   | 3   |
| 4   | 3   |

Tenemos el siguiente ejemplo, donde la tabla representa nuestros datos de entrenamiento y donde cada fila es un ejemplo. 

```vega-lite
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "description": "Visualización de los datos",
  "data": {
    "values": [
      {"x": 1, "y": 1}, {"x": 2, "y": 3}, {"x": 4, "y": 3}
    ]
  },
  "mark": "point",
  "encoding": {
    "x": {"field": "x", "type": "quantitative"},
    "y": {"field": "y", "type": "quantitative"}
  }
}
```
