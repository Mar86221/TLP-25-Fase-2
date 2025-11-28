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

El mini-parser implementado analiza un subconjunto restringido del español basado en una Gramática Libre de Contexto (CFG). El lenguaje está limitado a oraciones que siguen el patrón Sujeto-Verbo-Objeto (SVO), que es la estructura básica del español. El vocabulario está restringido a aproximadamente 80 palabras distribuidas en cuatro categorías gramaticales: artículos (6 palabras), sustantivos (~20 palabras), adjetivos (~30 palabras) y verbos (~14 palabras), según se define en mini_parser.py líneas 34-52.

**Justificación de las limitaciones:** La gramática fue diseñada con las siguientes restricciones intencionales (README_FASE2.md líneas 43-48): (1) ser suficientemente restrictiva para permitir análisis determinístico mediante parser descendente recursivo, (2) capturar la estructura básica SVO del español para propósitos educativos, (3) ser fácilmente extensible mediante actualización del vocabulario, y (4) permitir validación rápida con complejidad temporal O(n). Las restricciones específicas incluyen: máximo un adjetivo por sintagma nominal, artículo obligatorio en sujeto y complemento, y sin verificación de concordancia de número/género (simplificación intencional).

**Tipos de oraciones soportadas:** El parser solo acepta oraciones simples SVO con estructura: artículo + [adjetivo opcional] + sustantivo + verbo + artículo + [adjetivo opcional] + sustantivo. Permite flexibilidad sintáctica del español al aceptar adjetivos antes o después del sustantivo (mini_parser.py líneas 140-162). No soporta oraciones compuestas, subordinadas, preposiciones, adverbios, ni múltiples adjetivos por sintagma.

#### *Vocabulario de Símbolos Terminales*

El vocabulario completo está definido en mini_parser.py líneas 34-52. La siguiente tabla presenta todas las categorías gramaticales y sus tokens terminales:

| Categoría | Símbolo | Tokens Completos (mini_parser.py) |
|-----------|---------|-----------------------------------|
| Artículos | Art | el, la, un, una, los, las (6 tokens) |
| Sustantivos | N | perro, perros, gato, gatos, niño, niña, niños, niñas, casa, casas, libro, libros, árbol, árboles, computadora, computadoras, carro, carros, hueso, huesos (20 tokens) |
| Adjetivos | Adj | grande, grandes, pequeño, pequeña, pequeños, pequeñas, rojo, roja, rojos, rojas, azul, azules, hermoso, hermosa, hermosos, hermosas, viejo, vieja, viejos, viejas, nuevo, nueva, nuevos, nuevas, rápido, rápida, rápidos, rápidas (30 tokens) |
| Verbos | V | come, comen, lee, leen, ve, ven, quiere, quieren, tiene, tienen, busca, buscan, escribe, escriben, maneja, manejan (16 tokens) |

**Total del vocabulario:** 72 palabras exactas definidas en el código fuente.

### Reglas Sintácticas

La gramática implementada sigue un diseño jerárquico que refleja la estructura básica del español, según se documenta en README_FASE2.md líneas 11-29 y se implementa en mini_parser.py líneas 84-223.

**Estructura general de las oraciones:** Toda oración válida se compone de exactamente dos componentes principales: un sujeto seguido de un predicado (S → SN SV). Esta estructura corresponde al patrón Sujeto-Verbo-Objeto (SVO) característico del español. La implementación se encuentra en el método `parsear_oracion()` (mini_parser.py línea 132-136) que retorna verdadero solo si ambas partes son válidas: `return self.parsear_sujeto() and self.parsear_predicado()`.

**Composición del Sintagma Nominal (Sujeto):** El sujeto debe comenzar obligatoriamente con un artículo, seguido de un sustantivo (mini_parser.py líneas 138-162). La gramática permite tres variantes sintácticas:
1. Artículo + Sustantivo (forma básica): "el perro"
2. Artículo + Adjetivo + Sustantivo (adjetivo antepuesto): "el grande perro"
3. Artículo + Sustantivo + Adjetivo (adjetivo pospuesto): "el perro grande"

Esta flexibilidad refleja la libertad sintáctica del español para colocar adjetivos antes o después del sustantivo. El parser detecta el tipo de token siguiente al artículo y aplica la regla correspondiente. Solo se permite un adjetivo por sintagma nominal.

**Composición del Sintagma Verbal (Predicado):** El predicado se compone de un verbo seguido obligatoriamente de un complemento (mini_parser.py líneas 164-171): `return self.coincidir(TipoToken.VERBO) and self.parsear_complemento()`. No se permiten verbos sin complemento, lo que constituye una restricción de la gramática respecto al español natural.

**Composición del Complemento:** El complemento tiene la misma estructura que el sujeto, siendo esencialmente otro sintagma nominal con las mismas reglas (mini_parser.py líneas 173-197):
1. Artículo + Sustantivo: "un hueso"
2. Artículo + Adjetivo + Sustantivo: "un pequeño hueso"
3. Artículo + Sustantivo + Adjetivo: "un hueso pequeño"

El artículo es obligatorio en el complemento, constituyendo una restricción gramatical (el español permite "come pan" sin artículo, pero esta gramática lo rechaza).

**Reglas para modificadores:** Solo se soportan adjetivos como modificadores. Los adjetivos son opcionales y se limita su uso a uno por sintagma nominal. No se implementan adverbios, preposiciones, ni otros modificadores. El código verifica explícitamente si el token actual es un adjetivo y lo procesa opcionalmente (mini_parser.py líneas 159-160, 194-195).

**Manejo de oraciones compuestas:** La gramática NO soporta oraciones compuestas, coordinadas ni subordinadas. Solo acepta oraciones simples con un único verbo. No se implementan conjunciones (y, o, pero, etc.). Esta es una limitación intencional documentada en README_FASE2.md para mantener la gramática simple y determinística.

### Definición Formal de la Gramática G

La gramática está formalmente especificada en README_FASE2.md líneas 11-29 en notación BNF y documentada en mini_parser.py líneas 88-93. Se presenta a continuación la cuádrupla formal:

**G = (V<sub>N</sub>, V<sub>T</sub>, P, S)**

**Donde:**

> **V<sub>N</sub>** = { oración, sujeto, predicado, complemento, artículo, sustantivo, adjetivo, verbo }
>
> Este conjunto de símbolos no terminales representa las categorías sintácticas de la gramática. Cada uno se deriva en reglas más específicas hasta llegar a los terminales.

> **V<sub>T</sub>** = { el, la, un, una, los, las, perro, perros, gato, gatos, niño, niña, niños, niñas, casa, casas, libro, libros, árbol, árboles, computadora, computadoras, carro, carros, hueso, huesos, grande, grandes, pequeño, pequeña, pequeños, pequeñas, rojo, roja, rojos, rojas, azul, azules, hermoso, hermosa, hermosos, hermosas, viejo, vieja, viejos, viejas, nuevo, nueva, nuevos, nuevas, rápido, rápida, rápidos, rápidas, come, comen, lee, leen, ve, ven, quiere, quieren, tiene, tienen, busca, buscan, escribe, escriben, maneja, manejan }
>
> Total de 72 símbolos terminales según mini_parser.py líneas 34-52.

> **S** = oración
>
> El símbolo inicial es "oración", que constituye el punto de entrada para el proceso de derivación.

> **P** = Conjunto de producciones definido en la sección siguiente

**Producciones (P):**

La especificación completa de las producciones está documentada en README_FASE2.md líneas 11-29 en notación BNF. A continuación se presenta el conjunto completo:

**Reglas de estructura sintáctica:**

```
<oración>     ::= <sujeto> <predicado>
<sujeto>      ::= <artículo> <sustantivo>
                | <artículo> <adjetivo> <sustantivo>
                | <artículo> <sustantivo> <adjetivo>
<predicado>   ::= <verbo> <complemento>
<complemento> ::= <artículo> <sustantivo>
                | <artículo> <adjetivo> <sustantivo>
                | <artículo> <sustantivo> <adjetivo>
```

**Reglas de categorías léxicas (símbolos terminales):**

```
<artículo>    ::= "el" | "la" | "un" | "una" | "los" | "las"

<sustantivo>  ::= "perro" | "perros" | "gato" | "gatos" | "niño" | "niña"
                | "niños" | "niñas" | "casa" | "casas" | "libro" | "libros"
                | "árbol" | "árboles" | "computadora" | "computadoras"
                | "carro" | "carros" | "hueso" | "huesos"

<adjetivo>    ::= "grande" | "grandes" | "pequeño" | "pequeña" | "pequeños"
                | "pequeñas" | "rojo" | "roja" | "rojos" | "rojas" | "azul"
                | "azules" | "hermoso" | "hermosa" | "hermosos" | "hermosas"
                | "viejo" | "vieja" | "viejos" | "viejas" | "nuevo" | "nueva"
                | "nuevos" | "nuevas" | "rápido" | "rápida" | "rápidos"
                | "rápidas"

<verbo>       ::= "come" | "comen" | "lee" | "leen" | "ve" | "ven"
                | "quiere" | "quieren" | "tiene" | "tienen" | "busca"
                | "buscan" | "escribe" | "escriben" | "maneja" | "manejan"
```

**Observaciones sobre las producciones:**

1. La gramática es ambigua en la posición del adjetivo (antes o después del sustantivo), pero el parser resuelve esto mediante análisis determinístico del token siguiente (mini_parser.py líneas 149-161).

2. No existen producciones épsilon (ε) excepto para el adjetivo que es opcional, implementado mediante verificación condicional en el código.

3. La gramática es aproximadamente LL(1) con lookahead limitado, permitiendo parsing descendente recursivo eficiente.

4. Total de producciones: 4 reglas estructurales + 4 reglas léxicas = 8 reglas principales, expandidas a 72 terminales específicos.

---

<div style="page-break-after: always;"></div>

## Implementación del Mini-Parser

[Documentar aquí los detalles técnicos de la implementación. Extensión sugerida: 2-3 páginas.]

### Lenguaje y Herramientas Utilizadas

**Lenguaje de programación:** Python 3.8+ (mini_parser.py líneas 1-9)

**Justificación de la elección:** Python fue seleccionado por las siguientes razones evidenciadas en el código y documentación:

1. **Sintaxis clara y legible** para implementación educativa de conceptos de compiladores (README_FASE2.md enfatiza el propósito educativo del proyecto)

2. **Type hints nativos** (desde Python 3.5+) que permiten especificación de tipos sin sobrecarga de Java, utilizados extensivamente en todo el código: `List[Token]`, `Tuple[bool, List[str]]`, `Optional`, etc. (mini_parser.py líneas 6-7)

3. **Estructuras de datos integradas** como sets para vocabulario (mini_parser.py líneas 34-52) y dataclasses para definición de tokens (línea 21-26)

4. **Sin necesidad de compilación** para facilitar pruebas rápidas durante desarrollo

**Bibliotecas y módulos estándar utilizados:**

| Módulo | Propósito | Ubicación en código |
|--------|-----------|---------------------|
| `typing` | Type hints para anotaciones de tipos (List, Tuple, Optional) | mini_parser.py línea 6 |
| `dataclasses` | Decorador @dataclass para clase Token | mini_parser.py línea 7 |
| `enum` | Enumeración TipoToken para tipos de tokens | mini_parser.py línea 8 |
| `time` | Medición de rendimiento en comparaciones | comparacion_parsers.py línea 6 |
| `unittest` | Framework de testing (24 tests) | test_parser.py línea 6 |

**Dependencias externas (opcionales):**

- **spaCy 3.x** con modelo `es_core_news_sm`: Solo para comparación con NLP moderno (comparacion_parsers.py líneas 13-20), NO requerido para el parser principal
- El núcleo del parser (mini_parser.py) **no tiene dependencias externas**, siendo completamente standalone

**Versión mínima requerida:** Python 3.8+ según documentación en README_FASE2.md y RESUMEN_EJECUTIVO.md

### Arquitectura del Parser

**Tipo de parser implementado:** Parser Descendente Recursivo (Recursive Descent Parser), documentado en mini_parser.py líneas 84-93 y README_FASE2.md líneas 50-79. El parser es de tipo top-down predictivo, aproximadamente LL(1) con lookahead limitado.

**Arquitectura de dos fases:** El sistema implementa la arquitectura clásica de compiladores con separación clara entre análisis léxico y sintáctico (README_FASE2.md líneas 54-65):

```
┌─────────────────────────────────────────────────────────────┐
│                      MiniParser                              │
│                  (Interfaz unificada)                        │
│  ┌────────────────────┐         ┌──────────────────────┐   │
│  │ AnalizadorLéxico   │   →     │ ParserDescendente    │   │
│  │ (Tokenización)     │         │ (Análisis Sintáctico)│   │
│  └────────────────────┘         └──────────────────────┘   │
│          ↓                                  ↓                │
│    Lista de Tokens              Validación booleana         │
│                                 + Lista de errores          │
└─────────────────────────────────────────────────────────────┘
```

**Componente 1: Módulo de Análisis Léxico (AnalizadorLexico)**

Ubicación: mini_parser.py líneas 29-81

**Responsabilidades:**
- Tokenización de texto de entrada (conversión de string a tokens)
- Clasificación de palabras según vocabulario predefinido
- Detección de palabras desconocidas (fuera de vocabulario)
- Asignación de posición a cada token

**Estructuras de datos:**
- Vocabulario almacenado en 4 sets de Python (líneas 34-52) para búsqueda O(1)
- Token: dataclass con campos `tipo: TipoToken`, `valor: str`, `posicion: int` (líneas 21-26)
- TipoToken: enumeración con valores ARTICULO, SUSTANTIVO, ADJETIVO, VERBO, FIN, DESCONOCIDO (líneas 11-18)

**Complejidad:** O(n) donde n es el número de palabras (README_FASE2.md línea 73)

**Componente 2: Módulo de Análisis Sintáctico (ParserDescendenteRecursivo)**

Ubicación: mini_parser.py líneas 84-223

**Responsabilidades:**
- Validación de estructura sintáctica según gramática
- Generación de mensajes de error descriptivos
- Verificación de que todos los tokens son consumidos
- Detección de tokens adicionales al final

**Métodos principales:**
- `parsear_oracion()`: Punto de entrada, valida estructura S → SN SV (línea 132-136)
- `parsear_sujeto()`: Valida sintagma nominal del sujeto (líneas 138-162)
- `parsear_predicado()`: Valida verbo + complemento (líneas 164-171)
- `parsear_complemento()`: Valida sintagma nominal del complemento (líneas 173-197)
- `coincidir()`: Verifica y consume tokens del tipo esperado (líneas 111-130)

**Complejidad:** O(n) para gramática LL(1) (README_FASE2.md línea 79)

**Componente 3: Interfaz Unificada (MiniParser)**

Ubicación: mini_parser.py líneas 226-290

**Responsabilidades:**
- Coordinar análisis léxico y sintáctico
- Proporcionar interfaz simplificada al usuario
- Formatear resultados en estructura de diccionario
- Distinguir entre errores léxicos y sintácticos

**Flujo de ejecución del método `analizar()`** (líneas 233-267):
1. Tokenización con AnalizadorLexico
2. Verificación de tokens desconocidos (fase léxica)
3. Si todo el vocabulario es válido, parsing sintáctico
4. Retorno de diccionario con: valido, fase, texto, tokens, errores

**Estructura de datos para resultados:**

No se construye árbol de análisis explícito (AST). El parser solo valida y retorna:
- `valido`: bool - indica si la oración es válida
- `fase`: str - "léxico" o "sintáctico", indica dónde ocurrió el error
- `texto`: str - oración original
- `tokens`: List[Token] - tokens identificados
- `errores`: List[str] - mensajes de error descriptivos

**Justificación de no construir AST:** El propósito del parser es validación, no traducción o interpretación, por lo que la verificación booleana es suficiente (README_FASE2.md líneas 43-48 sobre diseño educativo)

### Algoritmos Clave

**Algoritmo 1: Tokenización (Análisis Léxico)**

Ubicación: mini_parser.py líneas 54-81

El algoritmo de tokenización convierte una cadena de texto en una lista de tokens clasificados:

```python
def tokenizar(self, texto: str) -> List[Token]:
    """
    Algoritmo de tokenización - mini_parser.py líneas 54-81
    Complejidad: O(n) donde n = número de palabras
    """
    # Paso 1: Normalizar texto (lowercase) y dividir en palabras
    palabras = texto.lower().strip().split()
    tokens = []

    # Paso 2: Clasificar cada palabra según vocabulario
    for i, palabra in enumerate(palabras):
        if palabra in self.articulos:
            tokens.append(Token(TipoToken.ARTICULO, palabra, i))
        elif palabra in self.sustantivos:
            tokens.append(Token(TipoToken.SUSTANTIVO, palabra, i))
        elif palabra in self.adjetivos:
            tokens.append(Token(TipoToken.ADJETIVO, palabra, i))
        elif palabra in self.verbos:
            tokens.append(Token(TipoToken.VERBO, palabra, i))
        else:
            # Palabra no reconocida
            tokens.append(Token(TipoToken.DESCONOCIDO, palabra, i))

    # Paso 3: Agregar token de fin
    tokens.append(Token(TipoToken.FIN, "", len(palabras)))
    return tokens
```

**Características del algoritmo:**
- Búsqueda en sets de Python: O(1) por palabra
- Insensible a mayúsculas/minúsculas (línea 64: `texto.lower()`)
- Retorna DESCONOCIDO para palabras fuera del vocabulario
- Preserva posición original de cada token

**Algoritmo 2: Parser Descendente Recursivo**

Ubicación: mini_parser.py líneas 132-197 y README_FASE2.md líneas 83-103

El algoritmo principal implementa parsing top-down siguiendo la gramática BNF:

```python
def parsear_oracion():
    """
    <oración> ::= <sujeto> <predicado>
    Implementación: mini_parser.py líneas 132-136
    """
    return parsear_sujeto() AND parsear_predicado()

def parsear_sujeto():
    """
    <sujeto> ::= <artículo> <sustantivo>
               | <artículo> <adjetivo> <sustantivo>
               | <artículo> <sustantivo> <adjetivo>
    Implementación: mini_parser.py líneas 138-162
    """
    # Paso 1: Artículo obligatorio
    if NOT coincidir(ARTICULO):
        return False

    # Paso 2: Verificar siguiente token para decidir regla
    if token_actual == ADJETIVO:
        # Regla: artículo + adjetivo + sustantivo
        coincidir(ADJETIVO)
        return coincidir(SUSTANTIVO)

    # Paso 3: Sustantivo obligatorio
    if NOT coincidir(SUSTANTIVO):
        return False

    # Paso 4: Adjetivo opcional después del sustantivo
    if token_actual == ADJETIVO:
        coincidir(ADJETIVO)

    return True

def parsear_predicado():
    """
    <predicado> ::= <verbo> <complemento>
    Implementación: mini_parser.py líneas 164-171
    """
    if NOT coincidir(VERBO):
        return False
    return parsear_complemento()

def parsear_complemento():
    """
    Mismo algoritmo que parsear_sujeto()
    Implementación: mini_parser.py líneas 173-197
    """
    # [Lógica idéntica a parsear_sujeto]
```

**Algoritmo 3: Coincidencia y Avance de Tokens**

Ubicación: mini_parser.py líneas 111-130

Este algoritmo fundamental verifica y consume tokens:

```python
def coincidir(self, tipo_esperado: TipoToken) -> bool:
    """
    Verifica si el token actual coincide con el tipo esperado
    y avanza la posición si hay coincidencia
    """
    if self.token_actual().tipo == tipo_esperado:
        self.avanzar()  # Consumir token
        return True

    # Generar mensaje de error descriptivo
    self.errores.append(
        f"Error en posición {self.posicion}: "
        f"Se esperaba {tipo_esperado.value}, "
        f"pero se encontró {self.token_actual().tipo.value}"
    )
    return False
```

**Propiedades del algoritmo:**
- Lookahead de 1 token (LL(1))
- Backtracking limitado solo para adjetivos opcionales
- Generación automática de mensajes de error con posición
- Avance automático al consumir token

**Algoritmo 4: Validación Post-Parsing**

Ubicación: mini_parser.py líneas 216-221

Verifica que todos los tokens fueron consumidos:

```python
# Después de parsear_oracion()
if exito and self.token_actual().tipo != TipoToken.FIN:
    self.errores.append(
        f"Error: Tokens adicionales después del final de la oración"
    )
    exito = False
```

**Construcción del árbol de derivación:**

El parser NO construye explícitamente un árbol de derivación (AST). La validación se realiza mediante retornos booleanos recursivos. Sin embargo, existe un archivo separado `visualizador_arbol.py` (mencionado en INDEX.md línea 15) que sí construye árboles para propósitos educativos/demostrativos, pero NO es parte del flujo principal del parser.

**Justificación:** Para validación sintáctica pura, la construcción de AST es innecesaria y añadiría overhead de memoria y complejidad (README_FASE2.md líneas 43-48 sobre diseño educativo simplificado).

### Decisiones de Diseño

Las siguientes decisiones de diseño fueron tomadas durante la implementación, fundamentadas en el código fuente y documentación del proyecto:

**Decisión 1: Parser Descendente Recursivo vs Otros Enfoques**

**Elección:** Parser descendente recursivo (mini_parser.py líneas 84-223)

**Justificación:**
- Mapeo directo 1:1 entre reglas gramaticales y métodos (cada no-terminal → un método)
- Código más legible y mantenible que tablas de parsing (README_FASE2.md enfatiza propósito educativo)
- Suficiente para gramática LL(1) simple del proyecto
- No requiere generador de parsers externo (yacc, ANTLR, etc.)

**Trade-offs considerados:**
- ✓ Ventaja: Simplicidad de implementación y comprensión
- ✓ Ventaja: Mensajes de error fáciles de personalizar
- ✗ Desventaja: No escalable a gramáticas complejas con ambigüedad
- ✗ Desventaja: Requiere gramática LL(k) con lookahead limitado

**Decisión 2: Separación en Dos Fases (Léxico + Sintáctico)**

**Elección:** Análisis léxico separado del sintáctico (AnalizadorLexico vs ParserDescendenteRecursivo)

**Justificación:**
- Permite detectar errores léxicos antes de parsing sintáctico (mini_parser.py líneas 247-256)
- Mensajes de error más específicos: "palabra desconocida" vs "estructura inválida"
- Cumple con arquitectura estándar de compiladores
- Facilita extensión del vocabulario sin modificar lógica de parsing

**Evidencia en código:** El método `analizar()` primero verifica tokens desconocidos (fase léxica) y solo si todos son válidos, procede al parsing sintáctico (líneas 244-267)

**Decisión 3: Vocabulario Cerrado con Sets de Python**

**Elección:** Vocabulario almacenado en sets (líneas 34-52) en lugar de archivos externos o bases de datos

**Justificación:**
- Búsqueda O(1) en sets vs O(n) en listas
- Vocabulario pequeño (~72 palabras) cabe en memoria
- No requiere lectura de archivos en cada ejecución
- Facilita portabilidad del código (standalone sin dependencias)

**Trade-offs:**
- ✓ Ventaja: Máxima velocidad de búsqueda
- ✓ Ventaja: Código completamente autónomo
- ✗ Desventaja: Cambiar vocabulario requiere modificar código fuente
- ✗ Desventaja: No escalable a vocabularios de miles de palabras

**Decisión 4: Sin Concordancia de Género/Número**

**Elección:** No validar concordancia (ej: acepta "el gatos" o "la perro")

**Justificación explícita:** README_FASE2.md línea 40 documenta esto como "simplificación intencional"

**Razones:**
- Simplifica gramática (evita multiplicar reglas por género/número)
- Enfoca el proyecto en estructura sintáctica SVO, no morfología
- Mantiene el parser determinístico sin tablas de concordancia
- Suficiente para demostrar conceptos de gramáticas formales

**Trade-offs:**
- ✓ Ventaja: Gramática más simple y clara
- ✓ Ventaja: Parser más rápido (menos validaciones)
- ✗ Desventaja: Acepta oraciones morfológicamente incorrectas
- ✗ Desventaja: No es realista para español completo

**Decisión 5: Adjetivo Opcional Antes o Después del Sustantivo**

**Elección:** Permitir ambas posiciones (mini_parser.py líneas 149-161)

**Justificación:**
- Refleja flexibilidad real del español ("perro grande" = "grande perro")
- Implementado mediante lookahead: verifica token siguiente al artículo
- Máximo un adjetivo por sintagma (restricción documentada)

**Implementación:** El parser verifica `if token_actual == ADJETIVO` después del artículo para decidir la variante de la regla

**Decisión 6: No Construir Árbol de Sintaxis Abstracta (AST)**

**Elección:** Retornar solo validación booleana + errores (mini_parser.py líneas 261-267)

**Justificación:**
- El propósito es **validación**, no interpretación ni traducción
- Ahorra memoria (no almacenar estructura de árbol)
- Respuesta más rápida (menos procesamiento)
- Suficiente para el objetivo educativo del proyecto

**Nota:** Existe `visualizador_arbol.py` separado para visualización educativa, pero NO es parte del flujo principal

**Decisión 7: Type Hints Completos**

**Elección:** Usar anotaciones de tipos en todas las funciones (líneas 6-7: `from typing import List, Tuple, Optional`)

**Justificación:**
- Mejora legibilidad del código (documenta tipos esperados)
- Permite detección de errores con herramientas estáticas (mypy)
- Facilita mantenimiento y extensión del código
- Buena práctica en Python moderno (3.5+)

**Ejemplos en código:**
- `def tokenizar(self, texto: str) -> List[Token]:`
- `def parsear(self, tokens: List[Token]) -> Tuple[bool, List[str]]:`
- `def analizar(self, texto: str) -> dict:`

**Decisión 8: Dataclasses para Tokens**

**Elección:** Usar `@dataclass` para Token (líneas 21-26) en lugar de tuplas o diccionarios

**Justificación:**
- Sintaxis concisa: auto-genera `__init__`, `__repr__`, `__eq__`
- Acceso por nombre: `token.tipo` vs `token[0]` (más legible)
- Type hints integrados en definición
- Inmutable si se necesita (puede agregar `frozen=True`)

**Decisión 9: Mensajes de Error Descriptivos**

**Elección:** Generar mensajes detallados con posición y contexto (líneas 125-129)

**Formato:** `"Error en posición X: Se esperaba Y, pero se encontró Z (valor)"`

**Justificación:**
- Facilita debugging para usuarios del parser
- Indica exactamente dónde y qué falló
- Más útil que simple "sintaxis inválida"
- Propósito educativo: enseñar qué está mal

**Decisión 10: Artículo Obligatorio en Sujeto y Complemento**

**Elección:** Exigir artículo siempre (mini_parser.py líneas 145, 180)

**Justificación:**
- Simplifica gramática (evita casos especiales)
- Mantiene estructura predecible: siempre Art + N + [Adj]
- Facilita parsing determinístico
- Trade-off aceptable para lenguaje limitado

**Restricción respecto al español real:** El español permite "come pan" sin artículo, pero esta gramática lo rechaza (documentado como limitación intencional)

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
