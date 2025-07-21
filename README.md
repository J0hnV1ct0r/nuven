# Desafio Técnico - Dev IA

Este projeto resolve o desafio de extração, indexação e busca inteligente de informações em documentos PDF e imagens de tabelas, utilizando técnicas de NLP e IA generativa.

## Funcionalidades

- **Extração de texto de PDF**: Utiliza `pdfplumber` para extrair e limpar o texto.
- **Extração de tabelas de imagens**: Usa OCR (`pytesseract` + `PIL`) para identificar e estruturar tabelas presentes em imagens.
- **Organização dos dados**: Une as seções do texto e as linhas da tabela em uma estrutura única.
- **Indexação semântica**: Aplica `SentenceTransformer` para gerar embeddings dos textos e indexa com `faiss` para busca eficiente.
- **Busca e geração de respostas**: Utiliza o modelo Gemini da Google para responder perguntas com base no contexto extraído.

## Arquitetura do pipeline

```mermaid
flowchart TD
    A[PDF e Imagem de Tabela] --> B[Extração de Texto e Tabela]
    B --> C[Limpeza e Organização dos Dados]
    C --> D[Indexação Semântica (embeddings + faiss)]
    D --> E[Busca Inteligente]
    E --> F[Geração de Respostas com Gemini]
```

## Como usar

1. **Pré-requisitos**  
   Instale as dependências:
   ```bash
   pip install pdfplumber pillow pytesseract sentence-transformers faiss-cpu google-generativeai
   ```

2. **Configuração da chave da API Gemini**  
   Obtenha uma chave em https://ai.google.dev/gemini-api/docs/oauth e configure no código:
   ```python
   import google.generativeai as genai
   genai.configure(api_key="SUA_CHAVE_AQUI")
   ```

3. **Executando o pipeline**  
   No Jupyter Notebook `desafio.ipynb`, ajuste os caminhos dos arquivos PDF e imagem:
   ```python
   pdf_path = "textos/codigo_de_obras.pdf"
   img_path = "textos/tabela.webp"
   dados_unidos = extracao_conteudo(pdf_path, img_path)
   chunks, index, model = indexar(dados_unidos)
   question_answering(chunks, index, model)
   ```

4. **Faça perguntas**  
   Digite sua pergunta quando solicitado e receba respostas baseadas no conteúdo dos documentos.

## Exemplo de entrada e saída

**Pergunta de entrada:**
```
Digite sua pergunta: Quais são as exigências para aprovação de projetos de construção?
```

**Saída gerada pelo modelo:**
```
pergunta: Quais são as exigências para aprovação de projetos de construção?
resposta do modelo:
Baseado nos trechos fornecidos, as exigências para que a construção (e, por extensão, o projeto que a fundamenta) possa ser iniciada são:

1.  **Concessão da licença para construção** (Art. 31).

Além disso, para a licença específica de implantação de **canteiro de obras fora dos limites do lote**, são exigidos (Art. 32):
*   Exame das condições locais de circulação criadas no horário de trabalho.
*   Avaliação dos inconvenientes ou prejuízos que venham causar ao trânsito de veículos e pedestres, bem como aos imóveis vizinhos.
*   Garantia de que, após o término da obra, seja restituída a cobertura vegetal preexistente à instalação do canteiro.
```

## Estrutura dos arquivos

- `desafio.ipynb`: Notebook principal com todo o pipeline.
- `textos/codigo_de_obras.pdf`: Documento PDF de referência.
- `textos/tabela.webp`: Imagem da tabela para extração via OCR.

## Observações

- O projeto pode ser adaptado para outros documentos e tabelas.
- Certifique-se de que o Tesseract está instalado no sistema para OCR funcionar.

## Autor
João Victor de Souza Albuquerque

Desenvolvido para o Desafio Técnico Dev IA.