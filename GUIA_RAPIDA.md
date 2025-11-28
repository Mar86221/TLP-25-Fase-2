# Guía Rápida - Mini-Parser para Lenguaje Natural Limitado

## 📋 Contenido del Proyecto

Este proyecto contiene la implementación completa de la Fase 2:

### Archivos Principales

1. **mini_parser.py** - Parser descendente recursivo principal
   - Analizador léxico (tokenización)
   - Parser sintáctico
   - Gramática formal SVO

2. **comparacion_parsers.py** - Comparación con NLP moderno
   - Análisis comparativo con spaCy
   - Métricas de desempeño
   - Estadísticas detalladas

3. **visualizador_arbol.py** - Visualización de árboles de parsing
   - Representación ASCII de árboles
   - Análisis paso a paso
   - Reglas aplicadas

4. **test_parser.py** - Suite de tests automatizados
   - 24 tests unitarios
   - Tests de integración
   - Tests de rendimiento

5. **README_FASE2.md** - Documentación completa
   - Especificación de gramática
   - Análisis comparativo detallado
   - Conclusiones y recomendaciones

## 🚀 Instalación Rápida

```bash
# Instalar dependencias (solo para comparación con spaCy)
pip install spacy --break-system-packages
python -m spacy download es_core_news_sm --break-system-packages
```

## 💻 Cómo Ejecutar

### 1. Parser Manual Básico
```bash
python mini_parser.py
```
**Output:** Casos de prueba válidos e inválidos con análisis detallado

### 2. Comparación con spaCy
```bash
python comparacion_parsers.py
```
**Output:** 
- Comparación lado a lado
- Métricas de velocidad
- Análisis de precisión
- Resumen estadístico

### 3. Visualización de Árboles
```bash
python visualizador_arbol.py
```
**Output:**
- Árboles de derivación ASCII
- Análisis paso a paso
- Reglas aplicadas

### 4. Tests Automatizados
```bash
python test_parser.py
```
**Output:** Resultado de 24 tests unitarios

## 📊 Resultados Clave

### Velocidad
- **Parser Manual:** 0.021 ms/oración promedio
- **spaCy (Deep Learning):** 4.06 ms/oración promedio
- **Resultado:** Parser manual es **197x más rápido**

### Precisión
- **Parser Manual:** 33.3% (4/12 casos) - Vocabulario limitado
- **spaCy:** 58.3% (7/12 casos) - Vocabulario ilimitado

## 🎯 Casos de Uso

### Usar Parser Manual Cuando:
✅ Necesitas máxima velocidad  
✅ Trabajas con vocabulario controlado  
✅ Requieres validación estricta  
✅ Desarrollas DSL o lenguajes específicos  

### Usar spaCy Cuando:
✅ Necesitas manejar texto general  
✅ Vocabulario abierto/ilimitado  
✅ Robustez ante variaciones  
✅ Análisis semántico profundo  

## 📖 Ejemplos de Uso

### Ejemplo 1: Validación Simple
```python
from mini_parser import MiniParser

parser = MiniParser()
resultado = parser.analizar("el perro come un hueso")

if resultado["valido"]:
    print("✓ Oración válida")
else:
    print(f"✗ Errores: {resultado['errores']}")
```

### Ejemplo 2: Análisis Interactivo
```python
from visualizador_arbol import VisualizadorArbol

vis = VisualizadorArbol()
print(vis.visualizar_pasos("la niña lee el libro"))
```

### Ejemplo 3: Tests Personalizados
```python
from mini_parser import MiniParser

parser = MiniParser()
mis_oraciones = [
    "el gato ve la casa",
    "un libro rojo tiene el niño"
]

for oracion in mis_oraciones:
    resultado = parser.analizar(oracion)
    print(f"{oracion}: {'✓' if resultado['valido'] else '✗'}")
```

## 🔧 Extensión del Vocabulario

Para agregar nuevas palabras, edita `mini_parser.py`:

```python
class AnalizadorLexico:
    def __init__(self):
        # Agregar más sustantivos
        self.sustantivos.add("mesa")
        self.sustantivos.add("silla")
        
        # Agregar más verbos
        self.verbos.add("corre")
        self.verbos.add("salta")
```

## 📝 Gramática Soportada

```
Estructura: SUJETO + VERBO + COMPLEMENTO

Sujeto: 
  - artículo + sustantivo
  - artículo + sustantivo + adjetivo
  - artículo + adjetivo + sustantivo

Complemento:
  - (mismo formato que sujeto)
```

## ✅ Verificación de Instalación

Ejecuta este comando para verificar que todo funciona:

```bash
python test_parser.py
```

Si ves "✓ TODOS LOS TESTS PASARON", la instalación es correcta.

## 📈 Métricas de Rendimiento

- **Throughput:** ~47,600 oraciones/segundo
- **Latencia promedio:** 0.021 ms
- **Memoria:** < 1 MB
- **CPU:** Mínima

## 🎓 Valor Educativo

Este proyecto demuestra:
1. Implementación práctica de gramáticas formales
2. Parser descendente recursivo desde cero
3. Análisis léxico y sintáctico
4. Comparación con técnicas modernas (Deep Learning)
5. Trade-offs en diseño de compiladores

## 📚 Referencias

- Aho, Lam, Sethi & Ullman - "Compilers: Principles, Techniques, and Tools"
- Jurafsky & Martin - "Speech and Language Processing"
- Documentación spaCy: https://spacy.io

## 🤝 Contribuciones

Para extender el proyecto:
1. Agregar más reglas gramaticales
2. Implementar concordancia número/género
3. Agregar análisis semántico
4. Crear interfaz web interactiva

## 📧 Soporte

Para preguntas sobre el proyecto:
- Revisar README_FASE2.md para documentación completa
- Ejecutar tests para verificar funcionalidad
- Revisar ejemplos en cada archivo .py

---

**Fecha:** Noviembre 2025  
**Versión:** 1.0  
**Licencia:** Educativa
