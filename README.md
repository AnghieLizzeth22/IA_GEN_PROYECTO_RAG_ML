🤖 ML Expert RAG System

Integrantes:
- Anghie Chilon 
- Carlos Mendoza

Pipeline de Generación Aumentada por Recuperación (RAG) para Consultas de Machine Learning.

Este proyecto implementa un sistema RAG avanzado capaz de responder preguntas técnicas sobre Machine Learning utilizando una arquitectura de filtrado progresivo, garantizando respuestas precisas y citadas.

🎯 Objetivo

Facilitar el acceso a información técnica de Machine Learning de manera rápida y confiable, optimizando el tiempo de búsqueda manual en múltiples fuentes académicas y libros especializados.

🏗 Arquitectura del Sistema: Progressive Context Filtering

El sistema no solo busca información, sino que la refina en capas para entregar solo lo más relevante al LLM:

Hybrid Retrieval (BM25 + FAISS HNSW): Combina búsqueda semántica vectorial con búsqueda por palabras clave.

Reranker (Cross-Encoder): Re-evalúa la relevancia de los documentos recuperados.

Context Compression: Extrae solo las oraciones clave para reducir el ruido y ahorrar tokens.

Generación (TinyLlama / Llama 2): Genera la respuesta en español basada estrictamente en el contexto.

Validación de Grounding: Cálculo de puntuación de confianza para evitar alucinaciones.

🚀 Guía de Ejecución

Opción A: Ejecución Automática (GitHub Actions)
Este repositorio está configurado con CI/CD para validar el código automáticamente en cada cambio.

Ve a la pestaña Actions en este repositorio.

Selecciona el flujo "Run RAG Notebook".

Al finalizar, descarga el archivo en la sección Artifacts para ver los resultados de las pruebas.

Nota: Requiere configurar el secreto HF_TOKEN en los Settings del repositorio.

Opción B: Uso Interactivo (Google Colab)
Para chatear con el bot en tiempo real:

Abre el notebook usando el botón "Open in Colab" arriba.

En el menú, ve a Entorno de ejecución > Cambiar tipo de entorno y selecciona T4 GPU (para usar Llama 2 7B con 4-bit).

Ejecuta todas las celdas (Ctrl + F9).

Al final, aparecerá una interfaz de Gradio con un link público para interactuar con el bot.

⚙️ Decisiones Técnicas
Vector DB: FAISS con HNSW para búsquedas de milisegundos.

Embeddings: all-MiniLM-L6-v2 (Balance ideal velocidad/calidad).

LLM de Producción: Llama 2 7B (Vía Hugging Face con cuantización 4-bit).

LLM de Testing: TinyLlama 1.1B (Para ejecución ligera en CPU de GitHub Actions).

Métricas de Calidad: Implementación de ROUGE-L, BLEU y Grounding Score personalizado.

📂 Estructura del Proyecto
Bash
├── .github/workflows/  # Configuración de ejecución automática
├── docs/               # Corpus de conocimiento (PDFs y Libros)
├── notebooks/          # Proyecto_RAG.ipynb (Core del proyecto)
├── requirements.txt    # Dependencias del sistema
└── README.md           # Documentación