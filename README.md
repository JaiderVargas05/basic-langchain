# 🧠 Proyecto: LangChain Básico con OpenAI

## 🎯 Objetivo
Este proyecto implementa un **LLM Chain simple** utilizando el framework **LangChain** y el modelo **GPT-4o-mini** de OpenAI.  
El propósito es comprender la construcción básica de un flujo *Prompt → LLM → Respuesta*, como base conceptual antes de desarrollar sistemas más avanzados como los RAG (Retrieval-Augmented Generation).

---

## 🧱 Arquitectura del proyecto

El flujo de ejecución en el notebook es el siguiente:

1. **Configuración del entorno**  
   - Se solicita al usuario la clave de OpenAI (`OPENAI_API_KEY`) con `getpass` o se carga automáticamente desde las variables de entorno.
2. **Inicialización del modelo y embeddings**  
   - Se crea un objeto `ChatOpenAI` para el modelo `gpt-4o-mini`.  
   - Se prueban los embeddings con `OpenAIEmbeddings`.
3. **Definición de un PromptTemplate**  
   - Se usa `ChatPromptTemplate` para definir la estructura del mensaje (system y human).
4. **Creación del Chain**  
   - Se combina el prompt con el modelo (`prompt | llm`).
5. **Invocación**  
   - El usuario ingresa una pregunta y el modelo genera una respuesta.

---

## 📂 Estructura del repositorio
```
basic-langchain/
├── lang-chain.ipynb       # Notebook principal con la implementación
├── .gitignore             # Archivos ignorados (entornos, claves, etc.)
└── README.md              # Este archivo
```

---

## ⚙️ Requisitos

### Python
Se recomienda usar **Python 3.11** o superior (evitar 3.14 por problemas de compatibilidad con numpy).

### Dependencias
Instálalas con:
```bash
pip install langchain langchain-openai python-dotenv tiktoken
```

### Variables de entorno
Crea un archivo `.env` en la raíz del proyecto:
```
OPENAI_API_KEY=sk-xxxxxx
```

O bien, puedes ingresar tu clave al ejecutar el notebook cuando te la pida:
```python
import getpass, os
os.environ["OPENAI_API_KEY"] = getpass.getpass("Enter your OpenAI API key: ")
```

---

## ▶️ Ejecución

Abre el notebook:
```bash
jupyter notebook lang-chain.ipynb
```

Y ejecuta las celdas paso a paso.  
Al final podrás invocar el modelo con un texto, por ejemplo:

```python
from langchain_openai import ChatOpenAI
from langchain.prompts import ChatPromptTemplate

llm = ChatOpenAI(model="gpt-4o-mini", temperature=0.2)
prompt = ChatPromptTemplate.from_messages([
    ("system", "Eres un asistente amable y preciso."),
    ("human", "Explica qué es un modelo de lenguaje en 3 líneas.")
])
chain = prompt | llm
response = chain.invoke({"input": ""})
print(response.content)
```

**Salida esperada:**
```
Un modelo de lenguaje predice texto a partir de contexto previo.
Aprende patrones y relaciones entre palabras mediante entrenamiento masivo.
Se usa para tareas como generación, traducción o chatbots.
```

---

## 📚 Referencias
- [LangChain LLM Chain Tutorial](https://python.langchain.com/docs/tutorials/llm_chain/)
- [OpenAI API Docs](https://platform.openai.com/docs/)
- [LangChain Chat Models](https://python.langchain.com/docs/integrations/chat/openai/)
