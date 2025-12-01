# Notas Completas: Tuning Llama 3 Parameters

## 📚 Curso: Working with Llama 3
**Lección:** Tuning Llama 3 Parameters  
**XP de la lección:** 50 XP  
**XP del día:** 750 XP

---

## 🎯 1. Introducción: ¿Por qué ajustar parámetros?

En la lección anterior aprendimos a generar respuestas básicas con Llama 3. Ahora surge la pregunta:

**¿Cómo controlamos la calidad, aleatoriedad y longitud de las respuestas?**

### Caso de uso práctico:

Imagina que estás generando **descripciones de productos para diferentes sitios de e-commerce**:

- **Algunos necesitan ser:**
  - Factuales y concisos
  - Directos al punto
  - Profesionales y técnicos

- **Otros deben ser:**
  - Atractivos y creativos
  - Persuasivos y emocionantes
  - Descriptivos y detallados

**Solución:** Ajustar los parámetros de decodificación de Llama 3 para adaptar el tono y estilo según las necesidades.

---

## 🔧 2. ¿Qué son los parámetros de decodificación?

### Definición:

Los **parámetros de decodificación** (decoding parameters) son configuraciones que:

- **"Decodifican"** o transforman la salida cruda del modelo en texto legible
- Permiten **modificar las respuestas** manteniendo el contenido central
- Controlan **cómo el modelo selecciona las palabras** para generar la respuesta

### Analogía:

Piensa en el modelo como un músico:
- El **contenido** es la melodía base (siempre la misma)
- Los **parámetros** son el estilo de interpretación (jazz, clásico, rock)
- El resultado final cambia según cómo "interpretes" la melodía

---

## 📊 3. Los 4 parámetros clave de Llama 3

Exploraremos cuatro parámetros fundamentales:

| Parámetro | Función | Controla |
|-----------|---------|----------|
| **`temperature`** | Controla la aleatoriedad | Qué tan predecible o creativo es el texto |
| **`top_k`** | Limita selección de tokens | Cuántas palabras considera el modelo en cada paso |
| **`top_p`** | Ajusta selección por probabilidad | Qué porcentaje de probabilidad acumulada usar |
| **`max_tokens`** | Limita longitud de respuesta | Cuántos tokens (palabras) generar como máximo |

---

## 🌡️ 4. Temperature (Temperatura)

### ¿Qué es?

La **temperatura** controla la **aleatoriedad** o **creatividad** de las respuestas del modelo.

### Rango de valores:

- **Típicamente:** 0.0 a 1.0
- **Valores extremos:** Pueden ir hasta 2.0, pero no es común

### Comportamiento:

#### 🧊 Temperatura BAJA (cercana a 0)

**Valor:** 0.0 - 0.3

**Características:**
- ✅ Respuestas **predecibles** y **consistentes**
- ✅ Más **factuales** y **precisas**
- ✅ Menos variación entre generaciones
- ❌ Puede ser **repetitivo** o **aburrido**
- ❌ Menos **creatividad**

**Ejemplo - Descripción de smartwatch con temperature=0.1:**

```
This smartwatch features:
- Heart rate monitor
- GPS tracking
- Long battery life (up to 7 days)
- Water resistance (50m)
- Sleep tracking
```

**Uso recomendado:**
- Documentación técnica
- Respuestas factuales
- Análisis de datos
- Resúmenes precisos
- Traducciones

---

#### 🔥 Temperatura ALTA (cercana a 1)

**Valor:** 0.7 - 1.0

**Características:**
- ✅ Respuestas **creativas** y **variadas**
- ✅ Más **expresivas** y **únicas**
- ✅ Mayor **diversidad** en el lenguaje
- ❌ Puede ser **menos preciso**
- ❌ A veces **incoherente** (si es muy alta)

**Ejemplo - Descripción de smartwatch con temperature=0.9:**

```
Discover the ultimate companion for your active lifestyle! 
This cutting-edge smartwatch seamlessly blends style with 
functionality, featuring an advanced heart rate monitor that 
keeps you in tune with your body's rhythms. Navigate your 
adventures with precision GPS, while the remarkable 7-day 
battery life ensures you're always connected. Dive into life 
with confidence thanks to its impressive 50m water resistance!
```

**Uso recomendado:**
- Marketing y copywriting
- Contenido creativo
- Storytelling
- Brainstorming de ideas
- Generación de variaciones

---

### 📝 Código de ejemplo:

```python
from llama_cpp import Llama

llm = Llama(model_path="./models/llama-3-8b.gguf")

prompt = "Write a product description for a smartwatch."

# Respuesta predecible (baja temperatura)
response_low = llm(
    prompt=prompt,
    temperature=0.1,
    max_tokens=100
)

# Respuesta creativa (alta temperatura)
response_high = llm(
    prompt=prompt,
    temperature=0.9,
    max_tokens=100
)

print("LOW TEMPERATURE (0.1):")
print(response_low["choices"][0]["text"])
print("\n" + "="*60 + "\n")
print("HIGH TEMPERATURE (0.9):")
print(response_high["choices"][0]["text"])
```

---

## 🎲 5. Top-k

### ¿Qué es?

**Top-k** controla **cuántas palabras** (tokens) el modelo considera usar **cada vez que añade una nueva palabra** a la respuesta.

### Cómo funciona:

En cada paso de generación, el modelo:
1. Calcula probabilidades para todas las palabras posibles
2. Ordena las palabras por probabilidad (de mayor a menor)
3. **Solo considera las k palabras más probables**
4. Selecciona una de esas k palabras

### Valores típicos:

- **Muy bajo:** `top_k = 1` (solo la palabra más probable)
- **Bajo:** `top_k = 5-10`
- **Medio:** `top_k = 20-30`
- **Alto:** `top_k = 50-100`

---

#### 🔒 Top-k BAJO (ej: top_k=1)

**Características:**
- ✅ Respuestas **muy predecibles**
- ✅ **Consistentes** entre generaciones
- ❌ Puede ser **repetitivo**
- ❌ Falta de **variedad**

**Ejemplo - Smartwatch con top_k=1:**

```
This smartwatch has a heart rate monitor, GPS, and long battery life.
This smartwatch has a heart rate monitor, GPS, and long battery life.
This smartwatch has a heart rate monitor, GPS, and long battery life.
```
*(Nota: Generaciones múltiples producen casi el mismo resultado)*

**Comportamiento:**
- El modelo **siempre elige la palabra más probable**
- Similar a una lista directa de características
- Muy parecido al efecto de temperatura baja

---

#### 🎨 Top-k ALTO (ej: top_k=50)

**Características:**
- ✅ Respuestas **más expresivas**
- ✅ Mayor **variedad** de vocabulario
- ✅ Más **natural** y **fluido**
- ⚠️ Puede introducir palabras menos comunes

**Ejemplo - Smartwatch con top_k=50:**

```
Experience cutting-edge wearable technology with this remarkable 
smartwatch, boasting comprehensive health monitoring through its 
sophisticated heart rate sensor, precise GPS navigation for your 
outdoor adventures, and an exceptional battery that lasts up to 
a full week on a single charge.
```

**Comportamiento:**
- El modelo puede elegir entre las **50 palabras más probables**
- Permite sinónimos y expresiones variadas
- Más libertad creativa manteniendo coherencia

---

### 📝 Código de ejemplo:

```python
from llama_cpp import Llama

llm = Llama(model_path="./models/llama-3-8b.gguf")

prompt = "Write a product description for a smartwatch."

# Respuesta muy predecible (top_k bajo)
response_low_k = llm(
    prompt=prompt,
    top_k=1,
    temperature=0.7,  # Temperatura neutral
    max_tokens=100
)

# Respuesta más expresiva (top_k alto)
response_high_k = llm(
    prompt=prompt,
    top_k=50,
    temperature=0.7,  # Misma temperatura
    max_tokens=100
)

print("LOW TOP-K (1):")
print(response_low_k["choices"][0]["text"])
print("\n" + "="*60 + "\n")
print("HIGH TOP-K (50):")
print(response_high_k["choices"][0]["text"])
```

---

## 📈 6. Top-p (Nucleus Sampling)

### ¿Qué es?

**Top-p** es similar a top-k, pero en lugar de limitar por **número de palabras**, limita por **probabilidad acumulada**.

También se conoce como **"nucleus sampling"** (muestreo del núcleo).

### Cómo funciona:

1. El modelo calcula probabilidades para todas las palabras posibles
2. Ordena las palabras por probabilidad (de mayor a menor)
3. **Suma las probabilidades acumulativamente** hasta alcanzar el valor de `top_p`
4. Solo considera las palabras dentro de ese "núcleo" de probabilidad
5. Selecciona una palabra de ese conjunto

### Valores típicos:

- **Muy bajo:** `top_p = 0.1` (solo las palabras más probables)
- **Bajo:** `top_p = 0.3-0.5`
- **Medio:** `top_p = 0.7-0.8`
- **Alto:** `top_p = 0.9-0.95`
- **Máximo:** `top_p = 1.0` (considera todas las palabras)

---

#### 🎯 Top-p BAJO (ej: top_p=0.4)

**Características:**
- ✅ Salida **enfocada** y **precisa**
- ✅ Solo menciona **funcionalidades centrales**
- ✅ Más **conservador** en la selección de palabras
- ❌ Menos **variedad** léxica

**Ejemplo - Smartwatch con top_p=0.4:**

```
This smartwatch includes heart rate monitoring, GPS tracking, 
and extended battery life.
```

**Comportamiento:**
- Solo considera palabras que suman hasta el **40% de probabilidad**
- Típicamente son las palabras más obvias y directas
- Respuesta concisa y al grano

---

#### 🌈 Top-p ALTO (ej: top_p=0.9)

**Características:**
- ✅ Respuestas **más variadas**
- ✅ Lista **múltiples características**
- ✅ Lenguaje más **rico** y **descriptivo**
- ⚠️ Puede incluir detalles menos relevantes

**Ejemplo - Smartwatch con top_p=0.9:**

```
Elevate your fitness journey with this feature-packed smartwatch! 
It offers comprehensive health tracking including heart rate 
monitoring, advanced GPS navigation for precise route tracking, 
an impressive 7-day battery life, water resistance up to 50 meters, 
sleep quality analysis, step counting, calorie tracking, and 
smartphone notifications to keep you connected throughout your day.
```

**Comportamiento:**
- Considera palabras que suman hasta el **90% de probabilidad**
- Incluye más opciones de vocabulario
- Permite descripciones más completas y detalladas

---

### 🆚 Top-k vs Top-p: ¿Cuál usar?

| Aspecto | Top-k | Top-p |
|---------|-------|-------|
| **Criterio** | Número fijo de palabras | Probabilidad acumulada |
| **Flexibilidad** | Siempre considera k palabras | Número variable según distribución |
| **Mejor para** | Control preciso del vocabulario | Adaptación dinámica al contexto |
| **Recomendación** | Usar cuando quieres límite estricto | Usar para más naturalidad |

**💡 Consejo:** Muchos practicionantes usan **ambos juntos** para un control más fino:

```python
response = llm(
    prompt=prompt,
    top_k=40,      # Máximo 40 palabras a considerar
    top_p=0.9,     # Pero solo hasta 90% de probabilidad
    temperature=0.7
)
```

---

### 📝 Código de ejemplo:

```python
from llama_cpp import Llama

llm = Llama(model_path="./models/llama-3-8b.gguf")

prompt = "Write a product description for a smartwatch."

# Respuesta enfocada (top_p bajo)
response_low_p = llm(
    prompt=prompt,
    top_p=0.4,
    temperature=0.7,
    max_tokens=100
)

# Respuesta variada (top_p alto)
response_high_p = llm(
    prompt=prompt,
    top_p=0.9,
    temperature=0.7,
    max_tokens=100
)

print("LOW TOP-P (0.4):")
print(response_low_p["choices"][0]["text"])
print("\n" + "="*60 + "\n")
print("HIGH TOP-P (0.9):")
print(response_high_p["choices"][0]["text"])
```

---

## 📏 7. Max Tokens

### ¿Qué es?

**Max tokens** limita la **longitud de la respuesta** especificando el número máximo de tokens (unidades de palabras) que el modelo puede generar.

### ¿Qué es un token?

- Un **token** puede ser:
  - Una palabra completa: `"smartwatch"` = 1 token
  - Parte de una palabra: `"smart"` + `"watch"` = 2 tokens
  - Un símbolo: `"!"` = 1 token
  - Un espacio o puntuación

**Regla aproximada:**
- **En inglés:** 1 token ≈ 0.75 palabras
- **100 tokens** ≈ 75 palabras
- **256 tokens** ≈ 190 palabras

### Valores típicos:

- **Muy corto:** `max_tokens = 10-20` (una oración)
- **Corto:** `max_tokens = 50-100` (un párrafo pequeño)
- **Medio:** `max_tokens = 150-300` (varios párrafos)
- **Largo:** `max_tokens = 500-1000` (respuesta extensa)
- **Muy largo:** `max_tokens = 2000+` (artículo completo)

---

#### 📌 Max tokens BAJO (ej: max_tokens=20)

**Uso:** Resúmenes cortos y precisos

**Ejemplo - Smartwatch con max_tokens=20:**

```
A smartwatch with heart rate monitor, GPS, and long battery life.
```

**Características:**
- ✅ **Conciso** y directo
- ✅ Solo información **esencial**
- ✅ Rápido de generar
- ❌ Puede cortar información importante
- ❌ Falta de detalles

**Casos de uso:**
- Títulos de productos
- Resúmenes ejecutivos
- Respuestas rápidas
- Etiquetas o tags
- Notificaciones breves

---

#### 📄 Max tokens ALTO (ej: max_tokens=100-200)

**Uso:** Explicaciones detalladas

**Ejemplo - Smartwatch con max_tokens=100:**

```
Discover the perfect blend of style and functionality with this 
advanced smartwatch. Featuring a state-of-the-art heart rate 
monitor that tracks your cardiovascular health in real-time, 
integrated GPS for accurate navigation and fitness tracking, 
and an impressive battery life that lasts up to 7 days on a 
single charge. Whether you're hitting the gym, exploring the 
outdoors, or managing your daily schedule, this smartwatch is 
your ideal companion for a connected, healthy lifestyle.
```

**Características:**
- ✅ **Detallado** y completo
- ✅ Incluye **contexto** y **beneficios**
- ✅ Más **persuasivo**
- ⚠️ Toma más tiempo generar
- ⚠️ Usa más recursos

**Casos de uso:**
- Descripciones de productos completas
- Artículos de blog
- Documentación
- Respuestas educativas
- Análisis detallados

---

### ⚠️ Consideraciones importantes:

1. **El modelo puede detenerse antes** si completa naturalmente la respuesta
2. **No es un límite estricto de palabras**, sino de tokens
3. **Afecta el costo computacional**: más tokens = más tiempo de procesamiento
4. **Debe considerar el contexto total**: prompt + respuesta no debe exceder `n_ctx`

### 📝 Código de ejemplo:

```python
from llama_cpp import Llama

llm = Llama(model_path="./models/llama-3-8b.gguf")

prompt = "Write a product description for a smartwatch."

# Respuesta corta
response_short = llm(
    prompt=prompt,
    max_tokens=20,
    temperature=0.7
)

# Respuesta detallada
response_long = llm(
    prompt=prompt,
    max_tokens=150,
    temperature=0.7
)

print("SHORT (20 tokens):")
print(response_short["choices"][0]["text"])
print("\n" + "="*60 + "\n")
print("LONG (150 tokens):")
print(response_long["choices"][0]["text"])
```

---

## 🎨 8. Combinando parámetros

La verdadera potencia viene de **combinar múltiples parámetros** para lograr el resultado deseado.

### Ejemplo 1: Descripción concisa y factual de un auto eléctrico

**Objetivo:** Descripción corta, precisa y profesional

```python
from llama_cpp import Llama

llm = Llama(model_path="./models/llama-3-8b.gguf")

prompt = "Describe an electric car."

response = llm(
    prompt=prompt,
    temperature=0.2,    # Baja creatividad, más factual
    top_k=1,            # Solo palabras más probables
    top_p=0.4,          # Enfoque en lo esencial
    max_tokens=20       # Respuesta muy corta
)

print(response["choices"][0]["text"])
```

**Resultado esperado:**

```
An electric vehicle powered by rechargeable batteries, 
offering zero emissions and efficient performance.
```

**Análisis de la configuración:**

| Parámetro | Valor | Efecto |
|-----------|-------|--------|
| `temperature=0.2` | Bajo | Respuesta predecible y factual |
| `top_k=1` | Mínimo | Solo la palabra más probable |
| `top_p=0.4` | Bajo | Enfocado en lo esencial |
| `max_tokens=20` | Corto | Descripción concisa |

**Resultado:** Descripción **corta, precisa y profesional** ✅

---

### Ejemplo 2: Descripción creativa y detallada de un auto eléctrico

**Objetivo:** Descripción larga, atractiva y persuasiva (para marketing)

```python
from llama_cpp import Llama

llm = Llama(model_path="./models/llama-3-8b.gguf")

prompt = "Describe an electric car."

response = llm(
    prompt=prompt,
    temperature=0.8,    # Alta creatividad
    top_k=10,           # Más opciones de palabras
    top_p=0.9,          # Amplio rango de vocabulario
    max_tokens=100      # Respuesta detallada
)

print(response["choices"][0]["text"])
```

**Resultado esperado:**

```
Experience the future of automotive innovation with this 
stunning electric vehicle! Seamlessly blending cutting-edge 
technology with environmental consciousness, this remarkable 
car delivers exhilarating instant torque, whisper-quiet 
operation, and zero tailpipe emissions. With its sleek, 
aerodynamic design and advanced regenerative braking system, 
you'll enjoy an impressive range of up to 300 miles on a 
single charge. The spacious, tech-forward interior features 
a state-of-the-art infotainment system, premium materials, 
and autonomous driving capabilities that redefine your 
journey. Embrace sustainable luxury and join the electric 
revolution today!
```

**Análisis de la configuración:**

| Parámetro | Valor | Efecto |
|-----------|-------|--------|
| `temperature=0.8` | Alto | Respuesta creativa y variada |
| `top_k=10` | Medio | Vocabulario más rico |
| `top_p=0.9` | Alto | Amplia selección de palabras |
| `max_tokens=100` | Largo | Descripción completa y detallada |

**Resultado:** Descripción **creativa, persuasiva y detallada** ✅

---

## 📋 9. Guía rápida de configuraciones recomendadas

### 🎯 Para diferentes casos de uso:

#### 1. **Documentación técnica / Respuestas factuales**

```python
response = llm(
    prompt=prompt,
    temperature=0.1,
    top_k=1,
    top_p=0.5,
    max_tokens=200
)
```

**Características:** Preciso, consistente, factual

---

#### 2. **Resúmenes ejecutivos**

```python
response = llm(
    prompt=prompt,
    temperature=0.3,
    top_k=5,
    top_p=0.6,
    max_tokens=100
)
```

**Características:** Conciso, claro, profesional

---

#### 3. **Contenido de marketing / Copywriting**

```python
response = llm(
    prompt=prompt,
    temperature=0.8,
    top_k=40,
    top_p=0.9,
    max_tokens=150
)
```

**Características:** Creativo, persuasivo, atractivo

---

#### 4. **Brainstorming / Ideas creativas**

```python
response = llm(
    prompt=prompt,
    temperature=0.9,
    top_k=50,
    top_p=0.95,
    max_tokens=200
)
```

**Características:** Muy creativo, diverso, innovador

---

#### 5. **Chatbot conversacional**

```python
response = llm(
    prompt=prompt,
    temperature=0.7,
    top_k=30,
    top_p=0.85,
    max_tokens=100
)
```

**Características:** Natural, balanceado, amigable

---

#### 6. **Análisis de datos / Reportes**

```python
response = llm(
    prompt=prompt,
    temperature=0.2,
    top_k=10,
    top_p=0.7,
    max_tokens=300
)
```

**Características:** Objetivo, estructurado, detallado

---

#### 7. **Generación de código**

```python
response = llm(
    prompt=prompt,
    temperature=0.1,
    top_k=1,
    top_p=0.5,
    max_tokens=500
)
```

**Características:** Preciso, sintácticamente correcto, predecible

---

#### 8. **Storytelling / Narrativa**

```python
response = llm(
    prompt=prompt,
    temperature=0.85,
    top_k=40,
    top_p=0.9,
    max_tokens=400
)
```

**Características:** Creativo, descriptivo, envolvente

---

## 🧪 10. Experimentación y mejores prácticas

### ✅ Mejores prácticas:

1. **Empieza con valores por defecto**
   ```python
   temperature=0.7
   top_k=40
   top_p=0.9
   max_tokens=256
   ```

2. **Ajusta un parámetro a la vez**
   - Cambia solo uno para ver su efecto individual
   - Documenta los resultados

3. **Prueba con el mismo prompt**
   - Usa el mismo prompt para comparar resultados
   - Facilita identificar el impacto de cada parámetro

4. **Considera el caso de uso**
   - ¿Necesitas precisión o creatividad?
   - ¿Respuesta corta o detallada?
   - ¿Tono formal o casual?

5. **Monitorea la calidad**
   - Revisa si las respuestas son coherentes
   - Verifica que no haya repeticiones excesivas
   - Asegúrate de que la longitud sea apropiada

### ⚠️ Errores comunes a evitar:

❌ **Temperatura demasiado alta (>1.0)**
- Puede generar texto incoherente o sin sentido

❌ **Max tokens demasiado bajo**
- Puede cortar respuestas importantes a la mitad

❌ **Combinar valores extremos**
- Ej: `temperature=0.0` con `top_k=100` (contradictorios)

❌ **No considerar el contexto total**
- `max_tokens` + longitud del prompt debe caber en `n_ctx`

❌ **Usar los mismos parámetros para todo**
- Diferentes tareas requieren diferentes configuraciones

---

## 📊 11. Tabla comparativa de efectos

| Parámetro | Valor Bajo | Valor Alto |
|-----------|------------|------------|
| **Temperature** | Predecible, factual, repetitivo | Creativo, variado, arriesgado |
| **Top-k** | Conservador, limitado | Expresivo, diverso |
| **Top-p** | Enfocado, preciso | Variado, completo |
| **Max tokens** | Conciso, breve | Detallado, extenso |

---

## 💻 12. Código completo de ejemplo

```python
"""
Ejemplo completo: Comparación de configuraciones de parámetros
"""

from llama_cpp import Llama

def generate_description(llm, prompt, config_name, **params):
    """Genera una descripción con parámetros específicos"""
    print(f"\n{'='*70}")
    print(f"CONFIGURACIÓN: {config_name}")
    print(f"{'='*70}")
    print(f"Parámetros: {params}")
    print(f"{'-'*70}\n")
    
    response = llm(prompt=prompt, **params)
    text = response["choices"][0]["text"]
    
    print(f"Resultado:\n{text}\n")
    
    # Mostrar estadísticas
    usage = response.get("usage", {})
    print(f"📊 Tokens generados: {usage.get('completion_tokens', 'N/A')}")
    print(f"{'='*70}\n")
    
    return text

def main():
    # Inicializar modelo
    print("Cargando modelo Llama 3...")
    llm = Llama(
        model_path="./models/llama-3-8b.gguf",
        n_ctx=2048,
        n_threads=8,
        verbose=False
    )
    print("✅ Modelo cargado\n")
    
    # Prompt común
    prompt = "Describe an electric car."
    
    # Configuración 1: Factual y conciso
    generate_description(
        llm, prompt,
        config_name="FACTUAL Y CONCISO",
        temperature=0.2,
        top_k=1,
        top_p=0.4,
        max_tokens=20
    )
    
    # Configuración 2: Creativo y detallado
    generate_description(
        llm, prompt,
        config_name="CREATIVO Y DETALLADO",
        temperature=0.8,
        top_k=10,
        top_p=0.9,
        max_tokens=100
    )
    
    # Configuración 3: Balanceado (uso general)
    generate_description(
        llm, prompt,
        config_name="BALANCEADO (RECOMENDADO)",
        temperature=0.7,
        top_k=40,
        top_p=0.85,
        max_tokens=80
    )
    
    # Configuración 4: Muy creativo (brainstorming)
    generate_description(
        llm, prompt,
        config_name="MUY CREATIVO (BRAINSTORMING)",
        temperature=0.9,
        top_k=50,
        top_p=0.95,
        max_tokens=120
    )
    
    # Configuración 5: Muy preciso (técnico)
    generate_description(
        llm, prompt,
        config_name="MUY PRECISO (TÉCNICO)",
        temperature=0.1,
        top_k=1,
        top_p=0.5,
        max_tokens=150
    )

if __name__ == "__main__":
    main()
```

---

## 🎓 13. Conceptos clave para recordar

### Términos importantes:

- **Decoding parameters:** Parámetros que controlan cómo se transforma la salida del modelo en texto
- **Temperature:** Controla la aleatoriedad/creatividad (0 = predecible, 1 = creativo)
- **Top-k:** Limita cuántas palabras considera el modelo en cada paso
- **Top-p (Nucleus sampling):** Limita palabras por probabilidad acumulada
- **Max tokens:** Número máximo de tokens a generar
- **Token:** Unidad básica de texto (≈0.75 palabras en inglés)

### Reglas de oro:

1. **No existe una configuración perfecta universal**
   - Cada tarea requiere ajustes específicos

2. **Experimenta y documenta**
   - Prueba diferentes combinaciones
   - Guarda las que funcionan bien

3. **Empieza conservador, ajusta gradualmente**
   - Comienza con valores moderados
   - Aumenta/disminuye según necesites

4. **Considera el trade-off**
   - Creatividad vs Precisión
   - Longitud vs Concisión
   - Velocidad vs Calidad

---

## 🚀 14. Próximos pasos

Después de dominar los parámetros básicos, puedes:

1. **Explorar parámetros avanzados**
   - `repeat_penalty`: Penaliza repeticiones
   - `frequency_penalty`: Reduce palabras frecuentes
   - `presence_penalty`: Fomenta nuevos temas
   - `stop`: Define secuencias de parada personalizadas

2. **Crear presets personalizados**
   - Guarda configuraciones para diferentes tareas
   - Crea una biblioteca de configuraciones

3. **Implementar A/B testing**
   - Compara diferentes configuraciones
   - Mide cuál funciona mejor para tu caso

4. **Automatizar la selección de parámetros**
   - Crea funciones que elijan parámetros según el tipo de tarea
   - Implementa lógica adaptativa

---

## 📚 15. Recursos adicionales

### Documentación:
- [llama-cpp-python - Parámetros de generación](https://github.com/abetlen/llama-cpp-python)
- [Hugging Face - Generation Parameters](https://huggingface.co/docs/transformers/main_classes/text_generation)

### Artículos recomendados:
- "The Curious Case of Neural Text Degeneration" (sobre nucleus sampling)
- "Temperature in Language Models" (análisis profundo)

### Herramientas útiles:
- [LLM Parameter Playground](https://huggingface.co/spaces) - Experimenta visualmente
- Notebooks de Jupyter para experimentación

---

## 💡 16. Resumen ejecutivo

Los **parámetros de decodificación** te permiten controlar cómo Llama 3 genera texto:

| Parámetro | Qué controla | Valores típicos |
|-----------|--------------|-----------------|
| **temperature** | Creatividad vs Precisión | 0.1 (preciso) - 0.9 (creativo) |
| **top_k** | Número de palabras a considerar | 1 (limitado) - 50 (variado) |
| **top_p** | Probabilidad acumulada | 0.4 (enfocado) - 0.9 (diverso) |
| **max_tokens** | Longitud de respuesta | 20 (corto) - 500+ (largo) |

**Configuración recomendada para empezar:**
```python
temperature=0.7, top_k=40, top_p=0.9, max_tokens=256
```

**Ajusta según necesites:**
- ⬇️ Baja temperatura/top-k/top-p para **precisión**
- ⬆️ Sube temperatura/top-k/top-p para **creatividad**
- ⬇️ Baja max_tokens para **concisión**
- ⬆️ Sube max_tokens para **detalle**

---

## ✨ Conclusión

Dominar los parámetros de Llama 3 es como aprender a afinar un instrumento musical: con práctica y experimentación, puedes lograr exactamente el tono y estilo que necesitas para cada situación. No tengas miedo de experimentar y encontrar las configuraciones que mejor funcionen para tus casos de uso específicos.

**¡Ahora estás listo para ajustar Llama 3 como un profesional! 🎯**

---

*Notas generadas a partir del curso "Working with Llama 3"*  
*Lección: Tuning Llama 3 Parameters*  
*XP de la lección: 50 | XP del día: 750*