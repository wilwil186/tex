# Notas Completas: Aplicaciones Prácticas con Llama 3

## 📚 Curso: Working with Llama 3
**Tema:** Proyectos y Aplicaciones del Mundo Real  
**Nivel:** Intermedio-Avanzado

---

## 🎯 1. Arquitectura de aplicaciones con LLMs

### 1.1 Patrones de diseño comunes:

```
┌─────────────────────────────────────────────────┐
│         APLICACIÓN CON LLM                      │
├─────────────────────────────────────────────────┤
│                                                 │
│  ┌──────────────┐                               │
│  │   Frontend   │ (Web/Mobile/CLI)              │
│  └──────┬───────┘                               │
│         │                                        │
│         ▼                                        │
│  ┌──────────────┐                               │
│  │   API Layer  │ (FastAPI/Flask)               │
│  └──────┬───────┘                               │
│         │                                        │
│         ▼                                        │
│  ┌──────────────────────────────────┐           │
│  │   Business Logic                 │           │
│  │   - Prompt Engineering           │           │
│  │   - Context Management           │           │
│  │   - Response Processing          │           │
│  └──────┬───────────────────────────┘           │
│         │                                        │
│         ▼                                        │
│  ┌──────────────┐      ┌──────────────┐         │
│  │  LLM Service │◄────►│  Vector DB   │         │
│  │  (Ollama)    │      │  (ChromaDB)  │         │
│  └──────────────┘      └──────────────┘         │
│         │                                        │
│         ▼                                        │
│  ┌──────────────┐                               │
│  │   Database   │ (PostgreSQL/SQLite)           │
│  └──────────────┘                               │
└─────────────────────────────────────────────────┘
```

---

## 💬 2. Proyecto 1: Chatbot Inteligente con Memoria

### 2.1 Arquitectura:

```python
import ollama
import json
import sqlite3
from datetime import datetime
from typing import List, Dict

class IntelligentChatbot:
    def __init__(self, model='llama3', db_path='chatbot.db'):
        self.model = model
        self.db_path = db_path
        self._init_database()
    
    def _init_database(self):
        """Inicializa base de datos para historial"""
        conn = sqlite3.connect(self.db_path)
        cursor = conn.cursor()
        
        cursor.execute('''
            CREATE TABLE IF NOT EXISTS conversations (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                session_id TEXT,
                role TEXT,
                content TEXT,
                timestamp DATETIME DEFAULT CURRENT_TIMESTAMP
            )
        ''')
        
        cursor.execute('''
            CREATE TABLE IF NOT EXISTS user_profiles (
                session_id TEXT PRIMARY KEY,
                name TEXT,
                preferences TEXT,
                created_at DATETIME DEFAULT CURRENT_TIMESTAMP
            )
        ''')
        
        conn.commit()
        conn.close()
        
        print("✅ Base de datos inicializada")
    
    def save_message(self, session_id: str, role: str, content: str):
        """Guarda mensaje en historial"""
        conn = sqlite3.connect(self.db_path)
        cursor = conn.cursor()
        
        cursor.execute(
            'INSERT INTO conversations (session_id, role, content) VALUES (?, ?, ?)',
            (session_id, role, content)
        )
        
        conn.commit()
        conn.close()
    
    def get_conversation_history(self, session_id: str, limit: int = 10) -> List[Dict]:
        """Recupera historial de conversación"""
        conn = sqlite3.connect(self.db_path)
        cursor = conn.cursor()
        
        cursor.execute('''
            SELECT role, content, timestamp 
            FROM conversations 
            WHERE session_id = ? 
            ORDER BY timestamp DESC 
            LIMIT ?
        ''', (session_id, limit))
        
        messages = []
        for row in reversed(cursor.fetchall()):
            messages.append({
                'role': row[0],
                'content': row[1],
                'timestamp': row[2]
            })
        
        conn.close()
        return messages
    
    def save_user_profile(self, session_id: str, name: str, preferences: Dict):
        """Guarda perfil de usuario"""
        conn = sqlite3.connect(self.db_path)
        cursor = conn.cursor()
        
        cursor.execute('''
            INSERT OR REPLACE INTO user_profiles (session_id, name, preferences)
            VALUES (?, ?, ?)
        ''', (session_id, name, json.dumps(preferences)))
        
        conn.commit()
        conn.close()
    
    def get_user_profile(self, session_id: str) -> Dict:
        """Recupera perfil de usuario"""
        conn = sqlite3.connect(self.db_path)
        cursor = conn.cursor()
        
        cursor.execute(
            'SELECT name, preferences FROM user_profiles WHERE session_id = ?',
            (session_id,)
        )
        
        row = cursor.fetchone()
        conn.close()
        
        if row:
            return {
                'name': row[0],
                'preferences': json.loads(row[1])
            }
        return None
    
    def chat(self, session_id: str, user_message: str) -> str:
        """Procesa mensaje y genera respuesta"""
        history = self.get_conversation_history(session_id)
        profile = self.get_user_profile(session_id)
        
        messages = []
        
        system_prompt = "Eres un asistente útil y amigable."
        if profile:
            system_prompt += f" El usuario se llama {profile['name']}."
            if profile['preferences']:
                prefs = profile['preferences']
                system_prompt += f" Preferencias: {', '.join([f'{k}: {v}' for k, v in prefs.items()])}."
        
        messages.append({
            'role': 'system',
            'content': system_prompt
        })
        
        for msg in history[-5:]:
            messages.append({
                'role': msg['role'],
                'content': msg['content']
            })
        
        messages.append({
            'role': 'user',
            'content': user_message
        })
        
        response = ollama.chat(
            model=self.model,
            messages=messages
        )
        
        assistant_message = response['message']['content']
        
        self.save_message(session_id, 'user', user_message)
        self.save_message(session_id, 'assistant', assistant_message)
        
        return assistant_message
    
    def analyze_sentiment(self, text: str) -> str:
        """Analiza sentimiento del mensaje"""
        prompt = f"""
        Analiza el sentimiento del siguiente mensaje y clasifícalo como:
        POSITIVO, NEGATIVO, o NEUTRAL
        
        Mensaje: "{text}"
        
        Responde solo con la clasificación.
        """
        
        response = ollama.generate(
            model=self.model,
            prompt=prompt,
            options={'temperature': 0.1}
        )
        
        return response['response'].strip()
    
    def get_conversation_summary(self, session_id: str) -> str:
        """Genera resumen de la conversación"""
        history = self.get_conversation_history(session_id, limit=20)
        
        conversation_text = "\n".join([
            f"{msg['role']}: {msg['content']}"
            for msg in history
        ])
        
        prompt = f"""
        Resume la siguiente conversación en 2-3 oraciones:
        
        {conversation_text}
        
        Resumen:
        """
        
        response = ollama.generate(
            model=self.model,
            prompt=prompt,
            options={'temperature': 0.3}
        )
        
        return response['response'].strip()

if __name__ == "__main__":
    chatbot = IntelligentChatbot()
    
    session_id = "user_123"
    
    chatbot.save_user_profile(
        session_id,
        name="Ana",
        preferences={'idioma': 'español', 'tono': 'formal'}
    )
    
    print("Chatbot iniciado. Escribe 'salir' para terminar.\n")
    
    while True:
        user_input = input("Tú: ")
        
        if user_input.lower() == 'salir':
            summary = chatbot.get_conversation_summary(session_id)
            print(f"\n📝 Resumen de la conversación:\n{summary}")
            break
        
        if user_input.lower() == 'sentimiento':
            last_msg = chatbot.get_conversation_history(session_id, limit=1)
            if last_msg:
                sentiment = chatbot.analyze_sentiment(last_msg[0]['content'])
                print(f"Sentimiento detectado: {sentiment}\n")
            continue
        
        response = chatbot.chat(session_id, user_input)
        print(f"Bot: {response}\n")
```

---

## 📄 3. Proyecto 2: Analizador de Documentos

### 3.1 Sistema completo de análisis:

```python
import ollama
from pathlib import Path
import PyPDF2
import docx
from typing import List, Dict

class DocumentAnalyzer:
    def __init__(self, model='llama3'):
        self.model = model
    
    def read_pdf(self, file_path: str) -> str:
        """Lee contenido de PDF"""
        text = ""
        with open(file_path, 'rb') as file:
            pdf_reader = PyPDF2.PdfReader(file)
            for page in pdf_reader.pages:
                text += page.extract_text()
        return text
    
    def read_docx(self, file_path: str) -> str:
        """Lee contenido de DOCX"""
        doc = docx.Document(file_path)
        text = "\n".join([paragraph.text for paragraph in doc.paragraphs])
        return text
    
    def read_txt(self, file_path: str) -> str:
        """Lee contenido de TXT"""
        with open(file_path, 'r', encoding='utf-8') as file:
            return file.read()
    
    def read_document(self, file_path: str) -> str:
        """Lee documento según extensión"""
        path = Path(file_path)
        extension = path.suffix.lower()
        
        if extension == '.pdf':
            return self.read_pdf(file_path)
        elif extension == '.docx':
            return self.read_docx(file_path)
        elif extension == '.txt':
            return self.read_txt(file_path)
        else:
            raise ValueError(f"Formato no soportado: {extension}")
    
    def summarize(self, text: str, max_words: int = 150) -> str:
        """Genera resumen del documento"""
        prompt = f"""
        Resume el siguiente texto en máximo {max_words} palabras.
        Captura los puntos principales y conclusiones.
        
        Texto:
        {text[:4000]}
        
        Resumen:
        """
        
        response = ollama.generate(
            model=self.model,
            prompt=prompt,
            options={'temperature': 0.3}
        )
        
        return response['response'].strip()
    
    def extract_key_points(self, text: str, num_points: int = 5) -> List[str]:
        """Extrae puntos clave del documento"""
        prompt = f"""
        Extrae los {num_points} puntos más importantes del siguiente texto.
        Lista cada punto en una línea separada, comenzando con un guion.
        
        Texto:
        {text[:4000]}
        
        Puntos clave:
        """
        
        response = ollama.generate(
            model=self.model,
            prompt=prompt,
            options={'temperature': 0.2}
        )
        
        points = [
            line.strip().lstrip('-').strip()
            for line in response['response'].strip().split('\n')
            if line.strip()
        ]
        
        return points[:num_points]
    
    def classify_document(self, text: str, categories: List[str]) -> str:
        """Clasifica documento en categorías"""
        categories_str = ", ".join(categories)
        
        prompt = f"""
        Clasifica el siguiente documento en una de estas categorías:
        {categories_str}
        
        Responde solo con el nombre de la categoría.
        
        Documento:
        {text[:3000]}
        
        Categoría:
        """
        
        response = ollama.generate(
            model=self.model,
            prompt=prompt,
            options={'temperature': 0.1}
        )
        
        return response['response'].strip()
    
    def extract_entities(self, text: str) -> Dict[str, List[str]]:
        """Extrae entidades nombradas"""
        prompt = f"""
        Extrae las siguientes entidades del texto:
        - Personas
        - Organizaciones
        - Lugares
        - Fechas
        
        Formato de respuesta:
        Personas: [lista]
        Organizaciones: [lista]
        Lugares: [lista]
        Fechas: [lista]
        
        Texto:
        {text[:3000]}
        
        Entidades:
        """
        
        response = ollama.generate(
            model=self.model,
            prompt=prompt,
            options={'temperature': 0.2}
        )
        
        entities = {
            'personas': [],
            'organizaciones': [],
            'lugares': [],
            'fechas': []
        }
        
        lines = response['response'].strip().split('\n')
        current_category = None
        
        for line in lines:
            line = line.strip()
            if line.startswith('Personas:'):
                current_category = 'personas'
                content = line.replace('Personas:', '').strip()
                if content:
                    entities['personas'].extend([x.strip() for x in content.split(',')])
            elif line.startswith('Organizaciones:'):
                current_category = 'organizaciones'
                content = line.replace('Organizaciones:', '').strip()
                if content:
                    entities['organizaciones'].extend([x.strip() for x in content.split(',')])
            elif line.startswith('Lugares:'):
                current_category = 'lugares'
                content = line.replace('Lugares:', '').strip()
                if content:
                    entities['lugares'].extend([x.strip() for x in content.split(',')])
            elif line.startswith('Fechas:'):
                current_category = 'fechas'
                content = line.replace('Fechas:', '').strip()
                if content:
                    entities['fechas'].extend([x.strip() for x in content.split(',')])
        
        return entities
    
    def analyze_sentiment(self, text: str) -> Dict[str, any]:
        """Analiza sentimiento del documento"""
        prompt = f"""
        Analiza el sentimiento general del siguiente texto.
        
        Proporciona:
        1. Sentimiento general (POSITIVO/NEGATIVO/NEUTRAL)
        2. Nivel de confianza (1-10)
        3. Breve explicación
        
        Texto:
        {text[:3000]}
        
        Análisis:
        """
        
        response = ollama.generate(
            model=self.model,
            prompt=prompt,
            options={'temperature': 0.3}
        )
        
        return {
            'analysis': response['response'].strip(),
            'raw_text': text[:500]
        }
    
    def compare_documents(self, text1: str, text2: str) -> str:
        """Compara dos documentos"""
        prompt = f"""
        Compara los siguientes dos documentos e identifica:
        1. Similitudes principales
        2. Diferencias clave
        3. Conclusión sobre la relación entre ambos
        
        Documento 1:
        {text1[:2000]}
        
        Documento 2:
        {text2[:2000]}
        
        Comparación:
        """
        
        response = ollama.generate(
            model=self.model,
            prompt=prompt,
            options={'temperature': 0.4}
        )
        
        return response['response'].strip()
    
    def full_analysis(self, file_path: str) -> Dict:
        """Análisis completo del documento"""
        print(f"📄 Analizando: {file_path}")
        
        text = self.read_document(file_path)
        
        print("  ⏳ Generando resumen...")
        summary = self.summarize(text)
        
        print("  ⏳ Extrayendo puntos clave...")
        key_points = self.extract_key_points(text)
        
        print("  ⏳ Extrayendo entidades...")
        entities = self.extract_entities(text)
        
        print("  ⏳ Analizando sentimiento...")
        sentiment = self.analyze_sentiment(text)
        
        return {
            'file': file_path,
            'word_count': len(text.split()),
            'summary': summary,
            'key_points': key_points,
            'entities': entities,
            'sentiment': sentiment
        }

if __name__ == "__main__":
    analyzer = DocumentAnalyzer()
    
    file_path = "documento.pdf"
    
    analysis = analyzer.full_analysis(file_path)
    
    print("\n" + "="*60)
    print("📊 ANÁLISIS COMPLETO")
    print("="*60)
    
    print(f"\n📄 Archivo: {analysis['file']}")
    print(f"📝 Palabras: {analysis['word_count']}")
    
    print(f"\n📋 Resumen:")
    print(analysis['summary'])
    
    print(f"\n🔑 Puntos clave:")
    for i, point in enumerate(analysis['key_points'], 1):
        print(f"  {i}. {point}")
    
    print(f"\n👥 Entidades:")
    for category, items in analysis['entities'].items():
        if items:
            print(f"  {category.capitalize()}: {', '.join(items)}")
    
    print(f"\n💭 Sentimiento:")
    print(analysis['sentiment']['analysis'])
```

---

## 🔍 4. Proyecto 3: Sistema de Búsqueda Semántica

### 4.1 Motor de búsqueda inteligente:

```python
import ollama
from sentence_transformers import SentenceTransformer
import chromadb
from typing import List, Dict
import json

class SemanticSearchEngine:
    def __init__(self, model='llama3', collection_name='documents'):
        self.llm_model = model
        self.embedding_model = SentenceTransformer('all-MiniLM-L6-v2')
        
        self.client = chromadb.PersistentClient(path="./search_db")
        
        try:
            self.collection = self.client.get_collection(collection_name)
            print(f"✅ Colección '{collection_name}' cargada")
        except:
            self.collection = self.client.create_collection(
                name=collection_name,
                metadata={"hnsw:space": "cosine"}
            )
            print(f"✅ Nueva colección '{collection_name}' creada")
    
    def index_documents(self, documents: List[Dict]):
        """Indexa documentos para búsqueda"""
        print(f"📚 Indexando {len(documents)} documentos...")
        
        texts = [doc['content'] for doc in documents]
        embeddings = self.embedding_model.encode(texts).tolist()
        
        existing_count = self.collection.count()
        ids = [f"doc_{existing_count + i}" for i in range(len(documents))]
        
        metadatas = []
        for doc in documents:
            metadata = {
                'title': doc.get('title', 'Sin título'),
                'source': doc.get('source', 'Desconocido'),
                'category': doc.get('category', 'General')
            }
            metadatas.append(metadata)
        
        self.collection.add(
            embeddings=embeddings,
            documents=texts,
            metadatas=metadatas,
            ids=ids
        )
        
        print(f"✅ {len(documents)} documentos indexados")
    
    def search(self, query: str, n_results: int = 5, filters: Dict = None) -> List[Dict]:
        """Búsqueda semántica"""
        query_embedding = self.embedding_model.encode([query]).tolist()
        
        search_params = {
            'query_embeddings': query_embedding,
            'n_results': n_results
        }
        
        if filters:
            search_params['where'] = filters
        
        results = self.collection.query(**search_params)
        
        formatted_results = []
        for i in range(len(results['documents'][0])):
            formatted_results.append({
                'content': results['documents'][0][i],
                'metadata': results['metadatas'][0][i],
                'distance': results['distances'][0][i],
                'similarity': 1 - results['distances'][0][i]
            })
        
        return formatted_results
    
    def search_with_explanation(self, query: str, n_results: int = 3) -> Dict:
        """Búsqueda con explicación generada por LLM"""
        results = self.search(query, n_results)
        
        context = "\n\n".join([
            f"[Documento {i+1}]\nTítulo: {r['metadata']['title']}\nContenido: {r['content']}"
            for i, r in enumerate(results)
        ])
        
        prompt = f"""
        Basándote en los siguientes documentos, responde la pregunta del usuario.
        Menciona qué documentos usaste para tu respuesta.
        
        Documentos:
        {context}
        
        Pregunta: {query}
        
        Respuesta:
        """
        
        response = ollama.generate(
            model=self.llm_model,
            prompt=prompt,
            options={'temperature': 0.4}
        )
        
        return {
            'query': query,
            'answer': response['response'].strip(),
            'sources': results
        }
    
    def advanced_search(self, query: str, search_type: str = 'hybrid') -> List[Dict]:
        """Búsqueda avanzada con múltiples estrategias"""
        if search_type == 'semantic':
            return self.search(query)
        
        elif search_type == 'keyword':
            expanded_query = self._expand_query(query)
            return self.search(expanded_query)
        
        elif search_type == 'hybrid':
            semantic_results = self.search(query, n_results=10)
            
            reranked = self._rerank_results(query, semantic_results)
            
            return reranked[:5]
    
    def _expand_query(self, query: str) -> str:
        """Expande query con sinónimos y términos relacionados"""
        prompt = f"""
        Genera una versión expandida de la siguiente consulta,
        añadiendo sinónimos y términos relacionados.
        
        Consulta original: {query}
        
        Consulta expandida:
        """
        
        response = ollama.generate(
            model=self.llm_model,
            prompt=prompt,
            options={'temperature': 0.5}
        )
        
        return response['response'].strip()
    
    def _rerank_results(self, query: str, results: List[Dict]) -> List[Dict]:
        """Re-rankea resultados usando LLM"""
        for result in results:
            relevance_score = self._calculate_relevance(query, result['content'])
            result['relevance_score'] = relevance_score
        
        return sorted(results, key=lambda x: x['relevance_score'], reverse=True)
    
    def _calculate_relevance(self, query: str, document: str) -> float:
        """Calcula relevancia usando LLM"""
        prompt = f"""
        En una escala de 0 a 10, ¿qué tan relevante es el siguiente documento
        para responder la consulta?
        
        Consulta: {query}
        Documento: {document[:500]}
        
        Responde solo con un número del 0 al 10.
        """
        
        response = ollama.generate(
            model=self.llm_model,
            prompt=prompt,
            options={'temperature': 0.1}
        )
        
        try:
            score = float(response['response'].strip())
            return min(max(score, 0), 10) / 10
        except:
            return 0.5
    
    def get_statistics(self) -> Dict:
        """Obtiene estadísticas del índice"""
        total_docs = self.collection.count()
        
        return {
            'total_documents': total_docs,
            'collection_name': self.collection.name
        }

if __name__ == "__main__":
    search_engine = SemanticSearchEngine()
    
    documents = [
        {
            'title': 'Introducción a Python',
            'content': 'Python es un lenguaje de programación interpretado de alto nivel. Es conocido por su sintaxis clara y legible.',
            'source': 'Tutorial Python',
            'category': 'Programación'
        },
        {
            'title': 'Machine Learning Básico',
            'content': 'El aprendizaje automático es una rama de la IA que permite a las computadoras aprender de datos sin ser programadas explícitamente.',
            'source': 'Curso ML',
            'category': 'IA'
        },
        {
            'title': 'Estructuras de Datos',
            'content': 'Las listas, diccionarios y conjuntos son estructuras de datos fundamentales en Python para organizar información.',
            'source': 'Guía Python',
            'category': 'Programación'
        }
    ]
    
    search_engine.index_documents(documents)
    
    query = "¿Cómo organizar datos en Python?"
    
    print(f"\n🔍 Búsqueda: {query}\n")
    
    result = search_engine.search_with_explanation(query)
    
    print(f"💡 Respuesta:\n{result['answer']}\n")
    
    print("📚 Fuentes:")
    for i, source in enumerate(result['sources'], 1):
        print(f"  {i}. {source['metadata']['title']} (Similitud: {source['similarity']:.3f})")
```

---

## 🎓 5. Resumen ejecutivo

**Aplicaciones prácticas con Llama 3:**

**Proyectos implementados:**
1. **Chatbot con memoria:** Conversaciones contextuales persistentes
2. **Analizador de documentos:** Extracción de información y análisis
3. **Motor de búsqueda semántica:** Búsqueda inteligente con explicaciones

**Componentes clave:**
- Gestión de estado y persistencia
- Procesamiento de documentos
- Embeddings y búsqueda vectorial
- Integración con bases de datos
- APIs y servicios web

**Stack tecnológico:**
```
Ollama + ChromaDB + SQLite + FastAPI
```

---

## ✨ Conclusión

Llama 3 permite crear aplicaciones de IA sofisticadas y prácticas que resuelven problemas reales, desde chatbots inteligentes hasta sistemas de análisis de documentos, todo ejecutándose localmente con control total sobre datos y privacidad.

---

*Notas generadas para el curso "Working with Llama 3"*  
*Tema: Aplicaciones Prácticas y Proyectos del Mundo Real*
