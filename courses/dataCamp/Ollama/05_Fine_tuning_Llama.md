# Notas Completas: Fine-tuning y Optimización de Llama 3

## 📚 Curso: Working with Llama 3
**Tema:** Fine-tuning y Optimización Avanzada  
**Nivel:** Avanzado

---

## 🎯 1. ¿Qué es Fine-tuning?

### Definición:

**Fine-tuning** es el proceso de adaptar un modelo pre-entrenado a una tarea o dominio específico mediante entrenamiento adicional con datos personalizados.

### Analogía:

Imagina que tienes un chef profesional (modelo pre-entrenado):
- **Pre-entrenamiento:** Aprendió cocina general en escuela culinaria
- **Fine-tuning:** Se especializa en cocina italiana trabajando en un restaurante italiano
- **Resultado:** Mantiene habilidades generales pero domina un área específica

### ¿Por qué hacer fine-tuning?

✅ **Especialización:** Adapta el modelo a tu dominio específico  
✅ **Mejor rendimiento:** Supera modelos generales en tareas específicas  
✅ **Estilo personalizado:** Ajusta tono, formato y comportamiento  
✅ **Conocimiento específico:** Incorpora terminología y conceptos de tu industria  
✅ **Eficiencia:** Modelo más pequeño puede superar uno grande general  

---

## 🔄 2. Tipos de Fine-tuning

### 2.1 Full Fine-tuning:

**Descripción:** Actualiza todos los parámetros del modelo.

**Ventajas:**
- ✅ Máxima adaptación posible
- ✅ Mejor rendimiento en tarea específica

**Desventajas:**
- ❌ Requiere mucha memoria (GPU)
- ❌ Tiempo de entrenamiento largo
- ❌ Riesgo de overfitting
- ❌ Costoso computacionalmente

**Cuándo usar:**
- Tienes muchos datos (>10,000 ejemplos)
- Necesitas máxima precisión
- Tienes recursos GPU potentes

### 2.2 LoRA (Low-Rank Adaptation):

**Descripción:** Añade matrices de bajo rango a las capas del modelo, entrenando solo estas matrices adicionales.

**Ventajas:**
- ✅ Mucho más eficiente en memoria
- ✅ Entrenamiento más rápido
- ✅ Fácil de combinar múltiples adaptaciones
- ✅ Menos riesgo de overfitting

**Desventajas:**
- ❌ Ligeramente menos potente que full fine-tuning
- ❌ Requiere configuración de hiperparámetros

**Cuándo usar:**
- Recursos GPU limitados
- Múltiples tareas/dominios
- Prototipado rápido

### 2.3 QLoRA (Quantized LoRA):

**Descripción:** Combina LoRA con cuantización del modelo base.

**Ventajas:**
- ✅ Extremadamente eficiente en memoria
- ✅ Permite fine-tuning en GPUs consumer
- ✅ Mantiene calidad cercana a LoRA

**Desventajas:**
- ❌ Configuración más compleja
- ❌ Requiere bibliotecas específicas

**Cuándo usar:**
- GPU con memoria limitada (<16GB)
- Modelos grandes (70B parámetros)
- Presupuesto limitado

### 2.4 Prompt Tuning:

**Descripción:** Solo entrena embeddings de prompts especiales, modelo base congelado.

**Ventajas:**
- ✅ Extremadamente eficiente
- ✅ Muy rápido
- ✅ Mínimo almacenamiento

**Desventajas:**
- ❌ Menos potente que otros métodos
- ❌ Limitado a tareas similares al pre-entrenamiento

---

## 🛠️ 3. Preparación de datos para Fine-tuning

### 3.1 Formato de datos:

**Formato JSONL (recomendado):**

```json
{"instruction": "Clasifica el sentimiento", "input": "Me encanta este producto!", "output": "POSITIVO"}
{"instruction": "Clasifica el sentimiento", "input": "Muy decepcionado", "output": "NEGATIVO"}
{"instruction": "Clasifica el sentimiento", "input": "Es un producto normal", "output": "NEUTRAL"}
```

**Formato conversacional:**

```json
{
  "messages": [
    {"role": "system", "content": "Eres un asistente experto en Python"},
    {"role": "user", "content": "¿Cómo creo una lista?"},
    {"role": "assistant", "content": "Usa corchetes: mi_lista = [1, 2, 3]"}
  ]
}
```

### 3.2 Script de preparación de datos:

```python
import json
import random

def create_training_data(examples, output_file="training_data.jsonl"):
    """
    Crea archivo JSONL para fine-tuning
    
    Args:
        examples: Lista de diccionarios con 'instruction', 'input', 'output'
        output_file: Nombre del archivo de salida
    """
    with open(output_file, 'w', encoding='utf-8') as f:
        for example in examples:
            json_line = json.dumps(example, ensure_ascii=False)
            f.write(json_line + '\n')
    
    print(f"✅ {len(examples)} ejemplos guardados en {output_file}")

def validate_training_data(file_path):
    """Valida formato de datos de entrenamiento"""
    with open(file_path, 'r', encoding='utf-8') as f:
        lines = f.readlines()
    
    errors = []
    
    for i, line in enumerate(lines, 1):
        try:
            data = json.loads(line)
            
            if 'instruction' not in data:
                errors.append(f"Línea {i}: Falta 'instruction'")
            if 'output' not in data:
                errors.append(f"Línea {i}: Falta 'output'")
            
            if len(data.get('output', '')) < 5:
                errors.append(f"Línea {i}: Output muy corto")
                
        except json.JSONDecodeError:
            errors.append(f"Línea {i}: JSON inválido")
    
    if errors:
        print("❌ Errores encontrados:")
        for error in errors[:10]:
            print(f"  - {error}")
        return False
    else:
        print(f"✅ {len(lines)} ejemplos validados correctamente")
        return True

def split_dataset(input_file, train_ratio=0.8):
    """Divide dataset en train y validation"""
    with open(input_file, 'r', encoding='utf-8') as f:
        lines = f.readlines()
    
    random.shuffle(lines)
    
    split_idx = int(len(lines) * train_ratio)
    train_lines = lines[:split_idx]
    val_lines = lines[split_idx:]
    
    with open('train.jsonl', 'w', encoding='utf-8') as f:
        f.writelines(train_lines)
    
    with open('validation.jsonl', 'w', encoding='utf-8') as f:
        f.writelines(val_lines)
    
    print(f"✅ Dataset dividido:")
    print(f"   Train: {len(train_lines)} ejemplos")
    print(f"   Validation: {len(val_lines)} ejemplos")

if __name__ == "__main__":
    examples = [
        {
            "instruction": "Traduce al español",
            "input": "Hello, how are you?",
            "output": "Hola, ¿cómo estás?"
        },
        {
            "instruction": "Traduce al español",
            "input": "Good morning",
            "output": "Buenos días"
        },
        {
            "instruction": "Traduce al español",
            "input": "Thank you very much",
            "output": "Muchas gracias"
        }
    ]
    
    create_training_data(examples)
    validate_training_data("training_data.jsonl")
    split_dataset("training_data.jsonl")
```

### 3.3 Mejores prácticas para datos:

**Cantidad:**
- Mínimo: 100-500 ejemplos
- Recomendado: 1,000-10,000 ejemplos
- Óptimo: 10,000+ ejemplos

**Calidad:**
- ✅ Ejemplos diversos y representativos
- ✅ Outputs consistentes en formato
- ✅ Instrucciones claras y específicas
- ✅ Balance entre categorías
- ❌ Evitar duplicados
- ❌ Evitar ejemplos contradictorios

**Formato:**
- Longitud consistente
- Estructura uniforme
- Codificación UTF-8
- Sin caracteres especiales problemáticos

---

## 🚀 4. Fine-tuning con Unsloth (Recomendado)

### 4.1 ¿Qué es Unsloth?

**Unsloth** es una biblioteca optimizada para fine-tuning eficiente de LLMs.

**Ventajas:**
- ✅ 2-5x más rápido que métodos tradicionales
- ✅ Usa 70% menos memoria
- ✅ Soporte para LoRA y QLoRA
- ✅ Fácil de usar
- ✅ Compatible con Llama 3

### 4.2 Instalación:

```bash
pip install unsloth
pip install "unsloth[colab-new] @ git+https://github.com/unslothai/unsloth.git"
pip install --no-deps trl peft accelerate bitsandbytes
```

### 4.3 Script completo de fine-tuning:

```python
from unsloth import FastLanguageModel
import torch
from datasets import load_dataset
from trl import SFTTrainer
from transformers import TrainingArguments

max_seq_length = 2048
dtype = None
load_in_4bit = True

model, tokenizer = FastLanguageModel.from_pretrained(
    model_name="unsloth/llama-3-8b-bnb-4bit",
    max_seq_length=max_seq_length,
    dtype=dtype,
    load_in_4bit=load_in_4bit,
)

model = FastLanguageModel.get_peft_model(
    model,
    r=16,
    target_modules=["q_proj", "k_proj", "v_proj", "o_proj",
                    "gate_proj", "up_proj", "down_proj"],
    lora_alpha=16,
    lora_dropout=0,
    bias="none",
    use_gradient_checkpointing="unsloth",
    random_state=3407,
    use_rslora=False,
    loftq_config=None,
)

alpaca_prompt = """Below is an instruction that describes a task, paired with an input that provides further context. Write a response that appropriately completes the request.

### Instruction:
{}

### Input:
{}

### Response:
{}"""

EOS_TOKEN = tokenizer.eos_token

def formatting_prompts_func(examples):
    instructions = examples["instruction"]
    inputs = examples["input"]
    outputs = examples["output"]
    texts = []
    
    for instruction, input, output in zip(instructions, inputs, outputs):
        text = alpaca_prompt.format(instruction, input, output) + EOS_TOKEN
        texts.append(text)
    
    return {"text": texts}

dataset = load_dataset("json", data_files="training_data.jsonl", split="train")
dataset = dataset.map(formatting_prompts_func, batched=True)

trainer = SFTTrainer(
    model=model,
    tokenizer=tokenizer,
    train_dataset=dataset,
    dataset_text_field="text",
    max_seq_length=max_seq_length,
    dataset_num_proc=2,
    packing=False,
    args=TrainingArguments(
        per_device_train_batch_size=2,
        gradient_accumulation_steps=4,
        warmup_steps=5,
        max_steps=60,
        learning_rate=2e-4,
        fp16=not torch.cuda.is_bf16_supported(),
        bf16=torch.cuda.is_bf16_supported(),
        logging_steps=1,
        optim="adamw_8bit",
        weight_decay=0.01,
        lr_scheduler_type="linear",
        seed=3407,
        output_dir="outputs",
    ),
)

trainer_stats = trainer.train()

print("✅ Fine-tuning completado!")
print(f"Tiempo de entrenamiento: {trainer_stats.metrics['train_runtime']:.2f}s")

model.save_pretrained("lora_model")
tokenizer.save_pretrained("lora_model")

print("✅ Modelo guardado en ./lora_model")
```

### 4.4 Inferencia con modelo fine-tuned:

```python
from unsloth import FastLanguageModel

model, tokenizer = FastLanguageModel.from_pretrained(
    model_name="lora_model",
    max_seq_length=2048,
    dtype=None,
    load_in_4bit=True,
)

FastLanguageModel.for_inference(model)

alpaca_prompt = """Below is an instruction that describes a task, paired with an input that provides further context. Write a response that appropriately completes the request.

### Instruction:
{}

### Input:
{}

### Response:
{}"""

def generate_response(instruction, input_text=""):
    """Genera respuesta con modelo fine-tuned"""
    prompt = alpaca_prompt.format(
        instruction,
        input_text,
        ""
    )
    
    inputs = tokenizer([prompt], return_tensors="pt").to("cuda")
    
    outputs = model.generate(
        **inputs,
        max_new_tokens=256,
        temperature=0.7,
        top_p=0.9,
        use_cache=True
    )
    
    response = tokenizer.batch_decode(outputs)[0]
    
    response = response.split("### Response:")[1].strip()
    response = response.replace(tokenizer.eos_token, "")
    
    return response

instruction = "Clasifica el sentimiento del siguiente texto"
input_text = "Este producto superó todas mis expectativas!"

response = generate_response(instruction, input_text)
print(f"Respuesta: {response}")
```

---

## ⚡ 5. Optimización de modelos

### 5.1 Cuantización:

**¿Qué es?**
Reducir la precisión de los pesos del modelo para ahorrar memoria.

**Tipos:**

| Tipo | Bits | Tamaño | Calidad | Uso |
|------|------|--------|---------|-----|
| **FP32** | 32 | 100% | Máxima | Entrenamiento |
| **FP16** | 16 | 50% | Muy alta | Inferencia GPU |
| **INT8** | 8 | 25% | Alta | Inferencia general |
| **INT4** | 4 | 12.5% | Buena | Dispositivos limitados |

**Cuantización con llama.cpp:**

```bash
python convert.py modelo_original.bin --outtype q4_0 --outfile modelo_q4.gguf
```

**Cuantización con Ollama:**

```bash
ollama pull llama3:8b-q4_0
ollama pull llama3:8b-q8_0
```

### 5.2 Pruning (Poda):

**Descripción:** Eliminar conexiones/neuronas menos importantes.

```python
import torch
import torch.nn.utils.prune as prune

def prune_model(model, amount=0.3):
    """
    Aplica pruning al modelo
    
    Args:
        model: Modelo PyTorch
        amount: Porcentaje de pesos a eliminar (0-1)
    """
    for name, module in model.named_modules():
        if isinstance(module, torch.nn.Linear):
            prune.l1_unstructured(module, name='weight', amount=amount)
            prune.remove(module, 'weight')
    
    return model

pruned_model = prune_model(model, amount=0.3)
print("✅ Modelo podado (30% de pesos eliminados)")
```

### 5.3 Distillation (Destilación):

**Descripción:** Entrenar un modelo pequeño para imitar uno grande.

```python
import torch
import torch.nn as nn
import torch.nn.functional as F

class DistillationTrainer:
    def __init__(self, teacher_model, student_model, temperature=2.0, alpha=0.5):
        self.teacher = teacher_model
        self.student = student_model
        self.temperature = temperature
        self.alpha = alpha
    
    def distillation_loss(self, student_logits, teacher_logits, labels):
        """Calcula pérdida de destilación"""
        soft_targets = F.softmax(teacher_logits / self.temperature, dim=-1)
        soft_prob = F.log_softmax(student_logits / self.temperature, dim=-1)
        
        soft_loss = F.kl_div(soft_prob, soft_targets, reduction='batchmean')
        soft_loss = soft_loss * (self.temperature ** 2)
        
        hard_loss = F.cross_entropy(student_logits, labels)
        
        total_loss = self.alpha * soft_loss + (1 - self.alpha) * hard_loss
        
        return total_loss
    
    def train_step(self, inputs, labels):
        """Un paso de entrenamiento"""
        with torch.no_grad():
            teacher_logits = self.teacher(inputs)
        
        student_logits = self.student(inputs)
        
        loss = self.distillation_loss(student_logits, teacher_logits, labels)
        
        return loss

teacher = load_model("llama3-70b")
student = load_model("llama3-8b")

trainer = DistillationTrainer(teacher, student)
```

---

## 📊 6. Evaluación de modelos fine-tuned

### 6.1 Métricas básicas:

```python
from sklearn.metrics import accuracy_score, precision_recall_fscore_support
import numpy as np

def evaluate_model(model, test_data):
    """Evalúa modelo en datos de prueba"""
    predictions = []
    ground_truth = []
    
    for example in test_data:
        pred = model.generate(example['input'])
        predictions.append(pred)
        ground_truth.append(example['output'])
    
    accuracy = accuracy_score(ground_truth, predictions)
    precision, recall, f1, _ = precision_recall_fscore_support(
        ground_truth, predictions, average='weighted'
    )
    
    return {
        'accuracy': accuracy,
        'precision': precision,
        'recall': recall,
        'f1': f1
    }

metrics = evaluate_model(fine_tuned_model, test_dataset)
print(f"Accuracy: {metrics['accuracy']:.3f}")
print(f"F1 Score: {metrics['f1']:.3f}")
```

### 6.2 Evaluación cualitativa:

```python
def qualitative_evaluation(model, test_cases):
    """Evaluación manual de calidad"""
    results = []
    
    for i, case in enumerate(test_cases, 1):
        print(f"\n{'='*60}")
        print(f"Caso {i}:")
        print(f"Input: {case['input']}")
        print(f"Expected: {case['expected']}")
        
        prediction = model.generate(case['input'])
        print(f"Predicted: {prediction}")
        
        rating = input("Calificación (1-5): ")
        
        results.append({
            'case': i,
            'rating': int(rating),
            'prediction': prediction
        })
    
    avg_rating = np.mean([r['rating'] for r in results])
    print(f"\n✅ Calificación promedio: {avg_rating:.2f}/5")
    
    return results

test_cases = [
    {
        'input': "Clasifica: Me encanta este producto",
        'expected': "POSITIVO"
    },
    {
        'input': "Clasifica: Muy decepcionado",
        'expected': "NEGATIVO"
    }
]

qualitative_evaluation(fine_tuned_model, test_cases)
```

### 6.3 Benchmark comparativo:

```python
import time

def benchmark_models(models, test_data):
    """Compara múltiples modelos"""
    results = {}
    
    for model_name, model in models.items():
        print(f"\nEvaluando {model_name}...")
        
        start_time = time.time()
        predictions = []
        
        for example in test_data:
            pred = model.generate(example['input'])
            predictions.append(pred)
        
        elapsed_time = time.time() - start_time
        
        accuracy = accuracy_score(
            [ex['output'] for ex in test_data],
            predictions
        )
        
        results[model_name] = {
            'accuracy': accuracy,
            'time': elapsed_time,
            'speed': len(test_data) / elapsed_time
        }
    
    print("\n📊 Resultados:")
    print(f"{'Modelo':<20} {'Accuracy':<12} {'Tiempo':<12} {'Ejemplos/s'}")
    print("-" * 60)
    
    for model_name, metrics in results.items():
        print(f"{model_name:<20} {metrics['accuracy']:<12.3f} "
              f"{metrics['time']:<12.2f} {metrics['speed']:.2f}")
    
    return results

models = {
    'Base Llama3': base_model,
    'Fine-tuned': fine_tuned_model,
    'Fine-tuned + Quantized': quantized_model
}

benchmark_models(models, test_dataset)
```

---

## 🎯 7. Casos de uso de Fine-tuning

### 7.1 Chatbot de soporte técnico:

```python
training_examples = [
    {
        "instruction": "Responde como agente de soporte técnico",
        "input": "Mi aplicación no abre",
        "output": "Entiendo tu frustración. Intentemos estos pasos:\n1. Reinicia tu dispositivo\n2. Verifica actualizaciones\n3. Reinstala la app si persiste\n¿Cuál es tu sistema operativo?"
    },
    {
        "instruction": "Responde como agente de soporte técnico",
        "input": "Olvidé mi contraseña",
        "output": "Sin problema, puedo ayudarte. Haz clic en '¿Olvidaste tu contraseña?' en la pantalla de inicio de sesión. Recibirás un correo con instrucciones para restablecerla."
    }
]
```

### 7.2 Generador de código específico:

```python
training_examples = [
    {
        "instruction": "Genera código Python para la tarea",
        "input": "Función para validar email",
        "output": """import re

def validate_email(email):
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$'
    return bool(re.match(pattern, email))"""
    },
    {
        "instruction": "Genera código Python para la tarea",
        "input": "Clase para manejar conexión a base de datos",
        "output": """import sqlite3

class DatabaseConnection:
    def __init__(self, db_path):
        self.db_path = db_path
        self.conn = None
    
    def __enter__(self):
        self.conn = sqlite3.connect(self.db_path)
        return self.conn
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.conn:
            self.conn.close()"""
    }
]
```

### 7.3 Clasificador de sentimientos personalizado:

```python
training_examples = [
    {
        "instruction": "Clasifica el sentimiento y explica",
        "input": "Este producto superó mis expectativas",
        "output": "POSITIVO - El cliente expresa satisfacción al mencionar que el producto 'superó expectativas', indicando una experiencia muy favorable."
    },
    {
        "instruction": "Clasifica el sentimiento y explica",
        "input": "No funciona como esperaba",
        "output": "NEGATIVO - El cliente muestra decepción al indicar que el producto no cumplió sus expectativas de funcionamiento."
    }
]
```

---

## 🔧 8. Troubleshooting común

### 8.1 Out of Memory (OOM):

**Soluciones:**

```python
training_args = TrainingArguments(
    per_device_train_batch_size=1,
    gradient_accumulation_steps=8,
    gradient_checkpointing=True,
    fp16=True,
    optim="adamw_8bit",
)

model = FastLanguageModel.from_pretrained(
    model_name="llama-3-8b",
    load_in_4bit=True,
    max_seq_length=1024,
)
```

### 8.2 Overfitting:

**Soluciones:**

```python
training_args = TrainingArguments(
    num_train_epochs=3,
    learning_rate=2e-5,
    weight_decay=0.01,
    warmup_ratio=0.1,
    evaluation_strategy="steps",
    eval_steps=100,
    save_strategy="steps",
    save_steps=100,
    load_best_model_at_end=True,
)
```

### 8.3 Convergencia lenta:

**Soluciones:**

```python
training_args = TrainingArguments(
    learning_rate=5e-4,
    lr_scheduler_type="cosine",
    warmup_steps=100,
    max_grad_norm=1.0,
)
```

---

## 🎓 9. Resumen ejecutivo

**Fine-tuning** adapta Llama 3 a tareas específicas:

**Métodos:**
- **Full Fine-tuning:** Máxima adaptación, requiere muchos recursos
- **LoRA:** Eficiente, recomendado para la mayoría de casos
- **QLoRA:** Muy eficiente, ideal para GPUs limitadas
- **Prompt Tuning:** Rápido pero limitado

**Proceso:**
1. Preparar datos (JSONL format)
2. Elegir método (LoRA recomendado)
3. Configurar hiperparámetros
4. Entrenar modelo
5. Evaluar y ajustar
6. Desplegar

**Herramientas recomendadas:**
- **Unsloth:** Rápido y eficiente
- **Hugging Face TRL:** Completo y flexible
- **Axolotl:** Configuración simplificada

**Optimización:**
- Cuantización (INT4/INT8)
- Pruning (eliminar pesos)
- Distillation (modelo pequeño)

---

## ✨ Conclusión

Fine-tuning transforma Llama 3 de un modelo general a un experto especializado en tu dominio. Con las herramientas modernas como Unsloth y técnicas como LoRA, el proceso es accesible incluso con recursos limitados, permitiendo crear soluciones de IA personalizadas y de alta calidad.

---

*Notas generadas para el curso "Working with Llama 3"*  
*Tema: Fine-tuning y Optimización Avanzada*
