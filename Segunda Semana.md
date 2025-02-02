# Segunda semana...

###### Georgina Salcido Valenzuela

#### 

#### Machine Learning

Se utiliza por falta de información o cuando el modelo es demasiado complejo.

- Ej. Calcular la probablidad de que una transacción sea fraudulenta.
  
  - En este caso, se ocuparían muchas reglas y aún así no sería confiable.

**El machine learning es inductivo.**

No se puede declarar como verdadero o falso, ya que no es posible asegurar algo por más repeticiones que tenga. Se basa en puras hipótesis y axiomas.

> El objetivo es hacer un programa que nos hará el programa deseado.

---

Asumimos la existencia de una función $f$ donde

$f: x -> y$, cuyo funcionamiento es desconocido.

Además, tenemos un conjunto de datos finito y limitado que asumiremos como una muestra de un conjunto más grande de datos desconocidos.

$x = [x^1, x^2, ..., x^m]$

$D = [(x^1, y^1), (x^2, y^2), ..., (x^m, y^m),]$

Asumimos $y^i = f(x^i) + e$, donde e es una v.a. de tamaño desconocido.

Entonces $h^* e H$ de funciones, donde

$h: x->y$ tal que $h^*=f$

Por lo que nuestro aprendizaje es

$h_{w0,w1} = w_1x + w_0$

---

> A. Samuel (1959)
> 
> Field of study that gives computers the habit to learn without being explicitly programmed.

> T. Mitchell (1998)
> 
>  A computer program is said to learn from experience E with respect to some task T and some performance measure P, if its performance on T, as measured by P, improves with experience E.

---

###### Método del vecino más próximo

Si un dato es desconocido, utilizaremos los datos conocidos a su alrededor para analizar cuál tipo de dato predomina y poder asignarle un tipo a nuestro dato desconocido.

<img title="" src="file:///C:/Users/geo_s/AppData/Roaming/marktext/images/2025-01-28-08-46-31-image.png" alt="" width="324" data-align="center">  Utilizando a los 5 vecinos más cercanos, podemos sacar una conclusión sobre cuáles son del tipo 1 y cuáles son del tipo 2. Sin embargo, es demasiado específico y no parece muy confiable. Para facilitar esto, **generalizamos**.

<img title="" src="file:///C:/Users/geo_s/AppData/Roaming/marktext/images/2025-01-28-08-51-23-image.png" alt="" data-align="center" width="320">

De esta forma tenemos más margen de error, pero es más digerible y fácil de trabajar.

- Sacrificar el error por optimización.

---

#### Aprendizaje supervisado como una posibilidad.

El objetivo del aprendizaje supervisado es encontrar una hipótesis $h^*$ tal que minimice el error en los datos de entrenamiento (1) y que también generalice bien a los datos desconocidos (2).

    Decimos que $f=h^*$ ssi

            (1) $E_i(h^*)≈0$

            (2) $E_o(h^*)≈E_i(h^*)$

**Generalización**

> *Capacidad de un modelo para desempeñarse bien en datos desconocidos, no solo en datos conocidos (de entrenamiento)*

Necesitamos $E_{in}(θ)=0$ **y** $E_{in}(θ)=E_{out}(θ)$

    - Si se cumple una pero la otra no o no podemos garantizar una de ellas, entonces no hay aprendizaje.

    - Si la diferencia entre $E_0$ y $E_i$ es casi 0 y $E_i$ se acerca a 0, hay aprendizaje

**Desigualdad de Hoeffding**

> *Proporciona una cota superior para la probabilidad de que el error en $E_i$ y el error de $E_o$ difieran en más de ϵ.*

<img src="file:///C:/Users/geo_s/AppData/Roaming/marktext/images/2025-01-28-12-24-15-image.png" title="" alt="" data-align="center">

Esto implica que, con suficientes datos $(M)$, es probable que el error $E_i$ y el error $E_o$ sean similares.

- *Problemas con la Desigualdad de Hoeffding*
  
  No toma en cuenta la complejidad del conjunto de hipótesis $H$. Si $H$ es muy grande, la cota puede ser demasiado amplia.

**Dicotomía**

> *Asignación de etiquetas a un conjunto de datos específicos.*

Para un número de datos de tamaño $M$, el número de dicotomías posibles está acotado por $2^M$.     $M_H(M)≤2^M$

Debido a la complejidad del espacio de hipótesis, se introduce una cota más ajustada, tomando en cuenta el número máximo de dicotomías $(m_H)$ que el espacio de hipótesis $H$ puede generar sobre $M$ puntos.

<img src="file:///C:/Users/geo_s/AppData/Roaming/marktext/images/2025-01-28-12-49-04-image.png" title="" alt="" data-align="center">

**Dimensión VC $d_{vc}$**

> Medida de la capacidad de un espacio de hipótesis para clasificar correctamente un conjunto de datos. 

Si $d_{vc}$ es finita, entonces $m_h(H)$ crece polinomialmente con $M$, lo que permite que el aprendizaje sea posible. Es el valor más grande de M para el cual $M_h(M)=2^M$.

<img title="" src="file:///C:/Users/geo_s/AppData/Roaming/marktext/images/2025-01-29-08-14-40-image.png" alt="" width="461" data-align="center">

*La desigualdad de Vapnik--Chervonenkis*

Un modelo con una dimensión VC alta puede ajustarse a muchos conjuntos de datos diferentes, pero también es más propenso al sobreajuste.

**Regla de Oro para la Generalización**

Se sugiere que, para garantizar una buena generalización, el número de datos de entrenamiento $M$ debe ser al menos 10 veces la dimensión $VC$ del espacio de hipótesis.

> $M ≥ 10dv(H)$

- Sin embargo, esta regla no es siempre aplicable y depende del problema específico.

**Sobreajuste (sobreaprendizaje)**

> Ocurre cuando el modelo se ajusta demasiado a los datos de entrenamiento, capturando incluso en los ruidos y los errores, lo que resulta en un mal desempeño en datoss nos vistos.

**Subajuste (subaprendizaje)**

> Ocurre cuando el modelo es demasiado simple y no captura la estructura subyacente de los datos, lo que también resulta en un mal desempeño.

Es importante tomar en cuenta el tamaño del conjunto de datos $M$, ya que entre más datos, es más probable que el modelo capture la verdadera distribución y generalice meejor, sin embargo, si el espacio de hipótesis es demasiado complejo, necesitaremos más datos para evitar el sobreaprendizaje.



---

#### Árboles de decisión

Modelo de aprendizaje supervizado fácil de interpretar, que divide recursivamente el espacio en regiones más pequeñas, asignando una etiqueta o valor a cada región.

- **Nodos internos:** Representan pruebas sobre atributos o características.

- **Ramas:** Corresponden a los posibles valores de los atributos

- **Hojas:** Asignan una clase o valor a las instancias que llegan a ellas.



**Espacio de hipótesis**

Los árboles de decisión pueden representar **cualquier función** de los atributos de entrada, incluyendo funciones booleanas. Sin embargo, esto puede requerir un número exponencial de nodos, lo que los hace computacionalmente costosos para problemas complejos.



**Aprendizaje de árboles de decisión**

- *NP-Completo*: Un problema de este tipo es encontrar el árbol de decisión más pequeño/óptimo, por lo que se recurre a heurísticas *greedy*.

- *Algoritmo Greedy*: 
  
  1. Comienza con un árbol vacío.
  
  2. En cada paso, selecciona el mejor atributo para dividir los datosw.
  
  3. Repite el proceso recursivamente en cada subconjunto.



**Selección de atributos**

- *Ganancia de información:* Se utiliza para seleccionar el mejor atributo para dividir. La ganancia de información mide la reducción de la entropía despues de dividir los datos.
  
  - *Entropía:* Mide la incertidumbre en la distribución de las clases.

<img title="" src="file:///C:/Users/geo_s/AppData/Roaming/marktext/images/2025-02-02-15-57-02-image.png" alt="" data-align="center" width="365">



**Sobreajuste en Árboles de decisión**

El mayor problema es que tienden a sobreajustarse a los datos de entrenamiento, especialmente cuando son muy profundos. Para esto hay diversas soluciones:

- *Poda de árbol*: Se usa para reducir el sobreajuste eliminando ramas irrelevantes.
  
  - Poda pre-pruning: Detiene el crecimiento temprano del árbol.
  
  - Poda post-prunning: Reduce el tamaño después de que el árbol está construido.

- *Métodos de ensamblaje:* Como bosques aleatorios, que combinan múltiples árboles para reducir el sobreajuste.



**Métodos de ensamblaje**

- Bagging (Bootstrap Aggregation): Entrenar múltiples modelos en diferentes subconjuntos de datos (muestras bootstrap) y combinar sus predicciones. Reduce la varianza del modelo sin aumentar el sesgo.

- Bosque aleatorio: Combina bagging con la selección aleatoria de atributos en cada división de árboles. Reduce el sobreajuste y mejora la generalización.
  
  - Algoritmo:
    
    1. Se generan múltiples árboles utilizando muestras bootstraps.
    
    2. En cada división, se selecciona un subconjunto aleatorio de atributos.
    
    3. Las predicciones finales se obtienen por mayoría (clasificación) o promedio (regresión).



**Algoritmos**

- *ID3:* utiliza la ganancia de información para seleccionar atributos.

- *C4.5:* Una mejora de ID3 que maneja datos continuos y valores faltantes.

- CART: Utiliza el criterio de Gini para clasificar.



**Trade-off entre sesgo y varianza**

- *Sesgo (Bias)*: Error debido a suposiciones incorrectas en el modelo.

- *Varianza:* Error debido a la sensibilidad del modelo a pequeñas fluctuaciones en el conjunto de entrenamiento.



**Aplicaciones**

Los árboles de decisión y los métodos de ensamblaje son ampliamente utilizados en el problemas de clasificación, como la detección de spam, diagnóstico médico, etc.

También se pueden utilizar para problemas de regresión, donde el objetivo es predecir un valor continuo.



**Limitaciones**

- *Sobreajuste:* Aunque los métodos de ensamblaje ayudan a reducir el sobreajuste, los árboles individuales aún pueden ser propensos a este problema.

- *Interpretabilidad:* Aunque los árboles individuales son interpretables, los métodos de ensamblaje como Bosque Aleatorio son menos interpretables debido a la combinación de múltiples árboles.
