# Trabajo autónomo — Sesión 8

**Minería de Datos · 26150 · grupo 020‑83**
**Jueves 3 de septiembre de 2026 · 8–10 a. m.**
**Bloque 2 — Preparación de datos:** normalización y estandarización

---

## Modalidad

**Trabajo autónomo, sin encuentro sincrónico.** El contenido está íntegro en
`S08_Normalizacion.ipynb`, con las explicaciones, el código ejecutado y las dos demostraciones
—el experimento medido y la fuga de información—. Los estudiantes lo recorren y lo aplican
**sobre el dataset de su grupo**, guiados por el enunciado del **Taller 4**.

Las horas de trabajo autónomo hacen parte de la estructura de la asignatura. Esta sesión las usa
para la parte del bloque 2 que se aprende mejor haciendo que escuchando: **decidir si escalar, cuál
transformación aplicar, cómo medir su efecto y dónde ponerla para que no haya fuga**.

**El registro de la sesión es la entrega del taller**, que cierra el domingo 6.

---

## Qué se publica, y cuándo

| Archivo | Cuándo |
|---|---|
| `S08_Normalizacion.ipynb` | **antes de las 8:00** |
| `TALLER_4_MD_2026-3.md` | **antes de las 8:00** |
| `S09_Codificacion.ipynb` | sábado 5, después de la clase |

---

## Qué cubre el taller, y por qué así

El enunciado cambió respecto de la primera versión, y el cambio es de fondo:

**Todos escalan y todos entrenan los tres modelos** —KNN, árbol y Ridge—, cada uno con y sin
escalado. Se eliminó el atajo de «si va con árboles, no necesita escalar».

**Por qué:** el objetivo no es que cada grupo prepare *su* modelo, sino que sepan **a dónde tiene que
llegar cada uno, cómo se mide y para qué sirve**. Un estudiante que solo probó árboles no sabe
reconocer cuándo un KNN está mal preparado.

Y hay un argumento técnico que hace obligatorio el escalado para todos:
**los coeficientes de un modelo lineal solo son comparables entre sí si las variables están en la
misma escala.** Sin escalar, el coeficiente más grande es el de la variable con las unidades más
pequeñas. **La interpretabilidad depende del escalado**, y ese es el eje de la parte D.

---

## La parte D — lo que hay que sostener el sábado

La parte D introduce **interpretabilidad**, que no estaba en el notebook. Pide comparar qué puede
explicar cada modelo:

| Modelo | Qué ofrece |
|---|---|
| Ridge | Coeficientes ordenados — **legibles solo si se escaló** |
| Árbol | `feature_importances_` y reglas en texto, traducibles a español |
| KNN | Nada más que los vecinos usados. **No explica: muestra.** |

**Conviene retomarlo al arrancar el sábado**, en cinco minutos, porque es lo único del taller que el
notebook no desarrolla y donde más se van a equivocar.

---

## Lo demás que el material tiene que sostener solo

Tres puntos del notebook que la lectura rápida se salta:

1. **Escalar no cambia la forma de la distribución.** Los cuatro histogramas lo muestran, pero la
   conclusión hay que decirla: si el problema es la asimetría, la herramienta es el logaritmo.
2. **La fuga de información no da mensaje de error** — el resultado se ve *mejor*. Por eso se
   previene por procedimiento, no por síntoma.
3. **El `Pipeline` como estructura que vuelve imposible el error**, no como forma más elegante de
   escribir lo mismo.

---

## Evaluación

Este trabajo autónomo **no se califica por separado**: se evalúa a través del **Taller 4**, que
cierra el **domingo 6 de septiembre, 11:59 p. m.**

**Al calificar, mirar primero la parte C.2** —la lectura de la tabla de los seis resultados—. Es
donde se ve quién corrió el código y quién entendió lo que salió.
