# Taller 4 — Minería de Datos
### Escalar, medir y comparar: qué hace cada modelo y cuál sabe explicarse

**26150 · grupo 020‑83 · bloque 2**
**Se abre:** jueves 3 de septiembre · **Cierra:** **domingo 6 de septiembre, 11:59 p. m.**
**Entrega:** un notebook por grupo, en Moodle · **Datos: el dataset propio del grupo**

---

## De qué se trata

**Todos escalan y todos prueban los tres modelos.** No hay atajo del tipo «como voy con árboles, me
salto el escalado»: el objetivo no es preparar *su* modelo, es que sepan **a dónde tiene que llegar
cada uno, cómo se mide y para qué sirve**.

Y hay una razón técnica que lo obliga: **los coeficientes de un modelo lineal solo se pueden
comparar entre sí si las variables están en la misma escala.** Sin escalar, el coeficiente más
grande es el de la variable con las unidades más pequeñas, no el de la variable más importante.
La interpretabilidad **depende** del escalado.

> **Lo que se evalúa no es que el código corra.** Es que cada número venga leído. Un notebook lleno
> de celdas verdes sin una sola frase de interpretación **no pasa de 3,0**.

---

## Parte A — El diagnóstico (1,0)

**A.1 (0,6) · La tabla del aporte a la distancia.**
Tomen dos filas cualesquiera y descompongan la distancia euclidiana entre ellas: cuánto aporta cada
variable, en valor absoluto y en **porcentaje del total**. Córranla **antes** de escalar.

**A.2 (0,4) · La lectura.**
¿Qué variable domina, y en qué porcentaje? ¿Es porque de verdad importa más, o solo porque se mide
en unidades más grandes? **Una frase, sobre sus datos.**

---

## Parte B — Las tres transformaciones (1,2)

**B.1 (0,6)** Apliquen **las tres** a su variable de mayor rango: mín‑máx, puntuación z y escalado
robusto. Muestren los cuatro histogramas —original más las tres— juntos.

**B.2 (0,3)** ¿Cambió la **forma** de la distribución? Si su variable es muy asimétrica, apliquen
además el logaritmo y muestren la diferencia.

**B.3 (0,3)** Vuelvan a correr la tabla de A.1 **con los datos estandarizados**. Comparen con la
original: ¿ahora las variables aportan de forma comparable?

---

## Parte C — Los tres modelos, medidos (1,6)

Entrenen **los tres**, cada uno **con y sin escalado**, con la misma partición y la misma semilla.

| Modelo | Qué representa | Qué esperar del escalado |
|---|---|---|
| **KNN** | Se apoya en **distancias** | Debe cambiar, y bastante |
| **Árbol de decisión** | Se apoya en **umbrales** | No debe cambiar |
| **Regresión lineal / Ridge** | Se apoya en **coeficientes** | El desempeño casi no cambia, **pero los coeficientes sí** |

**C.1 (0,8) · La tabla de resultados.** Seis filas: tres modelos × con/sin escalado. Reporten la
métrica adecuada al problema —R² si predicen un número, exactitud y F1 si predicen una
categoría— y **digan por qué escogieron esa métrica**.

**C.2 (0,5) · La lectura de la tabla.** Tres frases, una por modelo, explicando **el resultado que
obtuvieron**, no el que esperaban. Si algo salió distinto a lo previsto, **eso es el hallazgo** y
puntúa igual, siempre que lo expliquen.

**C.3 (0,3) · La fuga de información.** Muestren las dos formas —escalar antes de partir, y escalar
después ajustando solo con entrenamiento— y reporten **la media del conjunto de prueba en los dos
casos**. Expliquen qué significa la diferencia.

---

## Parte D — ¿Cuál sabe explicarse? (0,8)

Aquí está la pregunta que el taller quiere dejar sembrada: **un modelo que acierta pero no puede
explicar por qué, ¿sirve?** Depende de para qué. Averígüenlo con sus datos.

**D.1 (0,4) · Los coeficientes del modelo lineal.**
Muestren los coeficientes del Ridge **entrenado con datos escalados**, ordenados por valor absoluto.
Luego muéstrenlos **sin escalar**. Contesten: **¿por qué solo la primera lista se puede leer?**

**D.2 (0,3) · Lo que dice el árbol.**
Muestren `feature_importances_` y **las primeras dos o tres reglas** del árbol (`export_text` con
`max_depth=2`). Escriban **una regla en español**: *«si X está por encima de tanto, entonces…»*.

**D.3 (0,1) · Lo que dice el KNN.**
¿Puede explicar una predicción individual? Digan qué es lo único que puede mostrar, y por qué eso
no es lo mismo que explicar.

**Y la síntesis, en la tabla:**

| Modelo | ¿Interpretable? | ¿Qué se puede mostrar de una predicción? |
|---|---|---|
| Regresión lineal / Ridge | | |
| Árbol de decisión | | |
| KNN | | |

---

## Parte E — Cierre (0,4)

**Cinco frases máximo**, sobre sus datos y su proyecto:

1. ¿Qué modelo escogerían **y por qué** — desempeño, interpretabilidad, o las dos?
2. Si tuvieran que explicarle una predicción a alguien que no sabe de minería, ¿con cuál lo harían?

---

## Rúbrica — sobre 5,0

| Puntos | Criterio |
|---:|---|
| **1,5** | **La lectura de los números.** Cada tabla y cada gráfico con su interpretación, sobre los datos propios |
| **1,2** | **La tabla de C.1 completa y correcta**, con la métrica justificada |
| **1,0** | **Parte D** — entender que la interpretabilidad depende del escalado, y qué ofrece cada modelo |
| **0,8** | Corrección técnica: las tres transformaciones y los tres modelos bien aplicados |
| **0,5** | Sin fuga: todo se ajusta solo con entrenamiento |

**Descuentos.** Escalar antes de partir en train/test: **−0,8**, sin importar el resto.
Entregar menos de los tres modelos: **−0,5 por cada uno que falte**.
Celdas sin interpretación: −0,15 cada una, hasta −1,0.
Usar el dataset de ejemplo del notebook en vez del propio: **la entrega no se califica**.

---

## Lo que más se va a fallar

1. **Reportar el resultado esperado en vez del obtenido.** Si el árbol se mueve un poco, o el KNN no
   mejora, **repórtenlo y explíquenlo**. Eso puntúa; inventar el resultado del manual, no.
2. **No justificar la métrica.** R² y exactitud no sirven para lo mismo, y con clases
   desbalanceadas la exactitud engaña.
3. **Leer los coeficientes sin escalar.** Es exactamente el error que D.1 quiere hacerles ver.
4. **Poner el escalado fuera del `Pipeline`.** Funciona, y es la puerta de la fuga.

---

## Lo que sigue

La **codificación de categóricas** y el `ColumnTransformer` se ven el **sábado 5** y **no entran en
este taller**. Se aplican en el **Avance 1**, que se entrega y se sustenta el **sábado 19** con
defensa individual.
