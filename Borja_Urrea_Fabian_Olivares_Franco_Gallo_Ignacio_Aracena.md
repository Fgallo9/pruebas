# Informe – Tarea 1: Diseño y calibración de un brazo robótico industrial

**Integrantes:** Borja Urrea, Fabián Olivares, Franco Gallo, Ignacio Aracena.
**Asignatura:** ICI2141 – Métodos Numéricos.

> **Nota técnica importante del template:** la fórmula de punto fijo propuesta es
> `asin((Tmax/mgL)e^(-cθ))`. Con los datos nominales, el template fija `x0=0.5`,
> pero en ese punto el argumento del `asin` es mayor que 1. Para que el notebook
> pueda ejecutarse completo, se aplicó una saturación a `[-1,1]` únicamente como
> resguardo de dominio. Después del primer paso, la iteración vuelve a la fórmula
> normal y converge al mismo equilibrio.

## Acto 1 – Calibración

Se busca el equilibrio entre el torque disponible del motor y el torque gravitacional:

`f(θ) = Tmax·e^(-cθ) - mgL·sin(θ)`.

Con los valores nominales, los cuatro métodos convergen a un ángulo cercano a

**θ* ≈ 0.983094 rad**.

### Bisección

| k | aproximación | f(θ) | error relativo aprox. |
| --- | --- | --- | --- |
| 1 | 0.500000 | 8.528460e+00 | — |
| 2 | 0.750000 | 3.725696e+00 | 3.333333e-01 |
| 3 | 0.875000 | 1.630081e+00 | 1.428571e-01 |
| 4 | 0.937500 | 6.662879e-01 | 6.666667e-02 |
| 5 | 0.968750 | 2.062194e-01 | 3.225806e-02 |
| 6 | 0.984375 | -1.826313e-02 | 1.587302e-02 |
| 7 | 0.976562 | 9.351280e-02 | 8.000000e-03 |
| 8 | 0.980469 | 3.750830e-02 | 3.984064e-03 |
| 9 | 0.982422 | 9.593422e-03 | 1.988072e-03 |
| 10 | 0.983398 | -4.342149e-03 | 9.930487e-04 |
| 11 | 0.982910 | 2.623814e-03 | 4.967710e-04 |
| 12 | 0.983154 | -8.596235e-04 | 2.483238e-04 |
| 13 | 0.983032 | 8.819811e-04 | 1.241773e-04 |
| 14 | 0.983093 | 1.115030e-05 | 6.208481e-05 |
| 15 | 0.983124 | -4.242437e-04 | 3.104144e-05 |
| 16 | 0.983109 | -2.065485e-04 | 1.552096e-05 |
| 17 | 0.983101 | -9.769954e-05 | 7.760541e-06 |


La bisección necesitó **17 iteraciones** con el criterio solicitado. Es un método
robusto porque conserva un intervalo con cambio de signo. Su convergencia es lineal,
de orden aproximadamente **p = 1**, y el ancho del intervalo se reduce por un factor
aproximado de **1/2** en cada iteración.

### Punto fijo

| k | aproximación | f(θ) | error relativo aprox. |
| --- | --- | --- | --- |
| 1 | 1.570796 | -5.581237e+00 | 6.816901e-01 |
| 2 | 0.669156 | 5.194040e+00 | 1.347430e+00 |
| 3 | 1.340768 | -4.082563e+00 | 5.009163e-01 |
| 4 | 0.769721 | 3.380673e+00 | 7.418896e-01 |
| 5 | 1.183444 | -2.543443e+00 | 3.495927e-01 |
| 6 | 0.852441 | 1.991977e+00 | 3.883004e-01 |
| 7 | 1.093843 | -1.484875e+00 | 2.206918e-01 |
| 8 | 0.906557 | 1.136250e+00 | 2.065907e-01 |
| 9 | 1.044517 | -8.472334e-01 | 1.320799e-01 |
| 10 | 0.939134 | 6.418715e-01 | 1.122128e-01 |
| 11 | 1.017338 | -4.795511e-01 | 7.687113e-02 |
| 12 | 0.958080 | 3.616425e-01 | 6.185004e-02 |
| 13 | 1.002261 | -2.706467e-01 | 4.408130e-02 |
| 14 | 0.968928 | 2.036401e-01 | 3.440218e-02 |
| 15 | 0.993850 | -1.525746e-01 | 2.507635e-02 |
| 16 | 0.975091 | 1.146658e-01 | 1.923810e-02 |
| 17 | 0.989139 | -8.597208e-02 | 1.420243e-02 |
| 18 | 0.978579 | 6.457092e-02 | 1.079153e-02 |
| 19 | 0.986495 | -4.843288e-02 | 8.024175e-03 |
| 20 | 0.980549 | 3.636396e-02 | 6.064163e-03 |
| 21 | 0.985008 | -2.728214e-02 | 4.527371e-03 |
| 22 | 0.981660 | 2.047985e-02 | 3.411097e-03 |
| 23 | 0.984172 | -1.536715e-02 | 2.552466e-03 |
| 24 | 0.982286 | 1.153443e-02 | 1.919833e-03 |
| 25 | 0.983701 | -8.655580e-03 | 1.438426e-03 |
| 26 | 0.982639 | 6.496404e-03 | 1.080866e-03 |
| 27 | 0.983436 | -4.875198e-03 | 8.104199e-04 |
| 28 | 0.982838 | 3.658935e-03 | 6.086371e-04 |
| 29 | 0.983287 | -2.745900e-03 | 4.565348e-04 |
| 30 | 0.982950 | 2.060815e-03 | 3.427593e-04 |
| 31 | 0.983202 | -1.546590e-03 | 2.571606e-04 |
| 32 | 0.983013 | 1.160713e-03 | 1.930389e-04 |
| 33 | 0.983155 | -8.710928e-04 | 1.448493e-04 |
| 34 | 0.983048 | 6.537499e-04 | 1.087213e-04 |
| 35 | 0.983128 | -4.906288e-04 | 8.158638e-05 |
| 36 | 0.983068 | 3.682127e-04 | 6.123394e-05 |
| 37 | 0.983113 | -2.763384e-04 | 4.595292e-05 |
| 38 | 0.983080 | 2.073892e-04 | 3.448850e-05 |
| 39 | 0.983105 | -1.556429e-04 | 2.588244e-05 |
| 40 | 0.983086 | 1.168083e-04 | 1.942490e-05 |
| 41 | 0.983100 | -8.766318e-05 | 1.457791e-05 |
| 42 | 0.983089 | 6.579024e-05 | 1.094069e-05 |
| 43 | 0.983098 | -4.937477e-05 | 8.210782e-06 |


El punto fijo necesitó **43 iteraciones**. Cerca de la solución,
`|g'(θ*)| ≈ 0.750488`, menor que 1, por lo que existe convergencia local.
La razón entre errores sucesivos se aproxima a ese valor y el orden empírico es
**p ≈ 1**. Es claramente más lento que Newton y Secante.

### Newton-Raphson

| k | aproximación | f(θ) | error absoluto |
| --- | --- | --- | --- |
| 1 | 0.912232 | 1.048985e+00 | 4.122325e-01 |
| 2 | 0.980644 | 3.500537e-02 | 6.841121e-02 |
| 3 | 0.983091 | 4.575514e-05 | 2.447130e-03 |
| 4 | 0.983094 | 7.863754e-11 | 3.207002e-06 |
| 5 | 0.983094 | -1.776357e-15 | 5.511813e-12 |


Newton necesitó **5 iteraciones**. En la zona asintótica el error cae
aproximadamente como el cuadrado del error anterior, por lo que el orden observado
es cercano a **p ≈ 2**. Esto explica la caída muy rápida de las últimas iteraciones.

### Secante

| k | aproximación | f(θ) | error absoluto |
| --- | --- | --- | --- |
| 1 | 0.988191 | -7.251511e-02 | 1.180939e-02 |
| 2 | 0.983047 | 6.687958e-04 | 5.143446e-03 |
| 3 | 0.983094 | -1.832943e-06 | 4.700371e-05 |
| 4 | 0.983094 | -4.604317e-11 | 1.284691e-07 |


Secante necesitó **4 iteraciones**. Se observa convergencia superlineal:
es más rápida que los métodos de orden 1 y no requiere evaluar la derivada.
Con las pocas iteraciones disponibles antes de llegar al límite de precisión,
la estimación empírica queda alrededor de **p ≈ 1.8**; teóricamente la secante
tiende a un orden cercano a 1.618 cuando se alcanza claramente el régimen asintótico.

### Comparación de los cuatro métodos

| Método | Iteraciones | Orden/tasa observada | Comentario |
| --- | ---: | --- | --- |
| Bisección | 17 | p ≈ 1, factor ≈ 0.5 | Muy robusta, pero lenta |
| Punto fijo | 43 | p ≈ 1, factor ≈ 0.750 | Convergencia lineal y oscilatoria |
| Newton | 5 | p ≈ 2 | El más rápido cerca de la raíz |
| Secante | 4 | superlineal | Muy rápida sin derivada |

### Estudio paramétrico de la masa

| Masa (kg) | Resultado en [0,1] |
| ---: | --- |
| 1.0 | No hay raíz en el intervalo |
| 1.5 | θ* ≈ 0.983094 rad |
| 2.5 | θ* ≈ 0.635981 rad |

Al aumentar la masa, el torque gravitacional aumenta y el equilibrio aparece a un
ángulo menor. Por eso el límite seguro disminuye desde aproximadamente 0.983094 rad
para 1.5 kg a 0.635981 rad para 2.5 kg.

Para 1.0 kg no hay raíz en `[0,1]` porque incluso en θ = 1 el motor todavía entrega
más torque que el requerido por la gravedad. Eso no significa que el brazo falle:
significa que el cruce ocurre fuera del intervalo estudiado. El umbral para que la
raíz entre exactamente por θ = 1 es aproximadamente **m = 1.471016 kg**.
Por debajo de ese valor no aparece una raíz dentro de `[0,1]`; para masas mayores sí.

## Acto 2 – Trayectoria

Las soluciones normalizadas a `(-π,π]` son:

| Waypoint | (x,y) | θ1 (rad) | θ2 (rad) | det(J) |
| ---: | --- | ---: | ---: | ---: |
| 1 | (2.0, 1.0) | -0.251993 | 1.780667 | 2.934174 |
| 2 | (3.48, 0.1) | -0.060457 | 0.208222 | 0.620162 |
| 3 | (0.5, 2.0) | 0.569848 | 1.910633 | 2.828427 |

El waypoint 2 tiene un determinante mucho menor que los otros dos. Como
`det(J)=L1·L2·sin(θ2)`, un θ2 cercano a cero representa un brazo casi extendido.
En esa situación el Jacobiano se acerca a una matriz singular: pequeños cambios en
la posición objetivo pueden exigir cambios relativamente grandes en los ángulos.
Por eso esta configuración es más sensible a errores de medición o perturbaciones.

El **warm-start** es razonable porque el brazo recorre puntos consecutivos en el tiempo.
La configuración anterior normalmente está cerca de la siguiente solución, por lo que
Newton parte desde una estimación físicamente coherente y evita saltar innecesariamente
a soluciones coterminales.

## Acto 3 – Balance de fuerzas, condición y estabilidad

### Gauss sin pivoteo versus LU con pivoteo parcial

**Gauss sin pivoteo:**

`[0.979999, 2.005101, 2.999851, 3.996748, 4.9951, 5.996032, 7.003471]`

**LU con pivoteo parcial:**

`[0.998002, 2.000421, 3.000002, 3.999774, 4.999613, 5.999708, 7.000251]`

La solución nominal del sistema está muy cerca de `[1,2,3,4,5,6,7]`. Con truncamiento
a seis decimales, Gauss sin pivoteo se aleja más que LU. La causa principal es el
primer pivote `A00 = 0.0001`: dividir por un número tan pequeño produce
multiplicadores enormes y amplifica los errores de truncamiento.

El pivoteo parcial busca el elemento de mayor magnitud de la columna antes de eliminar.
Así evita usar el `0.0001` como primer divisor y reduce fuertemente la amplificación
numérica.

### Generalidad para cualquier n

Las funciones usan `n = len(A)` o `n = len(K)`, construyen matrices y vectores según
ese tamaño, y recorren filas y columnas con ciclos. No se escribieron soluciones
específicas para siete nodos. Esta misma idea se utiliza en Gauss, LU, sustituciones,
condición, factores de crecimiento y Cholesky.

### Fuerzas provenientes de los waypoints

| Waypoint | ||F||₂ | máx |Fi| |
| --- | --- | --- |
| 1 | 18.281502 | 16.571870 |
| 2 | 2.100684 | 1.884638 |
| 3 | 20.884978 | 19.223574 |


El **waypoint 3** genera la fuerza más riesgosa: posee la mayor norma euclidiana y el
mayor valor absoluto entre sus componentes. `resolver_multiples_f` reutiliza una sola
factorización y recupera, salvo los errores de truncamiento, los vectores de estado
asociados a cada waypoint:

`[-0.252033, 1.780675, -1e-06, -4e-06, -8e-06, -7e-06, 5e-06, -0.060449, 0.20822, 0.0, 0.0, 2e-06, 2e-06, -2e-06, 0.569833, 1.910636, -1e-06, -1e-06, -3e-06, -3e-06, 2e-06]`

### Número de condición estimado

`κ_estimado(A) ≈ 283.689103`.

Este valor muestra una sensibilidad bastante mayor que la del sistema de rigidez del
Acto 4. Sin embargo, el número de condición es una propiedad del **problema** y no del
algoritmo. Un `κ` elevado limita la precisión que puede esperarse frente a
perturbaciones de entrada, pero un método inestable puede empeorar todavía más el
resultado.

El pivote pequeño `A00=0.0001` no debe confundirse con el número de condición:
el pivote afecta especialmente al proceso de eliminación sin pivotear, mientras que
`κ` describe la sensibilidad del sistema lineal como problema.

### Factor de crecimiento

- Gauss sin pivoteo: **ρ ≈ 4417.853504**
- LU con pivoteo parcial: **ρ ≈ 1.000000**

La diferencia es enorme. Sin pivoteo aparecen números miles de veces mayores que los
de la matriz original; con pivoteo parcial, en esta matriz, no aparece un valor mayor
que el máximo inicial. Como ambos métodos resuelven el mismo sistema y por tanto tienen
el mismo `κ`, la diferencia de `ρ` se atribuye al **método numérico**. Pivotear reduce
el crecimiento porque evita divisiones por pivotes pequeños.

## Acto 4 – Rigidez de la estructura

La solución por Cholesky es:

`[0.999999, 2.0, 2.999999, 4.0, 4.999999, 6.0, 6.999999]`

El número de condición estimado es:

`κ_estimado(K) ≈ 1.584435`.

Comparado con `κ_estimado(A) ≈ 283.689103`, el sistema de rigidez es mucho menos
sensible a la perturbación ensayada en el vector de cargas. En este caso tiene sentido
confiar más en la respuesta de `Kx=F` que en la del sistema `Ax=b`.

### ¿Por qué falla Cholesky si la diagonal se multiplica por -1?

En Cholesky, cada elemento diagonal se obtiene mediante una raíz cuadrada de la forma

`Lii = sqrt(Kii - Σ Lik²)`.

Al hacer negativa la diagonal, el primer radicando ya puede resultar negativo.
Entonces no existe una raíz cuadrada real y la factorización se detiene. Desde el punto
de vista físico, perder la definición positiva significa que la energía elástica ya no
es positiva para toda deformación no nula; aparece una dirección en la que la estructura
no ofrece una rigidez restauradora estable.

### ¿Por qué Cholesky no necesita pivoteo?

Para una matriz real, simétrica y definida positiva, los pivotes de Cholesky son
positivos y la factorización existe sin intercambiar filas. Esa estructura evita el
tipo de pivote peligroso que aparece en Gauss sin pivotear. Además, Cholesky aprovecha
la simetría y trabaja solo con una parte de la matriz, por lo que requiere menos
operaciones que una eliminación general.

## Acto 5 – Precisión en el lazo de control

### Corrección angular

La forma ingenua produce:

`0.0`

La forma estable produce:

`0.5`

Para `Δθ=10^-8`, `cos(Δθ)` queda tan cerca de 1 que la resta `1-cos(Δθ)` pierde sus
dígitos significativos. La identidad

`1-cos(x)=2 sin²(x/2)`

evita restar dos números casi iguales y recupera el valor esperado cercano a **0.5**.

### Torque neto cerca del equilibrio

Con una raíz refinada para aislar el fenómeno de cancelación:

- Torque ingenuo con `δ=0`: `-1.7763568394002505e-15`
- Torque ingenuo con `δ=10^-16`: `-9.769954276528381e-05`
- Torque estable con `δ=10^-16`: `-1.4267213067215282e-15`

La evaluación ingenua entrega prácticamente el mismo valor para `δ=0` y
`δ=10^-16`: la resta de dos torques casi iguales no permite distinguir la señal
producida por la pequeña desviación. Dependiendo del redondeo de la plataforma puede
verse exactamente como cero o como un residuo del orden de la precisión de máquina.

La reformulación estable usa la expansión de Taylor alrededor del equilibrio:

`f(θ*+δ) ≈ f(θ*) + f'(θ*)δ = f'(θ*)δ`,

porque `f(θ*)=0`. Esto evita restar directamente los dos torques casi idénticos y
conserva la variación de primer orden.

Si el controlador trabaja a **1000 Hz**, una pérdida de precisión ocurre potencialmente
en cada milisegundo. Un error aislado puede ser pequeño, pero un sesgo persistente,
oscilaciones o correcciones equivocadas pueden degradar el control. En un brazo que
opera cerca de personas, por eso conviene usar formulaciones numéricamente estables.

## Acto 6 – Opcional: complejidad empírica

Se generaron matrices densas simétricas definidas positivas para poder aplicar los
tres métodos de forma comparable. Los tiempos de referencia medidos en esta ejecución
son:

| n | Gauss (s) | LU (s) | Cholesky (s) |
| --- | --- | --- | --- |
| 5 | 1.712400e-05 | 2.190500e-05 | 6.792000e-06 |
| 10 | 9.698600e-05 | 1.051030e-04 | 2.207700e-05 |
| 20 | 6.578860e-04 | 6.700210e-04 | 1.028340e-04 |
| 40 | 5.463083e-03 | 4.848811e-03 | 5.825350e-04 |


Los valores exactos cambian entre computadores y entre ejecuciones, por lo que deben
interpretarse como una tendencia, no como constantes universales. Al crecer `n`, los
tres tiempos aumentan rápidamente, de forma compatible con una dependencia cúbica.
Gauss y LU tienen costo teórico `O(n^3)`, mientras que Cholesky aprovecha simetría y
definición positiva y requiere aproximadamente una fracción de las operaciones de una
factorización general. La ventaja se vuelve más visible a medida que aumenta `n`.

## Conclusión

La tarea muestra que obtener una solución numérica no basta: también importa **cómo**
se obtiene y cuán sensible es el problema. En calibración, Newton y Secante son mucho
más rápidos que los métodos lineales. En trayectoria, el waypoint 2 es el más cercano
a una singularidad cinemática. En el sistema de fuerzas, el pivote pequeño vuelve
inestable a Gauss sin pivoteo, mientras que LU con pivoteo controla el crecimiento.
La matriz de rigidez es mucho mejor condicionada y permite usar Cholesky de manera
natural. Finalmente, el Acto 5 evidencia que expresiones algebraicamente equivalentes
pueden comportarse de forma muy distinta en aritmética de punto flotante.