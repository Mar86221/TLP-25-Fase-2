## Registro de ejecuciones

````markdown
PS C:\Users\luism\Desktop\TEO SEGUNDA FASE> wsl
lm@DESKTOP-KKSL5JU:/mnt/c/Users/luism/Desktop/TEO SEGUNDA FASE$ python3 mini_parser.py
============================================================
MINI-PARSER PARA LENGUAJE NATURAL LIMITADO
Parser Descendente Recursivo - Gramática Libre de Contexto
============================================================

============================================================
CASOS DE PRUEBA VÁLIDOS
============================================================

============================================================
Texto analizado: 'el perro come un hueso'
============================================================

Tokens identificados:
  [ARTICULO    ] -> 'el'
  [SUSTANTIVO  ] -> 'perro'
  [VERBO       ] -> 'come'
  [ARTICULO    ] -> 'un'
  [SUSTANTIVO  ] -> 'hueso'

✓ ORACIÓN VÁLIDA - La estructura cumple con la gramática
============================================================


============================================================
Texto analizado: 'la niña lee el libro'
============================================================

Tokens identificados:
  [ARTICULO    ] -> 'la'
  [SUSTANTIVO  ] -> 'niña'
  [VERBO       ] -> 'lee'
  [ARTICULO    ] -> 'el'
  [SUSTANTIVO  ] -> 'libro'

✓ ORACIÓN VÁLIDA - La estructura cumple con la gramática
============================================================


============================================================
Texto analizado: 'un gato grande ve la casa'
============================================================

Tokens identificados:
  [ARTICULO    ] -> 'un'
  [SUSTANTIVO  ] -> 'gato'
  [ADJETIVO    ] -> 'grande'
  [VERBO       ] -> 've'
  [ARTICULO    ] -> 'la'
  [SUSTANTIVO  ] -> 'casa'

✓ ORACIÓN VÁLIDA - La estructura cumple con la gramática
============================================================


============================================================
Texto analizado: 'el niño pequeño quiere un libro rojo'
============================================================

Tokens identificados:
  [ARTICULO    ] -> 'el'
  [SUSTANTIVO  ] -> 'niño'
  [ADJETIVO    ] -> 'pequeño'
  [VERBO       ] -> 'quiere'
  [ARTICULO    ] -> 'un'
  [SUSTANTIVO  ] -> 'libro'
  [ADJETIVO    ] -> 'rojo'

✓ ORACIÓN VÁLIDA - La estructura cumple con la gramática
============================================================


============================================================
Texto analizado: 'una computadora nueva tiene el carro'
============================================================

Tokens identificados:
  [ARTICULO    ] -> 'una'
  [SUSTANTIVO  ] -> 'computadora'
  [ADJETIVO    ] -> 'nueva'
  [VERBO       ] -> 'tiene'
  [ARTICULO    ] -> 'el'
  [SUSTANTIVO  ] -> 'carro'

✓ ORACIÓN VÁLIDA - La estructura cumple con la gramática
============================================================


============================================================
Texto analizado: 'los perros buscan las casas'
============================================================

Tokens identificados:
  [ARTICULO    ] -> 'los'
  [SUSTANTIVO  ] -> 'perros'
  [VERBO       ] -> 'buscan'
  [ARTICULO    ] -> 'las'
  [SUSTANTIVO  ] -> 'casas'

✓ ORACIÓN VÁLIDA - La estructura cumple con la gramática
============================================================


============================================================
CASOS DE PRUEBA INVÁLIDOS
============================================================

============================================================
Texto analizado: 'el perro grande'
============================================================

Tokens identificados:
  [ARTICULO    ] -> 'el'
  [SUSTANTIVO  ] -> 'perro'
  [ADJETIVO    ] -> 'grande'

✗ ORACIÓN INVÁLIDA - Error en fase de análisis sintáctico

Errores encontrados:
  • Error en posición 3: Se esperaba VERBO, pero se encontró FIN ('')
============================================================


============================================================
Texto analizado: 'come el libro'
============================================================

Tokens identificados:
  [VERBO       ] -> 'come'
  [ARTICULO    ] -> 'el'
  [SUSTANTIVO  ] -> 'libro'

✗ ORACIÓN INVÁLIDA - Error en fase de análisis sintáctico

Errores encontrados:
  • Error en posición 0: Se esperaba ARTICULO, pero se encontró VERBO ('come')
============================================================


============================================================
Texto analizado: 'el grande perro come libro'
============================================================

Tokens identificados:
  [ARTICULO    ] -> 'el'
  [ADJETIVO    ] -> 'grande'
  [SUSTANTIVO  ] -> 'perro'
  [VERBO       ] -> 'come'
  [SUSTANTIVO  ] -> 'libro'

✗ ORACIÓN INVÁLIDA - Error en fase de análisis sintáctico

Errores encontrados:
  • Error en posición 4: Se esperaba ARTICULO, pero se encontró SUSTANTIVO ('libro')
============================================================


============================================================
Texto analizado: 'perro el come un libro'
============================================================

Tokens identificados:
  [SUSTANTIVO  ] -> 'perro'
  [ARTICULO    ] -> 'el'
  [VERBO       ] -> 'come'
  [ARTICULO    ] -> 'un'
  [SUSTANTIVO  ] -> 'libro'

✗ ORACIÓN INVÁLIDA - Error en fase de análisis sintáctico

Errores encontrados:
  • Error en posición 0: Se esperaba ARTICULO, pero se encontró SUSTANTIVO ('perro')
============================================================


============================================================
Texto analizado: 'el perro muy grande come el libro'
============================================================

Tokens identificados:
  [ARTICULO    ] -> 'el'
  [SUSTANTIVO  ] -> 'perro'
  [DESCONOCIDO ] -> 'muy'
  [ADJETIVO    ] -> 'grande'
  [VERBO       ] -> 'come'
  [ARTICULO    ] -> 'el'
  [SUSTANTIVO  ] -> 'libro'

✗ ORACIÓN INVÁLIDA - Error en fase de análisis léxico

Errores encontrados:
  • Palabra desconocida: 'muy'
============================================================


============================================================
Texto analizado: 'python es genial'
============================================================

Tokens identificados:
  [DESCONOCIDO ] -> 'python'
  [DESCONOCIDO ] -> 'es'
  [DESCONOCIDO ] -> 'genial'

✗ ORACIÓN INVÁLIDA - Error en fase de análisis léxico

Errores encontrados:
  • Palabra desconocida: 'python'
  • Palabra desconocida: 'es'
  • Palabra desconocida: 'genial'
============================================================


============================================================
Texto analizado: 'el libro azul hermoso lee la niña'
============================================================

Tokens identificados:
  [ARTICULO    ] -> 'el'
  [SUSTANTIVO  ] -> 'libro'
  [ADJETIVO    ] -> 'azul'
  [ADJETIVO    ] -> 'hermoso'
  [VERBO       ] -> 'lee'
  [ARTICULO    ] -> 'la'
  [SUSTANTIVO  ] -> 'niña'

✗ ORACIÓN INVÁLIDA - Error en fase de análisis sintáctico

Errores encontrados:
  • Error en posición 3: Se esperaba VERBO, pero se encontró ADJETIVO ('hermoso')
============================================================

lm@DESKTOP-KKSL5JU:/mnt/c/Users/luism/Desktop/TEO SEGUNDA FASE$ python3 comparacion_parsers.py
================================================================================
VERIFICACIÓN DE DEPENDENCIAS
================================================================================
✓ spaCy y modelo es_core_news_sm disponibles


================================================================================
FASE 2: COMPARACIÓN DE PARSERS
Parser Descendente Recursivo vs Modelo NLP Moderno (spaCy)
================================================================================

================================================================================
COMPARACIÓN DETALLADA: PARSER MANUAL VS NLP MODERNO
================================================================================

────────────────────────────────────────────────────────────────────────────────
Caso 1: "el perro come un hueso"
────────────────────────────────────────────────────────────────────────────────

📋 PARSER MANUAL (Gramática Formal):
   ✓ VÁLIDO - Cumple gramática SVO definida
   ⏱ Tiempo: 0.0343 ms

🤖 PARSER NLP (spaCy - Deep Learning):
   Estructura SVO detectada: ✓ Sí
   • Sujeto: ✓
   • Verbo: ✓
   • Objeto: ✓
   ⏱ Tiempo: 35.0401 ms
   POS Tags: el:DET perro:PROPN come:VERB un:DET hueso:NOUN

────────────────────────────────────────────────────────────────────────────────
Caso 2: "la niña lee el libro"
────────────────────────────────────────────────────────────────────────────────

📋 PARSER MANUAL (Gramática Formal):
   ✓ VÁLIDO - Cumple gramática SVO definida
   ⏱ Tiempo: 0.0362 ms

🤖 PARSER NLP (spaCy - Deep Learning):
   Estructura SVO detectada: ✓ Sí
   • Sujeto: ✓
   • Verbo: ✓
   • Objeto: ✓
   ⏱ Tiempo: 4.4870 ms
   POS Tags: la:DET niña:NOUN lee:VERB el:DET libro:NOUN

────────────────────────────────────────────────────────────────────────────────
Caso 3: "un gato grande ve la casa"
────────────────────────────────────────────────────────────────────────────────

📋 PARSER MANUAL (Gramática Formal):
   ✓ VÁLIDO - Cumple gramática SVO definida
   ⏱ Tiempo: 0.0305 ms

🤖 PARSER NLP (spaCy - Deep Learning):
   Estructura SVO detectada: ✓ Sí
   • Sujeto: ✓
   • Verbo: ✓
   • Objeto: ✓
   ⏱ Tiempo: 3.7742 ms
   POS Tags: un:DET gato:NOUN grande:ADJ ve:VERB la:DET casa:NOUN

────────────────────────────────────────────────────────────────────────────────
Caso 4: "el niño pequeño quiere un libro rojo"
────────────────────────────────────────────────────────────────────────────────

📋 PARSER MANUAL (Gramática Formal):
   ✓ VÁLIDO - Cumple gramática SVO definida
   ⏱ Tiempo: 0.0334 ms

🤖 PARSER NLP (spaCy - Deep Learning):
   Estructura SVO detectada: ✓ Sí
   • Sujeto: ✓
   • Verbo: ✓
   • Objeto: ✓
   ⏱ Tiempo: 4.2162 ms
   POS Tags: el:DET niño:NOUN pequeño:ADJ quiere:VERB un:DET libro:NOUN rojo:ADJ

────────────────────────────────────────────────────────────────────────────────
Caso 5: "el perro come"
────────────────────────────────────────────────────────────────────────────────

📋 PARSER MANUAL (Gramática Formal):
   ✗ INVÁLIDO - Error en fase sintáctico
   ⏱ Tiempo: 0.0451 ms

🤖 PARSER NLP (spaCy - Deep Learning):
   Estructura SVO detectada: ✗ No
   • Sujeto: ✓
   • Verbo: ✗
   • Objeto: ✗
   ⏱ Tiempo: 3.4764 ms
   POS Tags: el:DET perro:PROPN come:PROPN

────────────────────────────────────────────────────────────────────────────────
Caso 6: "come el libro"
────────────────────────────────────────────────────────────────────────────────

📋 PARSER MANUAL (Gramática Formal):
   ✗ INVÁLIDO - Error en fase sintáctico
   ⏱ Tiempo: 0.0315 ms

🤖 PARSER NLP (spaCy - Deep Learning):
   Estructura SVO detectada: ✗ No
   • Sujeto: ✗
   • Verbo: ✓
   • Objeto: ✓
   ⏱ Tiempo: 3.8407 ms
   POS Tags: come:VERB el:DET libro:NOUN

────────────────────────────────────────────────────────────────────────────────
Caso 7: "el grande perro come libro"
────────────────────────────────────────────────────────────────────────────────

📋 PARSER MANUAL (Gramática Formal):
   ✗ INVÁLIDO - Error en fase sintáctico
   ⏱ Tiempo: 0.0343 ms

🤖 PARSER NLP (spaCy - Deep Learning):
   Estructura SVO detectada: ✗ No
   • Sujeto: ✓
   • Verbo: ✗
   • Objeto: ✓
   ⏱ Tiempo: 3.7704 ms
   POS Tags: el:DET grande:ADJ perro:PROPN come:PROPN libro:NOUN

────────────────────────────────────────────────────────────────────────────────
Caso 8: "el estudiante estudia matemáticas"
────────────────────────────────────────────────────────────────────────────────

📋 PARSER MANUAL (Gramática Formal):
   ✗ INVÁLIDO - Error en fase léxico
   ⏱ Tiempo: 0.0188 ms

🤖 PARSER NLP (spaCy - Deep Learning):
   Estructura SVO detectada: ✓ Sí
   • Sujeto: ✓
   • Verbo: ✓
   • Objeto: ✓
   ⏱ Tiempo: 4.0927 ms
   POS Tags: el:DET estudiante:NOUN estudia:VERB matemáticas:ADJ

────────────────────────────────────────────────────────────────────────────────
Caso 9: "python es un lenguaje de programación"
────────────────────────────────────────────────────────────────────────────────

📋 PARSER MANUAL (Gramática Formal):
   ✗ INVÁLIDO - Error en fase léxico
   ⏱ Tiempo: 0.0219 ms

🤖 PARSER NLP (spaCy - Deep Learning):
   Estructura SVO detectada: ✗ No
   • Sujeto: ✓
   • Verbo: ✓
   • Objeto: ✗
   ⏱ Tiempo: 3.8664 ms
   POS Tags: python:VERB es:AUX un:DET lenguaje:NOUN de:ADP programación:NOUN

────────────────────────────────────────────────────────────────────────────────
Caso 10: "la inteligencia artificial avanza rápidamente"
────────────────────────────────────────────────────────────────────────────────

📋 PARSER MANUAL (Gramática Formal):
   ✗ INVÁLIDO - Error en fase léxico
   ⏱ Tiempo: 0.0219 ms

🤖 PARSER NLP (spaCy - Deep Learning):
   Estructura SVO detectada: ✗ No
   • Sujeto: ✓
   • Verbo: ✓
   • Objeto: ✗
   ⏱ Tiempo: 3.7551 ms
   POS Tags: la:DET inteligencia:NOUN artificial:ADJ avanza:VERB rápidamente:ADV

────────────────────────────────────────────────────────────────────────────────
Caso 11: "el perro muy grande come el libro azul"
────────────────────────────────────────────────────────────────────────────────

📋 PARSER MANUAL (Gramática Formal):
   ✗ INVÁLIDO - Error en fase léxico
   ⏱ Tiempo: 0.0260 ms

🤖 PARSER NLP (spaCy - Deep Learning):
   Estructura SVO detectada: ✓ Sí
   • Sujeto: ✓
   • Verbo: ✓
   • Objeto: ✓
   ⏱ Tiempo: 3.8662 ms
   POS Tags: el:DET perro:NOUN muy:ADV grande:ADJ come:VERB el:DET libro:NOUN azul:ADJ

────────────────────────────────────────────────────────────────────────────────
Caso 12: "los gatos negros cazan ratones pequeños"
────────────────────────────────────────────────────────────────────────────────

📋 PARSER MANUAL (Gramática Formal):
   ✗ INVÁLIDO - Error en fase léxico
   ⏱ Tiempo: 0.0255 ms

🤖 PARSER NLP (spaCy - Deep Learning):
   Estructura SVO detectada: ✓ Sí
   • Sujeto: ✓
   • Verbo: ✓
   • Objeto: ✓
   ⏱ Tiempo: 5.2762 ms
   POS Tags: los:DET gatos:NOUN negros:ADJ cazan:VERB ratones:NOUN pequeños:ADJ


================================================================================
RESUMEN ESTADÍSTICO
================================================================================

📊 PARSER MANUAL:
   • Oraciones válidas: 4/12 (33.3%)
   • Oraciones inválidas: 8/12 (66.7%)
     - Errores léxicos: 5
     - Errores sintácticos: 3
   • Tiempo total: 0.3595 ms
   • Tiempo promedio: 0.0300 ms/oración

🤖 PARSER NLP (spaCy):
   • Con estructura SVO: 7/12 (58.3%)
   • Sin estructura SVO: 5/12 (41.7%)
   • Tiempo total: 79.4616 ms
   • Tiempo promedio: 6.6218 ms/oración


================================================================================
ANÁLISIS COMPARATIVO
================================================================================

⚡ DESEMPEÑO:
   • Parser Manual es 221.01x más rápido que spaCy

🎯 PRECISIÓN:
   • Parser Manual: Verifica gramática formal estricta (SVO con vocabulario limitado)
   • spaCy: Identifica dependencias sintácticas en lenguaje natural general

📝 FORTALEZAS Y DEBILIDADES:

   Parser Manual:
   ✓ Extremadamente rápido
   ✓ Reglas explícitas y comprensibles
   ✓ Ideal para lenguajes de dominio específico
   ✗ Vocabulario muy limitado
   ✗ No maneja variaciones del lenguaje natural
   ✗ Requiere mantenimiento manual de reglas

   Parser NLP (spaCy):
   ✓ Maneja vocabulario ilimitado
   ✓ Robusto ante variaciones lingüísticas
   ✓ Pre-entrenado en corpus masivos
   ✓ Identifica entidades, lemas, dependencias
   ✗ Más lento (requiere inferencia neural)
   ✗ Menos interpretable (caja negra)
   ✗ Requiere recursos computacionales mayores

================================================================================

lm@DESKTOP-KKSL5JU:/mnt/c/Users/luism/Desktop/TEO SEGUNDA FASE$ python3 visualizador_arbol.py

======================================================================
VISUALIZADOR DE ÁRBOLES DE PARSING
======================================================================
======================================================================
ANÁLISIS PASO A PASO: 'el perro come un hueso'
======================================================================

📍 PASO 1: ANÁLISIS LÉXICO (Tokenización)
----------------------------------------------------------------------
  Token 1: [ARTICULO    ] → 'el'
  Token 2: [SUSTANTIVO  ] → 'perro'
  Token 3: [VERBO       ] → 'come'
  Token 4: [ARTICULO    ] → 'un'
  Token 5: [SUSTANTIVO  ] → 'hueso'

📍 PASO 2: ANÁLISIS SINTÁCTICO
----------------------------------------------------------------------
  ✓ La oración es sintácticamente válida

  Reglas aplicadas:
  1. <oración> → <sujeto> <predicado>
  2. <sujeto> → <artículo> <sustantivo>
  3. <predicado> → <verbo> <complemento>
  4. <complemento> → <artículo> <sustantivo>

📍 PASO 3: ÁRBOL DE DERIVACIÓN
----------------------------------------------------------------------
ORACIÓN
├── SUJETO
│   ├── ARTÍCULO: "el"
│   └── SUSTANTIVO: "perro"
└── PREDICADO
    ├── VERBO: "come"
    └── COMPLEMENTO
        ├── ARTÍCULO: "un"
        └── SUSTANTIVO: "hueso"

======================================================================


======================================================================
ANÁLISIS PASO A PASO: 'la niña pequeña lee el libro rojo'
======================================================================

📍 PASO 1: ANÁLISIS LÉXICO (Tokenización)
----------------------------------------------------------------------
  Token 1: [ARTICULO    ] → 'la'
  Token 2: [SUSTANTIVO  ] → 'niña'
  Token 3: [ADJETIVO    ] → 'pequeña'
  Token 4: [VERBO       ] → 'lee'
  Token 5: [ARTICULO    ] → 'el'
  Token 6: [SUSTANTIVO  ] → 'libro'
  Token 7: [ADJETIVO    ] → 'rojo'

📍 PASO 2: ANÁLISIS SINTÁCTICO
----------------------------------------------------------------------
  ✓ La oración es sintácticamente válida

  Reglas aplicadas:
  1. <oración> → <sujeto> <predicado>
  2. <sujeto> → <artículo> [<adjetivo>] <sustantivo>
  3. <predicado> → <verbo> <complemento>
  4. <complemento> → <artículo> [<adjetivo>] <sustantivo>

📍 PASO 3: ÁRBOL DE DERIVACIÓN
----------------------------------------------------------------------
ORACIÓN
├── SUJETO
│   ├── ARTÍCULO: "la"
│   ├── SUSTANTIVO: "niña"
│   └── ADJETIVO: "pequeña"
└── PREDICADO
    ├── VERBO: "lee"
    └── COMPLEMENTO
        ├── ARTÍCULO: "el"
        ├── SUSTANTIVO: "libro"
        └── ADJETIVO: "rojo"

======================================================================


======================================================================
ANÁLISIS PASO A PASO: 'un gato ve la casa'
======================================================================

📍 PASO 1: ANÁLISIS LÉXICO (Tokenización)
----------------------------------------------------------------------
  Token 1: [ARTICULO    ] → 'un'
  Token 2: [SUSTANTIVO  ] → 'gato'
  Token 3: [VERBO       ] → 've'
  Token 4: [ARTICULO    ] → 'la'
  Token 5: [SUSTANTIVO  ] → 'casa'

📍 PASO 2: ANÁLISIS SINTÁCTICO
----------------------------------------------------------------------
  ✓ La oración es sintácticamente válida

  Reglas aplicadas:
  1. <oración> → <sujeto> <predicado>
  2. <sujeto> → <artículo> <sustantivo>
  3. <predicado> → <verbo> <complemento>
  4. <complemento> → <artículo> <sustantivo>

📍 PASO 3: ÁRBOL DE DERIVACIÓN
----------------------------------------------------------------------
ORACIÓN
├── SUJETO
│   ├── ARTÍCULO: "un"
│   └── SUSTANTIVO: "gato"
└── PREDICADO
    ├── VERBO: "ve"
    └── COMPLEMENTO
        ├── ARTÍCULO: "la"
        └── SUSTANTIVO: "casa"

======================================================================


======================================================================
ANÁLISIS PASO A PASO: 'el perro grande'
======================================================================

📍 PASO 1: ANÁLISIS LÉXICO (Tokenización)
----------------------------------------------------------------------
  Token 1: [ARTICULO    ] → 'el'
  Token 2: [SUSTANTIVO  ] → 'perro'
  Token 3: [ADJETIVO    ] → 'grande'

📍 PASO 2: ANÁLISIS SINTÁCTICO
----------------------------------------------------------------------
  ✗ La oración NO es válida
  Fase de error: sintáctico

  Errores detectados:
    • Error en posición 3: Se esperaba VERBO, pero se encontró FIN ('')

======================================================================


lm@DESKTOP-KKSL5JU:/mnt/c/Users/luism/Desktop/TEO SEGUNDA FASE$ python3 test_parser.py
======================================================================
SUITE DE TESTS - MINI-PARSER
======================================================================

test_mayusculas_minusculas (__main__.TestAnalizadorLexico)
Test insensibilidad a mayúsculas ... ok
test_palabra_desconocida (__main__.TestAnalizadorLexico)
Test detección de palabras desconocidas ... ok
test_reconocimiento_adjetivos (__main__.TestAnalizadorLexico)
Test reconocimiento de adjetivos ... ok
test_reconocimiento_articulos (__main__.TestAnalizadorLexico)
Test reconocimiento de artículos ... ok
test_reconocimiento_sustantivos (__main__.TestAnalizadorLexico)
Test reconocimiento de sustantivos ... ok
test_reconocimiento_verbos (__main__.TestAnalizadorLexico)
Test reconocimiento de verbos ... ok
test_tokenizacion_basica (__main__.TestAnalizadorLexico)
Test tokenización de oración simple ... ok
test_falta_articulo (__main__.TestParserDescendenteRecursivo)
Test falta artículo obligatorio ... ok
test_multiples_articulos (__main__.TestParserDescendenteRecursivo)
Test variación de artículos ... ok
test_oracion_con_adjetivo_complemento (__main__.TestParserDescendenteRecursivo)
Test oración con adjetivo en complemento ... ok
test_oracion_con_adjetivo_sujeto (__main__.TestParserDescendenteRecursivo)
Test oración con adjetivo en sujeto ... ok
test_oracion_con_adjetivos_ambos (__main__.TestParserDescendenteRecursivo)
Test oración con adjetivos en sujeto y complemento ... ok
test_oracion_svo_simple (__main__.TestParserDescendenteRecursivo)
Test oración SVO básica ... ok
test_orden_incorrecto (__main__.TestParserDescendenteRecursivo)
Test orden de palabras incorrecto ... ok
test_palabra_fuera_vocabulario (__main__.TestParserDescendenteRecursivo)
Test palabra fuera de vocabulario ... ok
test_sin_predicado (__main__.TestParserDescendenteRecursivo)
Test oración sin predicado (inválida) ... ok
test_sin_sujeto (__main__.TestParserDescendenteRecursivo)
Test oración sin sujeto (inválida) ... ok
test_casos_limite (__main__.TestIntegracion)
Test casos límite ... ok
test_conjunto_oraciones_invalidas (__main__.TestIntegracion)
Test conjunto de oraciones inválidas ... ok
test_conjunto_oraciones_validas (__main__.TestIntegracion)
Test conjunto de oraciones válidas ... ok
test_rendimiento (__main__.TestIntegracion)
Test básico de rendimiento ... ok
test_mensaje_error_lexico (__main__.TestErrores)
Test mensajes de error léxico ... ok
test_mensaje_error_sintactico (__main__.TestErrores)
Test mensajes de error sintáctico ... ok
test_multiples_errores_lexicos (__main__.TestErrores)
Test múltiples errores léxicos ... ok

----------------------------------------------------------------------
Ran 24 tests in 0.011s

OK

======================================================================
RESUMEN DE TESTS
======================================================================
Tests ejecutados: 24
Tests exitosos: 24
Tests fallidos: 0
Errores: 0

✓ TODOS LOS TESTS PASARON
======================================================================
````
