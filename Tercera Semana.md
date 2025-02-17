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

Para la regresión lineal tenemos un conjunto de *datos de entrenamiento*, que consiste en un conjunto de ejemplos. Cada ejemplo consiste en un input $x$ y un input $y$.

Tenemos el siguiente ejemplo, donde la tabla representa nuestros datos de entrenamiento y donde cada fila es un ejemplo.

| $x$ | $y$ |
|:---:|:---:|
| 1   | 1   |
| 2   | 3   |
| 4   | 3   |

Podemos visualizar los datos en la siguiente gráfica.

```vega-lite
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "description": "Visualización de los datos",
  "data": {
    "values": [
      {"x": 1, "y": 1}, {"x": 2, "y": 3}, {"x": 4, "y": 3},
      {"x": 3, "y": 2.71}
    ]
  },
  "layer": [
    {
      "mark": {
        "type": "point",
        "filled": true,
        "color": "blue",
        "size": 70
      },
      "encoding": {
        "x": {"field": "x", "type": "quantitative"},
        "y": {"field": "y", "type": "quantitative"}
      }
    },
    {
      "mark": {
        "type": "line",
        "color": "red"
      },
      "transform": [
        {
          "regression": "y",
          "on": "x"
        }
      ],
      "encoding": {
        "x": {"field": "x", "type": "quantitative"},
        "y": {"field": "y", "type": "quantitative"}
      }
    },
    {
      "mark": {
        "type": "point",
        "filled": true,
        "color": "white",
        "size": 100
      },
      "encoding": {
        "x": {"field": "x", "type": "quantitative"},
        "y": {"field": "y", "type": "quantitative"}
      },
      "transform": [
        {
          "filter": "datum.x === 3"
        }
      ]
    }
  ]
}
```

Lo que queremos es tomar todos estos datos, tener un algoritmo de aprendizaje, producir un *predictor* $f$, donde el predictor en este caso es una línea.

El predictor deberá tomar un input (en este caso 3) y producir un output (en este caso 2.71).



**¿Qué es la clase de hipótesis?**

Tenemos un primer predictor (la línea roja de la gráfica): $f(x)=1+0.57x$

Tenemos un segundo predictor: $f(x)=2+0.2x$

Los predictores tienen la forma de $f(x)=w_1+w_2x$  donde $w_1$ es la intersección, mientras que $w_2$ es la pendiente.

*Para generalizar* usamos notación vectorial: $w = [w_1, w_2]$ donde $w$ es un vector de peso.

Definimos un *extractor de características*: $\phi(x)=[1,x]$  donde el segundo vector es un output conocido como vector de características.

Con esto, tenemos nuestro predictor: $f_w(x)=w . \phi(x)$ 

- Ejemplo. $f_w(3)=[1,0.57].[1,3]=2.71$     (punto blanco de la gráfica)

Con todo esto, nuestra *clase de hipótesis* se define cómo:

$F={f_w:w\in\real^2}$ donde $F$ es el conjunto de todos los predictores $f_w$



**Función loss**

La calidad de un predictor depende de la calidad con las que se ajusta a los datos de entrenamiento, cuantificándola como la distancia entre la prediccion y un objetivo. A esta diferencia se le conoce como *residuo*, midiendo el residuo de todos nuestro puntos.

$Loss(x,y,z)=(f_w(x)-y)^2$         pérdida cuadrática

- Ejemplo 1. $Loss(1,1,[1,0.57])=([1,0.57].[1,1]-1)^2=0.32$

- Ejemplo 2. $Loss(2,3,[1,0.57])=([1,0.57].[1,2]-3)^2=0.74$

- Ejemplo 1. $Loss(4,3,[1,0.57])=([1,0.57].[1,4]-3)^2=0.08$

Con esto podemos definir la pérdida de entrenamiento de un vecto de onda particular como el promedio de las pérdidas.

$TrainLoss(w)=\frac{1}{|D_{train}|} \sum_{(x,y)}Loss(x,y,w)$

- Ejemplo. $TrainLoss([1,0.57])=0.38$



**Descenso a gradiente**

Queremos encontrar el algoritmo más óptimo con la menor perdida de  entrenamiento. ($min_wTrainLoss(w)$)

> *Gradiente*
> 
> El gradiente $\nabla_WTrainLoss(w)$ es la dirección en la que incrementa en mayor medida la pérdida de entrenamiento.

*Algoritmo*

```
initialize w = [0, ..., 0]
For t = 1, ..., T: #epochs
    w <- w - n f_wTrainLoss(w)
# donde n es el tamaño de los pasos y f_wTrainLoss(w) es el gradiente
```

El objetivo de la función es 

$TrainLoss(w)=\frac{1}{|D_{train}|} \sum_{(x,y \in D_{train})}(w.\phi(x)-y)^2$

Ergo el gradiente queda cómo 

$\nabla_WTrainLoss(w) = \frac{1}{|D_{train}|} \sum_{(x,y \in D_{train})} 2(w.\phi(x)-y)\phi(x)$

donde $w.\phi(x)$ es el predictor y $y$ es el target, por lo que si el predictor es igual al target, el gradiente es cero.  Pero si el predictor y el target no son iguales, el gradiente estará en la dirección en la que asciende la predicción, alejándose del target.





---

#### Clasificación lineal

> Método utilizado para separar datos en diferentes categorías mediante una línea o hiperplano.

Es un enfoque eficaz cuando los datos son linealmente separables, osea, cuando es posible trazar una línea que divida claramente las distintas clases.



**Ecuación de la recta**

> $y = mx + b$
> 
> donde $m$ es la pendiente y $b$ es la intersección con el eje $y$.

esta ecuación se generaliza a un hiperplano en espacios de mayor dimensión, permitiendo la separación de datos en espacios multidimensionales.



**Funciones de activación**

Determinan la salida de un modelo de clasificación en función de la entrada. Una función común es la función signo, que asigna una clase positiva o negativa según si la entrada es mayor o menor que cero. Sin embargo, esta función es sensible a pequeñas variaciones en los datos y no proporciona probabilidades de pertenencia a una clase específica.



**Perceptrón**

> algoritmo de aprendizaje supervisado que ajusta los pesos de las características para minimizar los errores de clasificación.

Funciona mediante la actualización iterativa de los pesos en función de los errores cometidos en las predicciones, utilizando una regla de actualización basada en el gradiente del error. Esto permite que el perceptrón aprenda a clasificar correctamente los datos linealmente separables.

- *Limitaciones:* incapacidad para resolver problemas no lineales



**Clasificadores lineales en múltiples dimensiones**

Los CL pueden manejar datos en espacios de alta dimensión mediante la generalización de la ecuación de la recta a un hiperplano. Esto permite la separación de datos en espacios multidimensionales.

- El entrenamiento de estos clasificadores se realiza utilizando métodos como la regresión logística, que ajusta los pesos para minimizar la función de pérdida y mejorar la precisión de la clasificación.



**Regresión logística**

> Extensión de la clasificación lineal que utiliza la función sigmoide para modelar probabilidades y manejar problemas de clasificación binaria.

La función sigmoide transforma la salida lineal en un valor entre 0 y 1, interpretado como la probabilidad de que una instancia pertenezca a una clase específica.



#### Descenso de gradiente estocástico

> **Descenso de gradiente:** Es un algoritmo de optimización que ajusta los parámetros del modelo para minimizar la función de pérdida.

- En conjuntos de datos grandes, calcular el gradiente de la función de pérdida completa en cada iteración puede ser muy costoso. Ya que cada iteración requiere procesar todos los ejemplos de procesamiento, lo que es lento y poco eficiente.



> **Descendo de gradiente estocástico:** es una variante del DG que en lugar de calcular el gradiente de la función de pérdida completa, actualiza los parámetros del modelo utiñizando el gradiente de la pérdida de un solo ejemplo de entrenamiento cada iteración.

- Reduce signitificativamente el tiempo de cómputo por iteración y permite que el modelo se actualice más rápidamente.



**Algoritmo**

1. *Inicialización:* Establecer los parámetros del modelo con valores iniciales.

2. *Iteración:* Para cada ejemplo de entrenamiento $(x,y)$:
   
   1. Calcular el gradiente de la función de pérdida respecto a los parámetros del modelo
   
   2. Actualizar los parámetros del modelo en la dirección opuesta al gradiente, utilizando una tasa de aprendizaje.
