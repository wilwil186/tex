# Notas Completas: RAG con Llama 3

## 📚 Curso: Working with Llama 3
**Tema:** Retrieval Augmented Generation (RAG)  
**Nivel:** Intermedio-Avanzado

---

## 🎯 1. ¿Qué es RAG?

### Definición:

**RAG (Retrieval Augmented Generation)** es una técnica que combina:
- **Recuperación de información** (Retrieval) de una base de conocimiento
- **Generación de texto** (Generation) usando un LLM

### El problema que resuelve:

Los LLMs tienen limitaciones:
- ❌ **Conocimiento limitado** al momento de entrenamiento
- ❌ **No tienen acceso** a información privada/específica
- ❌ **Pueden "alucinar"** información incorrecta
- ❌ **No pueden actualizar** su conocimiento fácilmente

### La solución RAG:

✅ **Proporciona contexto relevante** al LLM antes de generar  
✅ **Accede a información actualizada** de bases de datos  
✅ **Reduce alucinaciones** con datos verificables  
✅ **Permite conocimiento específico** de tu dominio  

### Analogía:

Imagina que estás en un examen:
- **Sin RAG:** Respondes solo con lo que memorizaste
- **Con RAG:** Puedes consultar libros y apuntes antes de responder

---

## 🔄 2. Arquitectura de RAG

### Flujo básico:

```
1. Usuario hace una pregunta
   ↓
2. Sistema busca información relevante en base de datos
   ↓
3. Recupera documentos/fragmentos más relevantes
   ↓
4. Combina pregunta + contexto recuperado
   ↓
5. LLM genera respuesta basada en el contexto
   ↓
6. Usuario recibe respuesta fundamentada
```

### Componentes principales:

```
┌─────────────────────────────────────────────┐
│           SISTEMA RAG                       │
├─────────────────────────────────────────────┤
│                                             │
│  ┌──────────────┐      ┌─────────────────┐ │
│  │  Documentos  │──────▶│  Embeddings     │ │
│  │  (Fuente)    │      │  (Vectores)     │ │
│  └──────────────┘      └─────────────────┘ │
│                              │              │
│                              ▼              │
│                        ┌─────────────────┐  │
│  ┌──────────────┐     │  Vector Store   │  │
│  │   Pregunta   │     │  (Base de datos)│  │
│  │   Usuario    │     └─────────────────┘  │
│  └──────────────┘              │            │
│         │                      │            │
│         ▼                      ▼            │
│  ┌─────────────────────────────────────┐   │
│  │    Búsqueda de Similitud            │   │
│  │    (Recuperación)                   │   │
│  └─────────────────────────────────────┘   │
│                   │                         │
│                   ▼                         │
│  ┌─────────────────────────────────────┐   │
│  │  Contexto + Pregunta → LLM          │   │
│  │  (Generación)                       │   │
│  └─────────────────────────────────────┘   │
│                   │                         │
│                   ▼                         │
│            ┌──────────────┐                 │
│            │   Respuesta  │                 │
│            └──────────────┘                 │
└─────────────────────────────────────────────┘
```

---

## 🧮 3. Embeddings - La base de RAG

### ¿Qué son los embeddings?

**Embeddings** son representaciones numéricas (vectores) de texto que capturan su significado semántico.

### Ejemplo visual:

```
Texto: "El gato duerme"
Embedding: [0.23, -0.45, 0.67, 0.12, ..., 0.89]
           (vector de 384 o más dimensiones)

Texto similar: "El felino descansa"
Embedding: [0.25, -0.43, 0.65, 0.15, ..., 0.87]
           (vector cercano en el espacio)
```

### Propiedad clave:

**Textos con significados similares tienen embeddings cercanos en el espacio vectorial.**

### Modelos de embeddings populares:

| Modelo | Dimensiones | Tamaño | Uso |
|--------|-------------|--------|-----|
| **sentence-transformers/all-MiniLM-L6-v2** | 384 | 80 MB | General, rápido |
| **sentence-transformers/all-mpnet-base-v2** | 768 | 420 MB | Alta calidad |
| **text-embedding-ada-002** (OpenAI) | 1536 | API | Muy preciso |
| **BAAI/bge-small-en-v1.5** | 384 | 133 MB | Eficiente |

---

## 🛠️ 4. Implementación básica de RAG

### 4.1 Instalación de dependencias:

```bash
pip install ollama
pip install sentence-transformers
pip install chromadb
pip install langchain
pip install langchain-community
```

### 4.2 Código completo - RAG simple:

```python
import ollama
from sentence_transformers import SentenceTransformer
import chromadb
from chromadb.config import Settings

class SimpleRAG:
    def __init__(self, model_name='llama3'):
        self.llm_model = model_name
        self.embedding_model = SentenceTransformer('all-MiniLM-L6-v2')
        
        self.client = chromadb.Client(Settings(
            anonymized_telemetry=False
        ))
        
        self.collection = self.client.create_collection(
            name="documents",
            metadata={"hnsw:space": "cosine"}
        )
        
        print("✅ RAG System inicializado")
    
    def add_documents(self, documents):
        """Añade documentos a la base de conocimiento"""
        print(f"Añadiendo {len(documents)} documentos...")
        
        embeddings = self.embedding_model.encode(documents).tolist()
        
        ids = [f"doc_{i}" for i in range(len(documents))]
        
        self.collection.add(
            embeddings=embeddings,
            documents=documents,
            ids=ids
        )
        
        print(f"✅ {len(documents)} documentos añadidos")
    
    def retrieve(self, query, n_results=3):
        """Recupera documentos relevantes"""
        query_embedding = self.embedding_model.encode([query]).tolist()
        
        results = self.collection.query(
            query_embeddings=query_embedding,
            n_results=n_results
        )
        
        return results['documents'][0]
    
    def generate(self, query, context):
        """Genera respuesta usando LLM"""
        prompt = f"""
Usa el siguiente contexto para responder la pregunta.
Si no puedes responder con el contexto dado, di que no tienes suficiente información.

Contexto:
{context}

Pregunta: {query}

Respuesta:
"""
        
        response = ollama.generate(
            model=self.llm_model,
            prompt=prompt,
            options={
                'temperature': 0.3,
                'num_predict': 200
            }
        )
        
        return response['response']
    
    def query(self, question, n_results=3):
        """Pipeline completo RAG"""
        print(f"\n🔍 Pregunta: {question}")
        
        relevant_docs = self.retrieve(question, n_results)
        
        print(f"📚 Documentos recuperados: {len(relevant_docs)}")
        for i, doc in enumerate(relevant_docs, 1):
            print(f"  {i}. {doc[:100]}...")
        
        context = "\n\n".join(relevant_docs)
        
        print("\n🤖 Generando respuesta...")
        answer = self.generate(question, context)
        
        return answer

if __name__ == "__main__":
    rag = SimpleRAG()
    
    documents = [
        "Python es un lenguaje de programación de alto nivel, interpretado y de propósito general.",
        "Python fue creado por Guido van Rossum y lanzado por primera vez en 1991.",
        "Python usa indentación para definir bloques de código en lugar de llaves.",
        "Las listas en Python son estructuras de datos mutables que pueden contener elementos de diferentes tipos.",
        "Los diccionarios en Python son colecciones no ordenadas de pares clave-valor.",
        "NumPy es una biblioteca de Python para computación científica que proporciona arrays multidimensionales.",
        "Pandas es una biblioteca de Python para análisis y manipulación de datos.",
        "Django es un framework web de alto nivel escrito en Python.",
        "Flask es un microframework web minimalista para Python.",
        "Machine learning en Python se facilita con bibliotecas como scikit-learn y TensorFlow."
    ]
    
    rag.add_documents(documents)
    
    questions = [
        "¿Quién creó Python?",
        "¿Qué es NumPy?",
        "¿Cómo define Python los bloques de código?"
    ]
    
    for question in questions:
        answer = rag.query(question)
        print(f"\n💡 Respuesta: {answer}")
        print("="*60)
```

---

## 📊 5. RAG con ChromaDB (Avanzado)

### 5.1 ¿Qué es ChromaDB?

**ChromaDB** es una base de datos vectorial diseñada específicamente para embeddings y RAG.

**Características:**
- ✅ Almacenamiento persistente
- ✅ Búsqueda de similitud eficiente
- ✅ Filtrado por metadatos
- ✅ Fácil integración con Python

### 5.2 Implementación con persistencia:

```python
import ollama
from sentence_transformers import SentenceTransformer
import chromadb
from chromadb.config import Settings
import os

class PersistentRAG:
    def __init__(self, persist_directory="./chroma_db", model_name='llama3'):
        self.llm_model = model_name
        self.embedding_model = SentenceTransformer('all-MiniLM-L6-v2')
        
        os.makedirs(persist_directory, exist_ok=True)
        
        self.client = chromadb.PersistentClient(path=persist_directory)
        
        try:
            self.collection = self.client.get_collection("documents")
            print("✅ Colección existente cargada")
        except:
            self.collection = self.client.create_collection(
                name="documents",
                metadata={"hnsw:space": "cosine"}
            )
            print("✅ Nueva colección creada")
    
    def add_documents(self, documents, metadatas=None):
        """Añade documentos con metadatos opcionales"""
        embeddings = self.embedding_model.encode(documents).tolist()
        
        existing_count = self.collection.count()
        ids = [f"doc_{existing_count + i}" for i in range(len(documents))]
        
        if metadatas is None:
            metadatas = [{"source": "manual"} for _ in documents]
        
        self.collection.add(
            embeddings=embeddings,
            documents=documents,
            metadatas=metadatas,
            ids=ids
        )
        
        print(f"✅ {len(documents)} documentos añadidos (Total: {self.collection.count()})")
    
    def retrieve_with_metadata(self, query, n_results=3, filter_dict=None):
        """Recupera documentos con filtrado por metadatos"""
        query_embedding = self.embedding_model.encode([query]).tolist()
        
        query_params = {
            'query_embeddings': query_embedding,
            'n_results': n_results
        }
        
        if filter_dict:
            query_params['where'] = filter_dict
        
        results = self.collection.query(**query_params)
        
        return {
            'documents': results['documents'][0],
            'metadatas': results['metadatas'][0],
            'distances': results['distances'][0]
        }
    
    def query_with_sources(self, question, n_results=3):
        """Query con información de fuentes"""
        print(f"\n🔍 Pregunta: {question}")
        
        results = self.retrieve_with_metadata(question, n_results)
        
        print(f"\n📚 Documentos recuperados:")
        for i, (doc, meta, dist) in enumerate(zip(
            results['documents'],
            results['metadatas'],
            results['distances']
        ), 1):
            print(f"  {i}. [Similitud: {1-dist:.3f}] {doc[:80]}...")
            print(f"     Fuente: {meta.get('source', 'N/A')}")
        
        context = "\n\n".join([
            f"[Fuente: {meta.get('source', 'N/A')}]\n{doc}"
            for doc, meta in zip(results['documents'], results['metadatas'])
        ])
        
        prompt = f"""
Usa el siguiente contexto para responder la pregunta.
Menciona las fuentes cuando sea relevante.

Contexto:
{context}

Pregunta: {question}

Respuesta:
"""
        
        response = ollama.generate(
            model=self.llm_model,
            prompt=prompt,
            options={'temperature': 0.3}
        )
        
        return response['response']
    
    def get_stats(self):
        """Obtiene estadísticas de la base de datos"""
        count = self.collection.count()
        return {
            'total_documents': count,
            'collection_name': self.collection.name
        }

if __name__ == "__main__":
    rag = PersistentRAG()
    
    documents = [
        "La fotosíntesis es el proceso por el cual las plantas convierten luz solar en energía química.",
        "El ADN contiene las instrucciones genéticas para el desarrollo y funcionamiento de los organismos.",
        "La mitosis es el proceso de división celular que resulta en dos células hijas idénticas.",
        "Los ecosistemas son comunidades de organismos que interactúan con su entorno físico.",
        "La evolución es el cambio en las características heredables de poblaciones a lo largo del tiempo."
    ]
    
    metadatas = [
        {"source": "Biología - Capítulo 3", "topic": "fotosíntesis"},
        {"source": "Genética - Capítulo 1", "topic": "ADN"},
        {"source": "Biología Celular - Capítulo 5", "topic": "división celular"},
        {"source": "Ecología - Capítulo 2", "topic": "ecosistemas"},
        {"source": "Evolución - Capítulo 1", "topic": "evolución"}
    ]
    
    rag.add_documents(documents, metadatas)
    
    stats = rag.get_stats()
    print(f"\n📊 Estadísticas: {stats}")
    
    answer = rag.query_with_sources("¿Qué es la fotosíntesis?")
    print(f"\n💡 Respuesta:\n{answer}")
```

---

## 🔗 6. RAG con LangChain

### 6.1 ¿Por qué LangChain?

**LangChain** es un framework que simplifica la construcción de aplicaciones con LLMs.

**Ventajas:**
- ✅ Abstracciones de alto nivel
- ✅ Componentes reutilizables
- ✅ Integración con múltiples LLMs y vectorstores
- ✅ Cadenas (chains) predefinidas para RAG

### 6.2 Implementación con LangChain:

```python
from langchain_community.llms import Ollama
from langchain_community.embeddings import HuggingFaceEmbeddings
from langchain_community.vectorstores import Chroma
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain.chains import RetrievalQA
from langchain.prompts import PromptTemplate

class LangChainRAG:
    def __init__(self, model_name='llama3', persist_directory="./langchain_db"):
        print("Inicializando LangChain RAG...")
        
        self.llm = Ollama(
            model=model_name,
            temperature=0.3
        )
        
        self.embeddings = HuggingFaceEmbeddings(
            model_name='sentence-transformers/all-MiniLM-L6-v2'
        )
        
        self.persist_directory = persist_directory
        self.vectorstore = None
        self.qa_chain = None
        
        print("✅ LangChain RAG inicializado")
    
    def load_documents(self, texts):
        """Carga y procesa documentos"""
        text_splitter = RecursiveCharacterTextSplitter(
            chunk_size=500,
            chunk_overlap=50,
            length_function=len
        )
        
        chunks = []
        for text in texts:
            chunks.extend(text_splitter.split_text(text))
        
        print(f"📄 {len(texts)} documentos divididos en {len(chunks)} chunks")
        
        self.vectorstore = Chroma.from_texts(
            texts=chunks,
            embedding=self.embeddings,
            persist_directory=self.persist_directory
        )
        
        self._create_qa_chain()
        
        print("✅ Documentos cargados en vectorstore")
    
    def _create_qa_chain(self):
        """Crea la cadena de QA"""
        template = """
Usa el siguiente contexto para responder la pregunta.
Si no sabes la respuesta, di que no tienes suficiente información.
No inventes información.

Contexto: {context}

Pregunta: {question}

Respuesta útil:
"""
        
        prompt = PromptTemplate(
            template=template,
            input_variables=["context", "question"]
        )
        
        self.qa_chain = RetrievalQA.from_chain_type(
            llm=self.llm,
            chain_type="stuff",
            retriever=self.vectorstore.as_retriever(
                search_kwargs={"k": 3}
            ),
            chain_type_kwargs={"prompt": prompt},
            return_source_documents=True
        )
    
    def query(self, question):
        """Realiza una consulta"""
        if self.qa_chain is None:
            return "Error: No hay documentos cargados"
        
        print(f"\n🔍 Pregunta: {question}")
        
        result = self.qa_chain.invoke({"query": question})
        
        answer = result['result']
        sources = result['source_documents']
        
        print(f"\n📚 Fuentes consultadas: {len(sources)}")
        for i, doc in enumerate(sources, 1):
            print(f"  {i}. {doc.page_content[:100]}...")
        
        return answer

if __name__ == "__main__":
    rag = LangChainRAG()
    
    documents = [
        """
        Python es un lenguaje de programación interpretado de alto nivel.
        Fue creado por Guido van Rossum y lanzado en 1991.
        Python enfatiza la legibilidad del código y usa indentación significativa.
        Es ampliamente usado en desarrollo web, ciencia de datos, IA y automatización.
        """,
        """
        NumPy es la biblioteca fundamental para computación científica en Python.
        Proporciona soporte para arrays multidimensionales y matrices.
        Incluye funciones matemáticas de alto nivel para operar con estos arrays.
        NumPy es la base de muchas otras bibliotecas científicas de Python.
        """,
        """
        Pandas es una biblioteca de Python para análisis y manipulación de datos.
        Proporciona estructuras de datos como DataFrame y Series.
        Facilita la limpieza, transformación y análisis de datos tabulares.
        Es esencial para ciencia de datos y análisis de datos en Python.
        """
    ]
    
    rag.load_documents(documents)
    
    questions = [
        "¿Quién creó Python y cuándo?",
        "¿Para qué se usa NumPy?",
        "¿Qué estructuras de datos proporciona Pandas?"
    ]
    
    for question in questions:
        answer = rag.query(question)
        print(f"\n💡 Respuesta: {answer}")
        print("="*60)
```

---

## 📄 7. RAG con documentos PDF

### 7.1 Instalación adicional:

```bash
pip install pypdf
pip install langchain-community
```

### 7.2 Procesamiento de PDFs:

```python
from langchain_community.document_loaders import PyPDFLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain_community.embeddings import HuggingFaceEmbeddings
from langchain_community.vectorstores import Chroma
from langchain_community.llms import Ollama
from langchain.chains import RetrievalQA
import os

class PDFRAG:
    def __init__(self, model_name='llama3'):
        self.llm = Ollama(model=model_name, temperature=0.3)
        self.embeddings = HuggingFaceEmbeddings(
            model_name='sentence-transformers/all-MiniLM-L6-v2'
        )
        self.vectorstore = None
        self.qa_chain = None
    
    def load_pdf(self, pdf_path):
        """Carga y procesa un PDF"""
        print(f"📄 Cargando PDF: {pdf_path}")
        
        if not os.path.exists(pdf_path):
            raise FileNotFoundError(f"PDF no encontrado: {pdf_path}")
        
        loader = PyPDFLoader(pdf_path)
        pages = loader.load()
        
        print(f"✅ {len(pages)} páginas cargadas")
        
        text_splitter = RecursiveCharacterTextSplitter(
            chunk_size=1000,
            chunk_overlap=200,
            length_function=len
        )
        
        chunks = text_splitter.split_documents(pages)
        print(f"📝 Dividido en {len(chunks)} chunks")
        
        self.vectorstore = Chroma.from_documents(
            documents=chunks,
            embedding=self.embeddings,
            persist_directory="./pdf_db"
        )
        
        self.qa_chain = RetrievalQA.from_chain_type(
            llm=self.llm,
            chain_type="stuff",
            retriever=self.vectorstore.as_retriever(search_kwargs={"k": 4}),
            return_source_documents=True
        )
        
        print("✅ PDF procesado y listo para consultas")
    
    def load_multiple_pdfs(self, pdf_directory):
        """Carga múltiples PDFs de un directorio"""
        pdf_files = [f for f in os.listdir(pdf_directory) if f.endswith('.pdf')]
        
        print(f"📚 Encontrados {len(pdf_files)} PDFs")
        
        all_chunks = []
        
        for pdf_file in pdf_files:
            pdf_path = os.path.join(pdf_directory, pdf_file)
            print(f"  Procesando: {pdf_file}")
            
            loader = PyPDFLoader(pdf_path)
            pages = loader.load()
            
            text_splitter = RecursiveCharacterTextSplitter(
                chunk_size=1000,
                chunk_overlap=200
            )
            
            chunks = text_splitter.split_documents(pages)
            all_chunks.extend(chunks)
        
        print(f"✅ Total de chunks: {len(all_chunks)}")
        
        self.vectorstore = Chroma.from_documents(
            documents=all_chunks,
            embedding=self.embeddings,
            persist_directory="./multi_pdf_db"
        )
        
        self.qa_chain = RetrievalQA.from_chain_type(
            llm=self.llm,
            chain_type="stuff",
            retriever=self.vectorstore.as_retriever(search_kwargs={"k": 5}),
            return_source_documents=True
        )
        
        print("✅ Todos los PDFs procesados")
    
    def query(self, question):
        """Consulta el sistema RAG"""
        if self.qa_chain is None:
            return "Error: No hay documentos cargados"
        
        print(f"\n🔍 Pregunta: {question}")
        
        result = self.qa_chain.invoke({"query": question})
        
        answer = result['result']
        sources = result['source_documents']
        
        print(f"\n📚 Fuentes:")
        for i, doc in enumerate(sources, 1):
            page = doc.metadata.get('page', 'N/A')
            source = doc.metadata.get('source', 'N/A')
            print(f"  {i}. Página {page} de {os.path.basename(source)}")
            print(f"     {doc.page_content[:150]}...")
        
        return answer

if __name__ == "__main__":
    rag = PDFRAG()
    
    rag.load_pdf("documento.pdf")
    
    answer = rag.query("¿Cuál es el tema principal del documento?")
    print(f"\n💡 Respuesta:\n{answer}")
```

---

## 🎯 8. Mejores prácticas para RAG

### 8.1 Chunking (División de documentos):

**Estrategias:**

1. **Fixed-size chunking:**
```python
chunk_size = 500
chunk_overlap = 50
```

2. **Semantic chunking:**
```python
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=1000,
    chunk_overlap=200,
    separators=["\n\n", "\n", ". ", " ", ""]
)
```

3. **Document-aware chunking:**
```python
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=1000,
    chunk_overlap=200,
    length_function=len,
    is_separator_regex=False
)
```

### 8.2 Optimización de retrieval:

```python
retriever = vectorstore.as_retriever(
    search_type="mmr",
    search_kwargs={
        "k": 5,
        "fetch_k": 20,
        "lambda_mult": 0.5
    }
)
```

**Parámetros:**
- `k`: Número de documentos a devolver
- `fetch_k`: Número de documentos a recuperar antes de filtrar
- `lambda_mult`: Balance entre relevancia y diversidad (0-1)

### 8.3 Prompt engineering para RAG:

```python
template = """
Eres un asistente experto que responde preguntas basándose en el contexto proporcionado.

REGLAS:
1. Usa SOLO la información del contexto para responder
2. Si el contexto no contiene la respuesta, di "No tengo suficiente información"
3. Cita las fuentes cuando sea posible
4. Sé conciso pero completo
5. No inventes información

Contexto:
{context}

Pregunta: {question}

Respuesta detallada:
"""
```

### 8.4 Evaluación de RAG:

```python
def evaluate_rag(rag_system, test_questions, expected_answers):
    """Evalúa el sistema RAG"""
    results = []
    
    for question, expected in zip(test_questions, expected_answers):
        answer = rag_system.query(question)
        
        similarity = calculate_similarity(answer, expected)
        
        results.append({
            'question': question,
            'answer': answer,
            'expected': expected,
            'similarity': similarity
        })
    
    avg_similarity = sum(r['similarity'] for r in results) / len(results)
    
    return {
        'results': results,
        'average_similarity': avg_similarity
    }
```

---

## 🚀 9. RAG avanzado - Técnicas adicionales

### 9.1 Re-ranking:

```python
from sentence_transformers import CrossEncoder

class ReRankingRAG:
    def __init__(self):
        self.retriever = ...
        self.reranker = CrossEncoder('cross-encoder/ms-marco-MiniLM-L-6-v2')
    
    def retrieve_and_rerank(self, query, k=10, top_n=3):
        initial_docs = self.retriever.get_relevant_documents(query, k=k)
        
        pairs = [[query, doc.page_content] for doc in initial_docs]
        scores = self.reranker.predict(pairs)
        
        ranked_docs = sorted(
            zip(initial_docs, scores),
            key=lambda x: x[1],
            reverse=True
        )
        
        return [doc for doc, score in ranked_docs[:top_n]]
```

### 9.2 Hybrid Search (Keyword + Semantic):

```python
from langchain.retrievers import BM25Retriever, EnsembleRetriever

class HybridRAG:
    def __init__(self, documents):
        self.bm25_retriever = BM25Retriever.from_documents(documents)
        self.bm25_retriever.k = 5
        
        vectorstore = Chroma.from_documents(documents, embeddings)
        self.semantic_retriever = vectorstore.as_retriever(search_kwargs={"k": 5})
        
        self.ensemble_retriever = EnsembleRetriever(
            retrievers=[self.bm25_retriever, self.semantic_retriever],
            weights=[0.5, 0.5]
        )
    
    def retrieve(self, query):
        return self.ensemble_retriever.get_relevant_documents(query)
```

### 9.3 Query Expansion:

```python
def expand_query(original_query, llm):
    """Expande la query para mejor retrieval"""
    prompt = f"""
    Genera 3 variaciones de la siguiente pregunta que mantengan el mismo significado:
    
    Pregunta original: {original_query}
    
    Variaciones:
    1.
    2.
    3.
    """
    
    response = llm.generate(prompt)
    variations = parse_variations(response)
    
    return [original_query] + variations
```

---

## 📊 10. Monitoreo y debugging de RAG

### 10.1 Logging detallado:

```python
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

class DebugRAG:
    def query(self, question):
        logger.info(f"Query recibida: {question}")
        
        retrieved_docs = self.retrieve(question)
        logger.info(f"Documentos recuperados: {len(retrieved_docs)}")
        
        for i, doc in enumerate(retrieved_docs):
            logger.debug(f"Doc {i}: {doc[:100]}...")
        
        answer = self.generate(question, retrieved_docs)
        logger.info(f"Respuesta generada: {len(answer)} caracteres")
        
        return answer
```

### 10.2 Métricas de rendimiento:

```python
import time

class MetricsRAG:
    def __init__(self):
        self.metrics = {
            'retrieval_times': [],
            'generation_times': [],
            'total_queries': 0
        }
    
    def query_with_metrics(self, question):
        start_total = time.time()
        
        start_retrieval = time.time()
        docs = self.retrieve(question)
        retrieval_time = time.time() - start_retrieval
        
        start_generation = time.time()
        answer = self.generate(question, docs)
        generation_time = time.time() - start_generation
        
        total_time = time.time() - start_total
        
        self.metrics['retrieval_times'].append(retrieval_time)
        self.metrics['generation_times'].append(generation_time)
        self.metrics['total_queries'] += 1
        
        return answer, {
            'retrieval_time': retrieval_time,
            'generation_time': generation_time,
            'total_time': total_time
        }
    
    def get_average_metrics(self):
        return {
            'avg_retrieval_time': sum(self.metrics['retrieval_times']) / len(self.metrics['retrieval_times']),
            'avg_generation_time': sum(self.metrics['generation_times']) / len(self.metrics['generation_times']),
            'total_queries': self.metrics['total_queries']
        }
```

---

## 🎓 11. Resumen ejecutivo

**RAG (Retrieval Augmented Generation)** combina búsqueda de información con generación de texto para:

✅ **Proporcionar respuestas fundamentadas** en datos reales  
✅ **Reducir alucinaciones** del LLM  
✅ **Acceder a información actualizada** y específica  
✅ **Mantener privacidad** procesando datos localmente  

**Componentes clave:**
1. **Embeddings:** Representaciones vectoriales de texto
2. **Vector Store:** Base de datos para búsqueda de similitud
3. **Retriever:** Sistema de recuperación de documentos relevantes
4. **LLM:** Generador de respuestas basadas en contexto

**Stack tecnológico recomendado:**
```python
ollama
sentence-transformers
chromadb
langchain
```

**Pipeline básico:**
```
Pregunta → Embedding → Búsqueda → Contexto → LLM → Respuesta
```

---

## ✨ Conclusión

RAG transforma los LLMs de generadores de texto a sistemas de conocimiento fundamentados en datos reales. Al combinar Llama 3 con RAG, puedes crear asistentes inteligentes que responden con precisión basándose en tu propia base de conocimiento, manteniendo privacidad y control total sobre los datos.

---

*Notas generadas para el curso "Working with Llama 3"*  
*Tema: Retrieval Augmented Generation (RAG)*
