# Laboratorio de Combinatoria

Aplicación web interactiva para aprender combinatoria sin memorizar fórmulas. Funciona completamente en el navegador, sin instalación ni conexión a internet (incluye KaTeX local).

**[→ Abrir la aplicación](https://jjdeharo.github.io/labcom/)**

## Qué incluye

- **Lecciones guiadas** — 6 tipos de problemas explicados paso a paso: desde una situación real hasta la fórmula, con construcción interactiva y exploración de todos los casos posibles.
- **¿Qué tipo?** — árbol de decisión de 3 preguntas que identifica el tipo y la fórmula adecuada.
- **Práctica** — 8 enunciados reales para clasificar antes de ver el cálculo.
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
3. **Práctica** — comprueba lo que has aprendido
4. **Laboratorio** — explora libremente

## Idiomas

Español · English · Català · Galego · Euskera

## Tecnología

HTML + CSS + JavaScript en un único archivo `index.html`. Sin dependencias externas en tiempo de ejecución. KaTeX incluido en `vendor/` para renderizar fórmulas matemáticas sin conexión.

## Uso local

Abre `index.html` directamente en el navegador. No necesita servidor.

## Licencia

- Contenido: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)
- Código: [AGPL-3.0](https://www.gnu.org/licenses/agpl-3.0.html)

© [Juan José de Haro](https://bilateria.org)
