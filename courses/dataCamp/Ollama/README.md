# 📚 Índice del Curso: Working with Llama 3

## Bienvenido al curso completo de Llama 3 y Ollama

Este repositorio contiene notas detalladas y completas sobre el uso de Llama 3, desde conceptos básicos hasta aplicaciones avanzadas.

---

## 📖 Contenido del Curso

### 📄 [01_Introduccion_Llama3.md](./01_Introduccion_Llama3.md) - Introducción a Llama 3
**Nivel:** Principiante
**Duración estimada:** 2-3 horas
**XP:** 50 XP

**Temas cubiertos:**
- ¿Qué es Llama 3?
- Ventajas de usar LLMs locales
- Instalación y configuración
- Primeros pasos con llama-cpp-python
- Generación básica de texto
- Manejo de respuestas

**Conceptos clave:**
- Modelos de lenguaje grandes (LLMs)
- Ejecución local vs cloud
- Formato GGUF
- Tokens y contexto

---

### 📄 [02_Tuning_Parameters.md](./02_Tuning_Parameters.md) - Tuning Llama 3 Parameters
**Nivel:** Principiante-Intermedio
**Duración estimada:** 3-4 horas
**XP:** 50 XP

**Temas cubiertos:**
- Parámetros de decodificación
- Temperature (temperatura)
- Top-k sampling
- Top-p (nucleus sampling)
- Max tokens
- Combinaciones de parámetros
- Casos de uso específicos

**Conceptos clave:**
- Control de creatividad vs precisión
- Optimización de respuestas
- Configuraciones recomendadas
- Trade-offs entre parámetros

**Ejemplos prácticos:**
- Generación de descripciones de productos
- Contenido técnico vs creativo
- Configuraciones para diferentes tareas

---

### 📄 [03_Introduccion_Ollama.md](./03_Introduccion_Ollama.md) - Introducción a Ollama
**Nivel:** Principiante  
**Duración estimada:** 2-3 horas

**Temas cubiertos:**
- ¿Qué es Ollama?
- Ollama vs llama-cpp-python
- Instalación en diferentes sistemas
- Comandos básicos de CLI
- API REST de Ollama
- Integración con Python
- Modelos disponibles
- Configuración avanzada

**Conceptos clave:**
- Gestión simplificada de modelos
- API REST para integración
- Modelfile personalizado
- Variables de entorno

**Ejemplos prácticos:**
- Chatbot local
- Analizador de sentimientos
- Generador de resúmenes
- Mejores prácticas

---

### 📄 [04_RAG_con_Llama.md](./04_RAG_con_Llama.md) - RAG (Retrieval Augmented Generation)
**Nivel:** Intermedio-Avanzado  
**Duración estimada:** 4-5 horas

**Temas cubiertos:**
- ¿Qué es RAG?
- Arquitectura de sistemas RAG
- Embeddings y vectores
- Bases de datos vectoriales (ChromaDB)
- Implementación básica de RAG
- RAG con LangChain
- Procesamiento de PDFs
- Técnicas avanzadas (re-ranking, hybrid search)

**Conceptos clave:**
- Búsqueda semántica
- Vector stores
- Chunking strategies
- Prompt engineering para RAG
- Evaluación de sistemas RAG

**Ejemplos prácticos:**
- RAG simple con ChromaDB
- RAG persistente con metadatos
- RAG con LangChain
- Análisis de documentos PDF
- Query expansion
- Monitoreo y debugging

---

### 📄 [05_Fine_tuning_Llama.md](./05_Fine_tuning_Llama.md) - Fine-tuning y Optimización
**Nivel:** Avanzado  
**Duración estimada:** 5-6 horas

**Temas cubiertos:**
- ¿Qué es fine-tuning?
- Tipos de fine-tuning (Full, LoRA, QLoRA, Prompt Tuning)
- Preparación de datos
- Fine-tuning con Unsloth
- Cuantización de modelos
- Pruning (poda)
- Distillation (destilación)
- Evaluación de modelos

**Conceptos clave:**
- Adaptación de modelos
- Eficiencia en memoria
- LoRA y QLoRA
- Formato de datos JSONL
- Hiperparámetros de entrenamiento

**Ejemplos prácticos:**
- Chatbot de soporte técnico
- Generador de código especializado
- Clasificador de sentimientos
- Troubleshooting común
- Benchmarking

---

### 📄 [06_Aplicaciones_Practicas.md](./06_Aplicaciones_Practicas.md) - Aplicaciones del Mundo Real
**Nivel:** Intermedio-Avanzado  
**Duración estimada:** 4-5 horas

**Temas cubiertos:**
- Arquitectura de aplicaciones con LLMs
- Chatbot inteligente con memoria
- Analizador de documentos
- Sistema de búsqueda semántica
- Integración con bases de datos
- Gestión de estado
- APIs y servicios web

**Conceptos clave:**
- Patrones de diseño
- Persistencia de datos
- Procesamiento de documentos
- Búsqueda híbrida
- Manejo de errores

**Proyectos completos:**
1. **Chatbot con memoria persistente**
   - Historial de conversaciones
   - Perfiles de usuario
   - Análisis de sentimientos
   - Resúmenes automáticos

2. **Analizador de documentos**
   - Soporte para PDF, DOCX, TXT
   - Resúmenes automáticos
   - Extracción de puntos clave
   - Clasificación de documentos
   - Extracción de entidades
   - Análisis de sentimientos
   - Comparación de documentos

3. **Motor de búsqueda semántica**
   - Indexación de documentos
   - Búsqueda con embeddings
   - Explicaciones generadas por LLM
   - Re-ranking de resultados
   - Query expansion

---

## 🎯 Ruta de Aprendizaje Recomendada

### Para Principiantes:
1. **01_Introduccion_Llama3.md** - Introducción a Llama 3
2. **03_Introduccion_Ollama.md** - Introducción a Ollama
3. **02_Tuning_Parameters.md** - Tuning Llama 3 Parameters

### Para Nivel Intermedio:
1. Completar ruta de principiantes
2. **04_RAG_con_Llama.md** - RAG
3. **06_Aplicaciones_Practicas.md** - Aplicaciones Prácticas

### Para Nivel Avanzado:
1. Completar rutas anteriores
2. **05_Fine_tuning_Llama.md** - Fine-tuning y Optimización
3. Proyectos personalizados

---

## 🛠️ Stack Tecnológico

### Bibliotecas principales:
```bash
pip install ollama
pip install llama-cpp-python
pip install sentence-transformers
pip install chromadb
pip install langchain
pip install langchain-community
pip install unsloth
pip install transformers
pip install datasets
pip install trl
```

### Herramientas adicionales:
```bash
pip install pypdf
pip install python-docx
pip install fastapi
pip install uvicorn
pip install sqlite3
```

---

## 📊 Resumen de XP y Progreso

| Archivo | Nivel | XP | Tiempo estimado |
|---------|-------|----|-----------------|
| 01_Introduccion_Llama3.md | Principiante | 50 | 2-3 horas |
| 02_Tuning_Parameters.md | Principiante-Intermedio | 50 | 3-4 horas |
| 03_Introduccion_Ollama.md | Principiante | 50 | 2-3 horas |
| 04_RAG_con_Llama.md | Intermedio-Avanzado | 100 | 4-5 horas |
| 05_Fine_tuning_Llama.md | Avanzado | 150 | 5-6 horas |
| 06_Aplicaciones_Practicas.md | Intermedio-Avanzado | 100 | 4-5 horas |
| **TOTAL** | | **500 XP** | **20-26 horas** |

---

## 🎓 Certificación

Al completar todos los módulos y proyectos prácticos, habrás adquirido:

✅ Conocimiento profundo de Llama 3 y LLMs locales  
✅ Habilidades en prompt engineering  
✅ Experiencia con RAG y búsqueda semántica  
✅ Capacidad de fine-tuning de modelos  
✅ Desarrollo de aplicaciones de IA completas  
✅ Optimización y deployment de modelos  

---

## 📚 Recursos Adicionales

### Documentación oficial:
- [Ollama Documentation](https://github.com/ollama/ollama)
- [llama-cpp-python](https://github.com/abetlen/llama-cpp-python)
- [LangChain Docs](https://python.langchain.com/)
- [ChromaDB Docs](https://docs.trychroma.com/)
- [Unsloth](https://github.com/unslothai/unsloth)

### Comunidades:
- [Ollama Discord](https://discord.gg/ollama)
- [Hugging Face Forums](https://discuss.huggingface.co/)
- [r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/)

### Modelos recomendados:
- **Llama 3 8B:** Uso general, balance calidad/velocidad
- **Llama 3 70B:** Máxima calidad, requiere GPU potente
- **Mistral 7B:** Alternativa eficiente
- **CodeLlama:** Especializado en código
- **Phi-3:** Para dispositivos limitados

---

## 💡 Consejos para el Aprendizaje

1. **Práctica constante:** Implementa cada ejemplo de código
2. **Experimenta:** Modifica parámetros y observa resultados
3. **Proyectos personales:** Aplica lo aprendido a tus propios casos de uso
4. **Comunidad:** Participa en foros y comparte tu progreso
5. **Documentación:** Lee la documentación oficial de las herramientas
6. **Iteración:** Mejora continuamente tus implementaciones

---

## 🚀 Próximos Pasos

Después de completar este curso, puedes:

1. **Crear aplicaciones productivas:**
   - Chatbots empresariales
   - Sistemas de análisis de documentos
   - Asistentes de código
   - Herramientas de investigación

2. **Contribuir a proyectos open source:**
   - Ollama
   - LangChain
   - ChromaDB
   - Unsloth

3. **Especializarte en áreas específicas:**
   - Multimodal AI (texto + imágenes)
   - Agentes autónomos
   - Fine-tuning avanzado
   - Optimización de rendimiento

4. **Mantenerte actualizado:**
   - Nuevas versiones de Llama
   - Técnicas emergentes
   - Mejores prácticas
   - Casos de uso innovadores

---

## ✨ Conclusión

Este curso te proporciona una base sólida para trabajar con Llama 3 y construir aplicaciones de IA avanzadas. La combinación de teoría, ejemplos prácticos y proyectos completos te prepara para crear soluciones reales que aprovechen el poder de los LLMs locales.

**¡Buena suerte en tu viaje de aprendizaje! 🎯**

---

*Curso: Working with Llama 3*  
*Plataforma: DataCamp*  
*Última actualización: 2024*
