# Notas Completas: Introducción a Ollama

## 📚 Curso: Working with Llama 3
**Tema:** Introducción a Ollama  
**Nivel:** Principiante

---

## 🎯 1. ¿Qué es Ollama?

### Definición:

**Ollama** es una herramienta de código abierto que simplifica la ejecución de modelos de lenguaje grandes (LLMs) en tu computadora local.

### Características principales:

- ✅ **Interfaz simple y amigable** - Similar a Docker para contenedores
- ✅ **Gestión automática de modelos** - Descarga, actualiza y elimina modelos fácilmente
- ✅ **Optimización automática** - Configura el hardware óptimamente sin intervención manual
- ✅ **API REST integrada** - Permite integración con aplicaciones
- ✅ **Soporte multi-modelo** - Ejecuta diferentes modelos según necesidades
- ✅ **Multiplataforma** - Funciona en Linux, macOS y Windows

### Analogía:

Piensa en Ollama como el **"Spotify de los LLMs"**:
- Spotify te permite reproducir música sin descargar archivos complejos
- Ollama te permite ejecutar LLMs sin configuraciones complicadas
- Ambos gestionan la complejidad técnica por ti

---

## 🆚 2. Ollama vs llama-cpp-python

### Comparación:

| Aspecto | Ollama | llama-cpp-python |
|---------|--------|------------------|
| **Facilidad de uso** | ⭐⭐⭐⭐⭐ Muy fácil | ⭐⭐⭐ Moderado |
| **Instalación** | Un comando | Requiere compilación |
| **Gestión de modelos** | Automática | Manual |
| **API** | REST API incluida | Debes crearla tú |
| **Configuración** | Automática | Manual detallada |
| **Flexibilidad** | Media | Alta |
| **Control fino** | Limitado | Total |
| **Curva de aprendizaje** | Baja | Media-Alta |

### ¿Cuándo usar cada uno?

**Usa Ollama si:**
- Quieres empezar rápidamente
- Necesitas una solución "plug and play"
- Vas a crear aplicaciones web/API
- Prefieres simplicidad sobre control total
- Trabajas en equipo con diferentes niveles técnicos

**Usa llama-cpp-python si:**
- Necesitas control total sobre parámetros
- Quieres optimizaciones específicas
- Trabajas en investigación o experimentación
- Necesitas integración profunda con Python
- Requieres configuraciones muy personalizadas

---

## 🔧 3. Instalación de Ollama

### En Linux:

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

### En macOS:

```bash
brew install ollama
```

O descarga el instalador desde: https://ollama.com/download

### En Windows:

Descarga el instalador desde: https://ollama.com/download/windows

### Verificar instalación:

```bash
ollama --version
```

**Salida esperada:**
```
ollama version 0.1.x
```

---

## 🚀 4. Comandos básicos de Ollama

### 4.1 Listar modelos disponibles localmente:

```bash
ollama list
```

**Salida ejemplo:**
```
NAME                    ID              SIZE    MODIFIED
llama3:8b              a6990ed6be41    4.7 GB  2 days ago
llama3:70b             9f438cb9cd58    39 GB   1 week ago
mistral:7b             f974a74358d6    4.1 GB  3 days ago
```

### 4.2 Descargar un modelo:

```bash
ollama pull llama3
```

**Proceso:**
```
pulling manifest
pulling 8934d96d3f08... 100% ▕████████████████▏ 4.7 GB
pulling 8c17c2ebb0ea... 100% ▕████████████████▏ 7.0 KB
pulling 7c23fb36d801... 100% ▕████████████████▏ 4.8 KB
pulling 2e0493f67d0c... 100% ▕████████████████▏ 59 B
pulling fa304d675061... 100% ▕████████████████▏ 91 B
pulling 42ba7f8a01dd... 100% ▕████████████████▏ 557 B
verifying sha256 digest
writing manifest
removing any unused layers
success
```

### 4.3 Ejecutar un modelo interactivamente:

```bash
ollama run llama3
```

**Sesión interactiva:**
```
>>> Hello! Who are you?
I'm Llama 3, an AI assistant created by Meta. I'm here to help answer 
your questions and have conversations. How can I assist you today?

>>> What can you do?
I can help with various tasks including:
- Answering questions on many topics
- Writing and editing text
- Coding assistance
- Creative writing
- Analysis and summarization
- And much more!

>>> /bye
```

### 4.4 Ejecutar un modelo con un prompt directo:

```bash
ollama run llama3 "Explain quantum computing in simple terms"
```

### 4.5 Eliminar un modelo:

```bash
ollama rm llama3:70b
```

### 4.6 Ver información de un modelo:

```bash
ollama show llama3
```

**Salida:**
```
Model
  architecture        llama
  parameters          8.0B
  context length      8192
  embedding length    4096
  quantization        Q4_0

License
  Meta Llama 3 Community License

System
  You are a helpful assistant.
```

---

## 🌐 5. API REST de Ollama

### 5.1 Iniciar el servidor:

Ollama inicia automáticamente un servidor en `http://localhost:11434`

### 5.2 Generar una respuesta (endpoint /api/generate):

```bash
curl http://localhost:11434/api/generate -d '{
  "model": "llama3",
  "prompt": "Why is the sky blue?",
  "stream": false
}'
```

**Respuesta:**
```json
{
  "model": "llama3",
  "created_at": "2024-01-15T10:30:00.000Z",
  "response": "The sky appears blue because of a phenomenon called Rayleigh scattering...",
  "done": true,
  "context": [1, 2, 3, ...],
  "total_duration": 5000000000,
  "load_duration": 1000000000,
  "prompt_eval_count": 10,
  "prompt_eval_duration": 500000000,
  "eval_count": 50,
  "eval_duration": 3500000000
}
```

### 5.3 Chat con historial (endpoint /api/chat):

```bash
curl http://localhost:11434/api/chat -d '{
  "model": "llama3",
  "messages": [
    {
      "role": "user",
      "content": "What is machine learning?"
    }
  ],
  "stream": false
}'
```

### 5.4 Streaming de respuestas:

```bash
curl http://localhost:11434/api/generate -d '{
  "model": "llama3",
  "prompt": "Write a short story",
  "stream": true
}'
```

**Respuesta (streaming):**
```json
{"model":"llama3","created_at":"...","response":"Once","done":false}
{"model":"llama3","created_at":"...","response":" upon","done":false}
{"model":"llama3","created_at":"...","response":" a","done":false}
{"model":"llama3","created_at":"...","response":" time","done":false}
...
{"model":"llama3","created_at":"...","response":"","done":true}
```

---

## 🐍 6. Usar Ollama con Python

### 6.1 Instalación de la biblioteca oficial:

```bash
pip install ollama
```

### 6.2 Ejemplo básico:

```python
import ollama

response = ollama.chat(
    model='llama3',
    messages=[
        {
            'role': 'user',
            'content': 'Why is the ocean salty?'
        }
    ]
)

print(response['message']['content'])
```

### 6.3 Ejemplo con streaming:

```python
import ollama

stream = ollama.chat(
    model='llama3',
    messages=[
        {
            'role': 'user',
            'content': 'Tell me a joke'
        }
    ],
    stream=True
)

for chunk in stream:
    print(chunk['message']['content'], end='', flush=True)
```

### 6.4 Ejemplo con historial de conversación:

```python
import ollama

messages = []

def chat(user_message):
    messages.append({
        'role': 'user',
        'content': user_message
    })
    
    response = ollama.chat(
        model='llama3',
        messages=messages
    )
    
    assistant_message = response['message']['content']
    
    messages.append({
        'role': 'assistant',
        'content': assistant_message
    })
    
    return assistant_message

print(chat("Hello! What's your name?"))
print(chat("What can you help me with?"))
print(chat("Tell me about Python programming"))
```

### 6.5 Ejemplo con parámetros personalizados:

```python
import ollama

response = ollama.generate(
    model='llama3',
    prompt='Write a product description for a laptop',
    options={
        'temperature': 0.8,
        'top_k': 40,
        'top_p': 0.9,
        'num_predict': 200
    }
)

print(response['response'])
```

---

## 📦 7. Modelos disponibles en Ollama

### Modelos populares:

| Modelo | Tamaño | Descripción | Uso recomendado |
|--------|--------|-------------|------------------|
| **llama3:8b** | 4.7 GB | Modelo general de Meta | Uso general, conversación |
| **llama3:70b** | 39 GB | Versión grande de Llama 3 | Tareas complejas, análisis |
| **mistral:7b** | 4.1 GB | Modelo eficiente de Mistral AI | Rápido y preciso |
| **codellama:7b** | 3.8 GB | Especializado en código | Programación, debugging |
| **phi3:mini** | 2.3 GB | Modelo pequeño de Microsoft | Dispositivos limitados |
| **gemma:7b** | 4.8 GB | Modelo de Google | Tareas variadas |
| **neural-chat:7b** | 4.1 GB | Optimizado para chat | Conversaciones naturales |

### Descargar modelos específicos:

```bash
ollama pull llama3:8b
ollama pull mistral:7b-instruct
ollama pull codellama:13b
```

### Variantes de modelos:

Los modelos pueden tener diferentes variantes:
- **Base:** Modelo sin ajuste fino
- **Instruct:** Ajustado para seguir instrucciones
- **Chat:** Optimizado para conversaciones
- **Code:** Especializado en programación

**Ejemplo:**
```bash
ollama pull llama3:8b-instruct
ollama pull codellama:7b-python
```

---

## ⚙️ 8. Configuración avanzada de Ollama

### 8.1 Modelfile - Personalizar modelos:

Crea un archivo llamado `Modelfile`:

```dockerfile
FROM llama3

PARAMETER temperature 0.8
PARAMETER top_k 40
PARAMETER top_p 0.9

SYSTEM """
You are a helpful coding assistant specialized in Python.
You provide clear, concise code examples with explanations.
"""
```

Crear el modelo personalizado:

```bash
ollama create python-assistant -f Modelfile
```

Usar el modelo personalizado:

```bash
ollama run python-assistant
```

### 8.2 Configurar variables de entorno:

```bash
export OLLAMA_HOST=0.0.0.0:11434
export OLLAMA_MODELS=/custom/path/to/models
export OLLAMA_NUM_PARALLEL=4
export OLLAMA_MAX_LOADED_MODELS=2
```

### 8.3 Configurar GPU:

Ollama detecta automáticamente GPUs disponibles. Para forzar CPU:

```bash
OLLAMA_NUM_GPU=0 ollama run llama3
```

---

## 🔍 9. Casos de uso prácticos

### 9.1 Chatbot local:

```python
import ollama

def chatbot():
    print("Chatbot iniciado. Escribe 'salir' para terminar.\n")
    messages = []
    
    while True:
        user_input = input("Tú: ")
        
        if user_input.lower() == 'salir':
            print("¡Hasta luego!")
            break
        
        messages.append({
            'role': 'user',
            'content': user_input
        })
        
        response = ollama.chat(
            model='llama3',
            messages=messages
        )
        
        assistant_message = response['message']['content']
        messages.append({
            'role': 'assistant',
            'content': assistant_message
        })
        
        print(f"Bot: {assistant_message}\n")

chatbot()
```

### 9.2 Analizador de sentimientos:

```python
import ollama

def analyze_sentiment(text):
    prompt = f"""
    Analiza el sentimiento del siguiente texto y clasifícalo como:
    POSITIVO, NEGATIVO o NEUTRAL
    
    Texto: "{text}"
    
    Responde solo con la clasificación.
    """
    
    response = ollama.generate(
        model='llama3',
        prompt=prompt,
        options={'temperature': 0.1}
    )
    
    return response['response'].strip()

reviews = [
    "Este producto es excelente, lo recomiendo totalmente!",
    "Muy decepcionado con la calidad, no vale la pena.",
    "Es un producto normal, nada especial."
]

for review in reviews:
    sentiment = analyze_sentiment(review)
    print(f"Review: {review}")
    print(f"Sentimiento: {sentiment}\n")
```

### 9.3 Generador de resúmenes:

```python
import ollama

def summarize_text(text, max_words=50):
    prompt = f"""
    Resume el siguiente texto en máximo {max_words} palabras:
    
    {text}
    
    Resumen:
    """
    
    response = ollama.generate(
        model='llama3',
        prompt=prompt,
        options={
            'temperature': 0.3,
            'num_predict': max_words * 2
        }
    )
    
    return response['response'].strip()

article = """
La inteligencia artificial está transformando múltiples industrias.
Desde la medicina hasta el transporte, los sistemas de IA están
mejorando la eficiencia y creando nuevas oportunidades. Sin embargo,
también plantean desafíos éticos y sociales que debemos abordar
cuidadosamente para garantizar un desarrollo responsable.
"""

summary = summarize_text(article)
print(f"Resumen: {summary}")
```

---

## 🎯 10. Mejores prácticas

### 10.1 Gestión de recursos:

```python
import ollama
import time

def generate_with_timeout(prompt, timeout=30):
    start_time = time.time()
    
    try:
        response = ollama.generate(
            model='llama3',
            prompt=prompt,
            options={'num_predict': 100}
        )
        
        elapsed = time.time() - start_time
        
        if elapsed > timeout:
            return None, "Timeout excedido"
        
        return response['response'], None
        
    except Exception as e:
        return None, str(e)

result, error = generate_with_timeout("Explain quantum physics")

if error:
    print(f"Error: {error}")
else:
    print(f"Respuesta: {result}")
```

### 10.2 Manejo de errores:

```python
import ollama

def safe_generate(model, prompt, retries=3):
    for attempt in range(retries):
        try:
            response = ollama.generate(
                model=model,
                prompt=prompt
            )
            return response['response']
            
        except ollama.ResponseError as e:
            print(f"Error en intento {attempt + 1}: {e}")
            if attempt == retries - 1:
                return None
            time.sleep(2)
        
        except Exception as e:
            print(f"Error inesperado: {e}")
            return None

result = safe_generate('llama3', 'Hello!')
print(result)
```

### 10.3 Optimización de prompts:

```python
import ollama

def optimized_prompt(task, context, constraints=None):
    prompt_parts = [
        f"Task: {task}",
        f"Context: {context}"
    ]
    
    if constraints:
        prompt_parts.append(f"Constraints: {constraints}")
    
    prompt_parts.append("Response:")
    
    return "\n\n".join(prompt_parts)

task = "Generate a product description"
context = "Wireless headphones with noise cancellation"
constraints = "Maximum 50 words, focus on benefits"

prompt = optimized_prompt(task, context, constraints)

response = ollama.generate(
    model='llama3',
    prompt=prompt,
    options={'temperature': 0.7}
)

print(response['response'])
```

---

## 📊 11. Monitoreo y debugging

### 11.1 Ver logs de Ollama:

```bash
journalctl -u ollama -f
```

### 11.2 Verificar uso de recursos:

```bash
ollama ps
```

**Salida:**
```
NAME        ID              SIZE    PROCESSOR    UNTIL
llama3:8b   a6990ed6be41    4.7 GB  100% GPU     4 minutes from now
```

### 11.3 Debugging en Python:

```python
import ollama
import json

response = ollama.generate(
    model='llama3',
    prompt='Hello!',
    options={'temperature': 0.7}
)

print(json.dumps(response, indent=2))
```

---

## 🎓 12. Resumen ejecutivo

**Ollama** simplifica la ejecución de LLMs localmente:

✅ **Instalación simple:** Un comando  
✅ **Gestión automática:** Descarga y actualiza modelos fácilmente  
✅ **API REST:** Integración sencilla con aplicaciones  
✅ **Biblioteca Python:** Interfaz pythonica para desarrollo  
✅ **Múltiples modelos:** Llama 3, Mistral, CodeLlama y más  

**Comandos esenciales:**
```bash
ollama pull llama3
ollama run llama3
ollama list
ollama rm modelo
```

**Python básico:**
```python
import ollama
response = ollama.chat(model='llama3', messages=[...])
print(response['message']['content'])
```

---

## ✨ Conclusión

Ollama democratiza el acceso a LLMs potentes, eliminando la complejidad técnica y permitiendo que desarrolladores de todos los niveles puedan integrar IA avanzada en sus proyectos. Su simplicidad no sacrifica potencia, convirtiéndolo en la herramienta ideal para prototipado rápido y producción.

---

*Notas generadas para el curso "Working with Llama 3"*  
*Tema: Introducción a Ollama*
