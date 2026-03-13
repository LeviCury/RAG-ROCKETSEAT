# Desafio RAG - "Os Sertões" de Euclides da Cunha

Implementação de três abordagens distintas de **Retrieval-Augmented Generation (RAG)** para responder perguntas sobre o livro *"Os Sertões"* de Euclides da Cunha.

## Abordagens

| Notebook | Abordagem | Descrição |
|---|---|---|
| `01_naive_rag.ipynb` | **Naive RAG** | Chunking fixo (1000 chars) + busca por similaridade top-k |
| `02_parent_rag.ipynb` | **Parent RAG** | Busca em child chunks (400 chars), retorna parent chunks (2000 chars) |
| `03_rerank_rag.ipynb` | **Rerank RAG** | Busca ampla (top-20) + re-ranking com cross-encoder FlashRank |

## Stack Tecnológica

- **Embeddings**: `sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2`
- **Vector Store**: ChromaDB
- **LLM**: OpenAI GPT-4o-mini
- **Re-ranker**: FlashRank (`ms-marco-MultiBERT-L-12`)
- **Framework**: LangChain

## Perguntas do Desafio

1. Qual é a visão de Euclides da Cunha sobre o ambiente natural do sertão nordestino e como ele influencia a vida dos habitantes?
2. Quais são as principais características da população sertaneja descritas por Euclides da Cunha? Como ele relaciona essas características com o ambiente em que vivem?
3. Qual foi o contexto histórico e político que levou à Guerra de Canudos, segundo Euclides da Cunha?
4. Como Euclides da Cunha descreve a figura de Antônio Conselheiro e seu papel na Guerra de Canudos?
5. Quais são os principais aspectos da crítica social e política presentes em "Os Sertões"? Como esses aspectos refletem a visão do autor sobre o Brasil da época?

## Como Executar

1. Clone o repositório:
   ```bash
   git clone https://github.com/LeviCury/desafio-rag.git
   cd desafio-rag
   ```

2. Instale as dependências:
   ```bash
   pip install -r requirements.txt
   ```

3. Baixe o PDF do livro:
   - [Os Sertões - PDF](https://fundar.org.br/wp-content/uploads/2021/06/os-sertoes.pdf)
   - Salve como `os-sertoes.pdf` na raiz do projeto

4. Configure a chave da OpenAI:
   ```bash
   cp .env.example .env
   # Edite .env e insira sua OPENAI_API_KEY
   ```

5. Execute os notebooks no Jupyter:
   ```bash
   jupyter notebook
   ```

## Comparação das Abordagens

| Aspecto | Naive RAG | Parent RAG | Rerank RAG |
|---|---|---|---|
| **Chunk de busca** | 1000 chars | 400 chars (child) | 1000 chars |
| **Chunk para LLM** | 1000 chars | 2000 chars (parent) | 1000 chars |
| **Retrieval** | Top-8 similaridade | Top-10 child → parent | Top-20 → re-rank top-6 |
| **Vantagem** | Simplicidade | Contexto mais amplo | Relevância mais precisa |
