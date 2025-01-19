# Curso de Inteligencia Artificial

#### Maestro: Julio Waissman

#### Página del curso: [ia-uson.github.io](https://ia-unison.github.io/)

##### Bibliografía recomendada: Inteligencia Artificial: Un enfoque moderno.

### Criterios de evaluación:

- Actividades de evaluación continua (notas): 20%

- Actividades de evaluación de conocimientos (Problemarios): 20%

- Actividades de evaluación de competencias (laboratorio): 20%

- Exámenes: 40%

##### Notas:

Se abrirá un repositorio donde semanalmente se suban los archivos MD.

Se hará un MD por semana.

Pueden subirse a github.

Las notas se revisaran los días martes.

##### Laboratorio:

En github, haremos un fork del repositorio del maestro y realizar un pull request para entregar el trabajo.

Es necesario aprobar el laboratorio para aprobar el curso.

Solo se calificará el mejor 80% de los trabajos entregados.

##### Exámenes:

Son a libro, cuaderno y computadora abierta.

Al final habrá uno global.



----

## Iniciando con el curso...

~~Inteligencia artificial~~ Inteligencia Racional

###### La inteligencia artificial es el desarrollo de agentes racionales.

Agentes que al interactuar con un entorno, maximice la esperanza de una utilidad futura. 

> $max( E [utilidad (t + vt)])$



###### Interactuar racionalmente

Maximizar un valor esperado con mediciones **posibles** con acciones **posibles** con **lo que se conoce** del entorno.

> Que sea racional **no** significa que será *exitoso y perfecto*

###### 

###### Lo que debe de saber el agente del entorno: PEAS

- Medida de desempeño/utilidad (Performance)

- Características del Entorno

- Actuadores

- Sensores
  
  

> Es muy importante saber en cada entorno qué acciones legales puedo hacer, es decir, cuáles son posibles.



1. Tarea

2. Medida de desempeño

3. Percepciones

4. Acciones

5. Entorno
   
   

###### Entornos que puedo tener:

- Discreto / Continuo

- Estático / Dinámico

- Observable / Parcialmente observable

- Determinista / Estocaico

- Conocido / Desconocido

- Un agente / Multiagente

- Periódico / Secuencial

--- 

###### Ejemplo 1

Tengo 2 cuartos: A y B que están sucios y se limpian con una aspiradora automática.

- La tarea es limpiar los cuartos

- La medida de desempeño es que los dos estén limpios en el menor número de casos posibles y con el menor gasto de energía posible.

- Las acciones serían moverse a la izquierda (cuarto A) o derecha (cuarto B), limpiar o no hacer nada.

- Espacio de estado: 
  
  - $X_1$ = {L, S}
  
  - $X_2$ = {L, S}
  
  - $X_3$ = {A, B}

       x = (L, S, A)

Como tiene espacios finitos, es discreto.



###### Ejemplo 2

Tengo un dron.

- Espacio de estado: h, x, y, θ, h', x', y', θ'. 

Como se encuentra en los reales, es continuo.

---

Problema finita y numerable - se puede presentar como grafo.

``Espacio de entorno: todos los posibles estados.``

> $Desempeño_{t+v} = desempeño_t + desempeño_{local} (x_t, a_t, x_{t+vt})$



### Agentes

- ###### Agente aleatorio:

Se recomienda cuando no se conoce el entorno.

- ###### Agente reactivo:
  
  EJ. programas Demon.
  
  Agentes reflejo

- ###### Learning agents:
  
  $a = f(p)$
  
  $­â = f_{aprox}(p, θ)$
  
  
