```bash
# ⚖️ JurisMind – Assistente Jurídico com IA
```

```bash
![Python](https://img.shields.io/badge/python-3.12-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-0.115-green)
![IA](https://img.shields.io/badge/IA-OpenRouter-purple)
![Docker](https://img.shields.io/badge/Docker-ready-brightgreen)

Assistente jurídico inteligente que traduz perguntas em português para consultas SQL e retorna dados processuais reais. Desenvolvido para demonstrar habilidades em **engenharia de prompt**, **integração com LLMs gratuitas** e **arquitetura de software**.

## ✨ Funcionalidades

- 🧠 **Interpretação de linguagem natural**: transforma perguntas como *"Quais processos da 2ª Vara Fazenda têm assunto IPTU?"* em SQL válido.
- 🔄 **Fallback automático de modelos**: tenta 5 modelos gratuitos da OpenRouter até encontrar um disponível.
- 🛡️ **Execução segura**: apenas `SELECT` é permitido; SQL é validado antes de executar.
- 🎨 **Interface web profissional**: design escuro moderno com campo de busca, chips de exemplos e tabela responsiva.
- 🐳 **Pronto para deploy**: Dockerfile e Docker Compose incluídos.
- 📊 **Banco de dados populado**: 100 processos de exemplo para testes imediatos.

## 🧱 Arquitetura

```

[Interface Web] <-> [FastAPI] <-> [Motor de IA] <-> [OpenRouter]

```

1. O usuário digita uma pergunta em português.
2. A API envia um prompt estruturado para a LLM, instruindo-a a gerar apenas SQL.
3. O SQL gerado é executado com segurança no banco de processos.
4. Os resultados são exibidos na interface web.

## 🚀 Como executar rapidamente (Docker)

```bash
git clone https://github.com/dgdesiign/projeto3-jurismind.git
cd projeto3-jurismind
# Crie um arquivo .env com sua chave da OpenRouter (veja .env.example)
docker compose up --build
```

Acesse http://localhost:8002 e comece a perguntar.

💻 Execução manual (local ou Codespaces)

1. Clone o repositório

```bash
git clone https://github.com/dgdesiign/projeto3-jurismind.git
cd projeto3-jurismind
```

2. Configure as variáveis de ambiente

Crie um arquivo .env baseado no exemplo:

```bash
cp .env.example .env
# Edite .env e insira sua chave da OpenRouter
```

3. Instale as dependências

```bash
pip install -r requirements.txt
```

4. Popule o banco de dados (opcional, já incluso)

```bash
python seed.py
```

5. Inicie a API

```bash
uvicorn api.main:app --host 0.0.0.0 --port 8002 --reload
```

6. Acesse a interface

· Interface principal: http://localhost:8002
· Documentação Swagger: http://localhost:8002/docs

🧪 Exemplos de perguntas

Pergunta SQL esperado
Quais processos são da 2ª Vara Fazenda? SELECT * FROM processos WHERE vara LIKE '%2ª Vara Fazenda%'
Processos do juiz Ricardo Silva SELECT * FROM processos WHERE juiz LIKE '%Ricardo Silva%'
Quantos processos têm assunto IPTU? SELECT COUNT(*) FROM processos WHERE assunto LIKE '%IPTU%'
Liste os 5 processos mais recentes SELECT * FROM processos ORDER BY data_consulta DESC LIMIT 5

🔐 Configuração da OpenRouter

1. Acesse openrouter.ai e crie uma conta.
2. Vá em Keys e gere uma chave gratuita.
3. Copie a chave para o arquivo .env:
   ```
   OPENROUTER_API_KEY=sk-or-v1-sua-chave
   MODEL_NAME=openrouter/free
   ```

📁 Estrutura do projeto

```
projeto3-jurismind/
├── api/                  # FastAPI (endpoints)
│   └── main.py
├── core/                 # Motor de IA e prompts
│   └── engine.py
├── prompts/              # Templates de prompt
│   └── system.txt
├── static/               # Interface web
│   └── index.html
├── models.py             # Modelo do banco de dados
├── database.py           # Conexão SQLite
├── seed.py               # Popula o banco com dados de exemplo
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
└── .env.example
```

🛠️ Tecnologias

· Python 3.12, FastAPI, Uvicorn
· SQLAlchemy + SQLite
· OpenRouter API (modelos gratuitos como Llama, Gemma, Qwen)
· Docker & Docker Compose
· GitHub Codespaces (desenvolvimento em nuvem)

👨‍💻 Autor

Douglas – Candidato a Backend Júnior na Trimon
📧 douglasgoncalvesr.lima@gmail.com
📱 (71) 9 9172-2209
LinkedIn | GitHub

📝 Licença

MIT
EOF
