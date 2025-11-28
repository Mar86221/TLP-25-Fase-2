# Gramáticas Formales y Algoritmos Modernos: Diseño e Implementación de un Mini-Parser para un Subconjunto del Español

---

**[Nombre Completo del Integrante 1, ID: 00000000]**

**[Nombre Completo del Integrante 2, ID: 00000000]**

**[Nombre Completo del Integrante 3, ID: 00000000]**

---

Departamento de Electrónica e Informática

Universidad Centroamericana José Simeón Cañas

[Código]: Teoría de Lenguajes de Programación

[Nombre del Docente]

[Fecha de Entrega]

---

<div style="page-break-after: always;"></div>

## Resumen Ejecutivo

[Redactar aquí el resumen ejecutivo del proyecto. Este debe ser un párrafo conciso de aproximadamente 150-250 palabras que sintetice:

- El objetivo principal del proyecto.
- La gramática diseñada y el alcance del lenguaje.
- Principales hallazgos de la comparación con herramientas NLP modernas.
- Conclusión principal sobre la aplicabilidad de gramáticas formales.]

---

<div style="page-break-after: always;"></div>

## Diseño y Especificación de la Gramática

### Alcance del Lenguaje Limitado y Vocabulario

[Describir aquí el alcance del subconjunto del español que el parser puede analizar. Extensión sugerida: 1-2 párrafos. Incluir:

- Justificación de las limitaciones elegidas.
- Tipos de oraciones soportadas (simples, compuestas, etc.).]

#### *Vocabulario de Símbolos Terminales*

[Listar aquí las categorías gramaticales (terminales) del vocabulario. Presentar en formato de tabla:]

| Categoría | Símbolo | Ejemplos |
|-----------|---------|----------|
| Sustantivos | [N] | [gato, perro, casa...] |
| Verbos | [V] | [corre, come, duerme...] |
| Artículos | [Art] | [el, la, los, las, un, una...] |
| Adjetivos | [Adj] | [grande, pequeño, rápido...] |
| Preposiciones | [Prep] | [en, con, de, a...] |
| [Agregar...] | [...] | [...] |

### Reglas Sintácticas

[Describir aquí la estructura sintáctica del lenguaje. Extensión sugerida: 1-2 páginas. Explicar:

- Estructura general de las oraciones (S → SN SV).
- Composición del Sintagma Nominal (SN).
- Composición del Sintagma Verbal (SV).
- Reglas para modificadores (adjetivos, adverbios).
- Manejo de oraciones compuestas (si aplica).]

### Definición Formal de la Gramática G

[Presentar aquí la definición formal de la gramática G = (V_N, V_T, P, S). Extensión sugerida: 1 página.]

**G = (V<sub>N</sub>, V<sub>T</sub>, P, S)**

**Donde:**

> V<sub>N</sub> = { [Listar símbolos no terminales: S, SN, SV, ...] }
>
> V<sub>T</sub> = { [Listar símbolos terminales: el, la, gato, perro, corre, ...] }
>
> S = [Símbolo inicial, típicamente 'Oración' u 'O']
>
> P = [Conjunto de producciones - listar cada regla]

**Producciones (P):**

[Listar cada producción en formato BNF o similar, por ejemplo:]

```
O   → SN SV
SN  → Art N | Art N Adj | Art Adj N | ...
SV  → V | V SN | V SN SP | ...
SP  → Prep SN
N   → gato | perro | niña | casa | ...
V   → corre | come | duerme | ve | ...
Art → el | la | los | las | un | una | ...
Adj → grande | pequeño | rápido | rojo | ...
Prep → en | con | de | a | para | ...
```

[Continuar con todas las producciones...]

---

<div style="page-break-after: always;"></div>

## Implementación del Mini-Parser

[Documentar aquí los detalles técnicos de la implementación. Extensión sugerida: 2-3 páginas.]

### Lenguaje y Herramientas Utilizadas

[Especificar el lenguaje de programación elegido (Python, Java, etc.) y justificar la elección. Mencionar bibliotecas o frameworks utilizados.]

### Arquitectura del Parser

[Describir la arquitectura general del sistema:

- Tipo de parser implementado (LL(1), descendente recursivo, etc.).
- Módulo de análisis léxico (tokenizador).
- Módulo de análisis sintáctico.
- Estructura de datos para el árbol de análisis.]

### Algoritmos Clave

[Explicar los algoritmos principales utilizados en el parser. Incluir pseudocódigo o fragmentos de código relevantes si es apropiado. Describir cómo se construye el árbol de derivación.]

```python
# Ejemplo de pseudocódigo o código relevante
def parse_oracion():
    """
    [Describir el algoritmo principal]
    """
    pass
```

### Decisiones de Diseño

[Documentar las decisiones de diseño tomadas durante la implementación y sus justificaciones. Incluir trade-offs considerados.]

---

<div style="page-break-after: always;"></div>

## Pruebas y Resultados del Parser Propio

### Casos de Prueba

[Presentar los casos de prueba utilizados para validar el parser. Extensión sugerida: 1-2 páginas.]

| ID | Oración de Entrada | Resultado Esperado | Resultado Obtenido |
|----|-------------------|-------------------|-------------------|
| 1 | "El gato duerme" | Válida | [Documentar] |
| 2 | "La niña come manzanas" | Válida | [Documentar] |
| 3 | "El perro grande corre rápido" | Válida | [Documentar] |
| 4 | "gato el duerme" | Inválida | [Documentar] |
| 5 | "La casa roja" | [Evaluar] | [Documentar] |
| ... | [Agregar más casos...] | [...] | [...] |

#### *Árboles de Derivación*

[Incluir aquí representaciones visuales o textuales de los árboles de derivación generados para los casos de prueba principales.]

**Ejemplo para "El gato duerme":**

```
            O
           / \
         SN   SV
        / \    |
      Art  N   V
       |   |   |
      el gato duerme
```

[Agregar más árboles de derivación...]

### Manejo de Errores

[Documentar cómo el parser maneja oraciones inválidas. Incluir:

- Tipos de errores detectados.
- Mensajes de error generados.
- Ejemplos de oraciones inválidas y su manejo.]

| Oración Inválida | Tipo de Error | Mensaje Generado |
|-----------------|---------------|------------------|
| "gato el duerme" | [Orden incorrecto] | [Documentar] |
| "El corre" | [Falta sustantivo] | [Documentar] |
| [...] | [...] | [...] |

---

<div style="page-break-after: always;"></div>

## Comparación con Herramienta de NLP Moderna

### Selección de la Herramienta

[Indicar la herramienta NLP seleccionada y justificar la elección. Extensión sugerida: 1 párrafo. Por ejemplo: spaCy, NLTK, Stanford NLP, Stanza, etc.]

#### *Función Utilizada: Dependency Parsing*

[Describir la función específica de la herramienta utilizada para la comparación. Explicar brevemente cómo funciona el dependency parsing o la técnica elegida.]

### Análisis Comparativo

[Realizar el análisis comparativo usando los mismos casos de prueba de la sección anterior. Extensión sugerida: 2-3 páginas.]

#### *Resultados de la Herramienta NLP*

[Presentar los resultados obtenidos con la herramienta NLP para cada caso de prueba. Incluir capturas de pantalla o representaciones del análisis de dependencias si es apropiado.]

**Ejemplo de análisis con [Herramienta]:**

```
[Incluir salida de la herramienta o representación visual]
```

#### *Tabla Comparativa*

| Aspecto | Parser Propio | [Herramienta NLP] | Observaciones |
|---------|--------------|-------------------|---------------|
| Enfoque teórico | CFG/gramática formal | Estadístico/ML | [Documentar] |
| Precisión | [Evaluar] | [Evaluar] | [...] |
| Flexibilidad | [Evaluar] | [Evaluar] | [...] |
| Interpretabilidad | [Evaluar] | [Evaluar] | [...] |
| Manejo de ambigüedad | [Evaluar] | [Evaluar] | [...] |
| Escalabilidad | [Evaluar] | [Evaluar] | [...] |
| Facilidad de modificación | [Evaluar] | [Evaluar] | [...] |
| [Agregar aspectos...] | [...] | [...] | [...] |

#### *Discusión de Resultados*

[Discutir las diferencias observadas entre ambos enfoques. Analizar ventajas y desventajas de cada uno. Reflexionar sobre cuándo es más apropiado usar gramáticas formales vs. herramientas NLP modernas.]

---

<div style="page-break-after: always;"></div>

## Conclusiones

[Redactar las conclusiones generales del proyecto. Extensión sugerida: 1-2 páginas. Incluir:

- Síntesis de los objetivos alcanzados.
- Principales aprendizajes sobre gramáticas formales y su aplicación.
- Reflexión sobre la relevancia de las gramáticas formales en el contexto actual del NLP.
- Limitaciones del proyecto y trabajo futuro.
- Recomendaciones para proyectos similares.]

---

<div style="page-break-after: always;"></div>

## Referencias

[Listar aquí todas las referencias bibliográficas en formato APA 7ª edición. Aplicar sangría francesa. Ordenar alfabéticamente por apellido del autor.]

American Psychological Association. (2020). *Publication manual of the American Psychological Association* (7a. ed.). https://doi.org/10.1037/0000165-000

Chomsky, N. (1956). Three models for the description of language. *IRE Transactions on Information Theory*, *2*(3), 113-124.

[Agregar referencia de la herramienta NLP utilizada...]

[Agregar más referencias según las fuentes consultadas...]

---

<div style="page-break-after: always;"></div>

## Anexos

### Anexo A. Código Fuente del Mini-Parser

[Incluir aquí el código fuente completo del parser o proporcionar el enlace al repositorio (GitHub, GitLab, etc.). Si el código es extenso, incluir solo los módulos principales y referenciar el repositorio para el código completo.]

**Repositorio:** [URL del repositorio]

```python
# Código principal del parser
# [Incluir código aquí o referenciar archivos específicos]
```

### Anexo B. Capturas de Pantalla

[Incluir capturas de pantalla relevantes de la ejecución del parser y de la herramienta NLP. Cada figura debe tener su número y título según formato APA.]

**Figura B1**

*Ejecución del Mini-Parser con caso de prueba exitoso*

[Insertar imagen]

**Figura B2**

*Análisis de dependencias con [Herramienta NLP]*

[Insertar imagen]

### Anexo C. Material Adicional

[Incluir cualquier material adicional que complemente el informe: diagramas de flujo, especificaciones técnicas adicionales, datos de pruebas completos, etc.]

---

*Documento estructurado según APA 7ª edición - Guía UCA*
