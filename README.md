# Laboratorio de Combinatoria

Aplicación web interactiva para aprender combinatoria sin memorizar fórmulas. Funciona completamente en el navegador, sin instalación ni conexión a internet (incluye KaTeX local).

**[→ Abrir la aplicación](https://jjdeharo.github.io/labcom/)**

## Qué incluye

- **Lecciones guiadas** — 6 tipos de problemas explicados paso a paso: desde una situación real hasta la fórmula, con construcción interactiva y exploración de todos los casos posibles.
- **¿Qué tipo?** — árbol de decisión de 3 preguntas que identifica el tipo y la fórmula adecuada.
- **Práctica** — banco de más de 230 enunciados reales. Cada ejercicio se resuelve en cuatro pasos: clasificar el tipo, identificar n y k, elegir la fórmula y verificar el resultado. Incluye dos modos:
  - **Sistema inteligente de problemas** — primero diagnostica el nivel en cada tipo (2 ejercicios por tipo, 12 en total) y después refuerza los más débiles, usando un modelo adaptativo bayesiano formativo con ganancia de información (IRT heurístico + entropía de Shannon). Un indicador de fase (diagnóstica / refuerzo) es visible en todo momento.
  - **Selección manual** — elige uno o varios tipos concretos para practicarlos.
  - **Panel de progreso** — muestra la probabilidad estimada de acierto por tipo con barras de color codificadas (🔴 Iniciando · 🟡 En proceso · 🟢 Dominado).
  - **Informe de práctica** — al terminar el diagnóstico se genera un informe con el nivel inicial por tipo, puntos fuertes, debilidades y una recomendación personalizada. Durante la fase de refuerzo el informe se actualiza y muestra la comparativa de progreso (nivel al terminar el diagnóstico vs. nivel actual).
  - **Diagnóstico por habilidad** — además del nivel por tipo, el informe muestra en qué *paso* del proceso acierta o falla el alumno, en dos bloques: *lectura del enunciado* (¿importa el orden?, ¿se usan todos los elementos?, ¿hay repetición?) y *pasos de resolución* (nombrar el tipo, identificar *n* y *k*, elegir la fórmula), cada uno con su semáforo 🔴/🟡/🟢. Es un corte complementario al nivel por tipo: indica *en qué falla*, no solo *con qué tipo de problema*.
- **Laboratorio** — ajusta *n* y *k* en tiempo real y visualiza todas las posibilidades.
- **Tabla resumen** — los 6 tipos con las tres preguntas clave y las fórmulas.

## Tipos de problemas cubiertos

| Tipo | Fórmula |
|------|---------|
| Permutación | $P_n = n!$ |
| Permutación con repetición | $P = \dfrac{n!}{a!\,b!\cdots}$ |
| Variación | $V_{n,k} = \dfrac{n!}{(n-k)!}$ |
| Variación con repetición | $VR_{n,k} = n^k$ |
| Combinación | $C_{n,k} = \dbinom{n}{k}$ |
| Combinación con repetición | $CR_{n,k} = \dbinom{n+k-1}{k}$ |

## Ruta de aprendizaje recomendada

1. **Lecciones** — aprende cada tipo paso a paso
2. **¿Qué tipo?** — identifica el tipo cuando tengas un enunciado real
3. **Práctica** — comprueba y refuerza lo que has aprendido
4. **Laboratorio** — explora libremente

## Nota sobre el sistema adaptativo

La práctica usa probabilidades para orientar la selección de ejercicios, no para emitir una calificación psicométrica. El modelo mantiene una estimación separada por tipo de problema y la actualiza con una puntuación parcial del ejercicio, ponderada entre cuatro componentes: lectura de los parámetros que definen el tipo (las tres preguntas sobre orden, alcance y repetición, con crédito parcial) 20 %, clasificación del tipo 20 %, identificación de \(n\) y \(k\) 30 %, y elección de la fórmula 30 %. El resultado numérico final del ejercicio no interviene en la puntuación. Los parámetros IRT se usan como heurística inicial de dificultad; no proceden de una calibración empírica con alumnado.

En paralelo, y solo con fines de diagnóstico (no influye en la selección de ejercicios), el modelo mantiene una segunda estimación bayesiana **por habilidad transversal** —independiente del tipo de problema— para cada uno de los seis pasos: las tres preguntas de lectura del enunciado y los tres pasos de resolución (tipo, *n* y *k*, fórmula). Esto permite localizar en qué paso concreto falla el alumno, de forma complementaria a la estimación por tipo.

**Cómo leer los porcentajes.** Cada % no es el porcentaje de aciertos del alumno, sino la probabilidad estimada de que acierte ese paso en un problema de dificultad media, derivada de la creencia bayesiana sobre su nivel. Por eso no llega al 100 % ni baja a 0: cada paso tiene un **suelo de adivinación** que refleja la probabilidad de acertar al azar — **1/2** en las preguntas de sí/no y en la identificación de *n* y *k* (el enunciado muestra dos números que basta con asignar), y **1/6** en la elección del tipo y de la fórmula (seis opciones). Como consecuencia, los porcentajes de pasos con distinto suelo no son directamente comparables entre sí; el juicio de dominio (🔴/🟡/🟢) se basa en el **nivel estimado**, no en el porcentaje mostrado.

**Qué es el nivel estimado.** El modelo no guarda un recuento de aciertos, sino una creencia sobre el dominio del alumno repartida entre tres hipótesis —*no aprendido*, *aprendiendo* y *dominado*— en una escala interna. Esa creencia empieza repartida por igual y cada ejercicio la desplaza mediante la regla de Bayes (un acierto mueve probabilidad hacia «dominado»; un fallo, hacia «no aprendido»). El nivel estimado es el valor medio de esa creencia, y el semáforo lo traduce a 🔴/🟡/🟢. El porcentaje y el nivel son dos vistas de la misma creencia: el porcentaje es la probabilidad de acertar en un problema típico (depende del suelo de adivinación), mientras que el nivel sitúa al alumno en la escala de dominio y, al no depender del suelo, sí es comparable entre todos los pasos.

El diseño sigue el enfoque descrito en [Recursos educativos adaptativos bayesianos](https://jjdeharo.github.io/recursos-adaptativos/): inferencia bayesiana para actualizar el estado estimado del alumno, entropía de Shannon para medir incertidumbre y selección adaptativa de ejercicios combinando información diagnóstica con utilidad pedagógica.

## Idiomas

Español · English · Català · Galego · Euskera

## Tecnología

HTML + CSS + JavaScript en un único archivo `index.html`. Sin dependencias externas en tiempo de ejecución. KaTeX incluido en `vendor/` para renderizar fórmulas matemáticas sin conexión.

## Uso local

Requiere un servidor local porque la práctica carga `problems.json` mediante `fetch()`. La forma más sencilla:

```bash
python -m http.server
```

Y abre `http://localhost:8000` en el navegador. Alternativamente usa la [versión en línea](https://jjdeharo.github.io/labcom/).

## Sugerencias y problemas

Abre un [issue en GitHub](https://github.com/jjdeharo/labcom/issues).

## Licencia

- Contenido: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)
- Código: [AGPL-3.0](https://www.gnu.org/licenses/agpl-3.0.html)

© [Juan José de Haro](https://bilateria.org)
