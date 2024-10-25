# Enterprise LLM Routing System

<div align="center">
  <img src="https://github.com/samuelfernandof/enterprise-llm-routing-system/blob/main/llm-router/src/Captura%20de%20tela%202024-10-25%20112950.png" width="300" alt="Logo do projeto">
</div>

### Estrutura do projeto
```bash
llm-router/
├── src/
│   ├── api/
│   │   ├── __init__.py
│   │   ├── routes.py
│   │   └── middleware.py
│   ├── controllers/
│   │   ├── __init__.py
│   │   ├── route_controller.py
│   │   ├── auth_controller.py
│   │   └── prompt_controller.py
│   ├── models/
│   │   ├── __init__.py
│   │   ├── request_model.py
│   │   ├── response_model.py
│   │   └── llm_model.py
│   ├── core/
│   │   ├── __init__.py
│   │   ├── routing/
│   │   │   ├── __init__.py
│   │   │   ├── route_manager.py
│   │   │   ├── load_balancer.py
│   │   │   └── request_router.py
│   │   ├── services/
│   │   │   ├── __init__.py
│   │   │   ├── prompt_manager.py
│   │   │   ├── context_manager.py
│   │   │   └── prompt_engine.py
│   │   └── providers/
│   │       ├── __init__.py
│   │       ├── base.py
│   │       ├── anthropic.py
│   │       ├── openai.py
│   │       └── google.py
│   ├── data/
│   │   ├── __init__.py
│   │   ├── database.py
│   │   ├── cache.py
│   │   └── queue.py
│   └── config/
│       ├── __init__.py
│       └── settings.py
├── tests/
│   ├── __init__.py
│   ├── test_controllers/
│   ├── test_models/
│   └── test_core/
├── docs/
│   └── api.yaml
├── requirements.txt
└── main.py




```

### Arquitetura do Sistema

## 1. VIEW LAYER (Camada de Apresentação)
- **Web Interface/API Gateway**: Ponto de entrada único para todas as requisições
- **API Documentation**: Documentação OpenAPI/Swagger para os endpoints

## 2. CONTROLLER LAYER (Camada de Controle)
- **Route Controller**: Gerencia o roteamento inicial das requisições
- **Auth Controller**: Controle de autenticação e autorização
- **Prompt Controller**: Gerenciamento dos prompts e inputs

## 3. MODEL LAYER (Camada de Modelo/Negócios)

### A. ROUTING ENGINE (🔀 Core do Sistema)
- **Route Manager**: Gerencia as regras de roteamento
- **Load Balancer**: Distribui carga entre os LLMs
- **Request Router**: Determina qual LLM usar baseado em regras específicas

### B. CORE SERVICES
- **Prompt Manager**: Gerencia e otimiza os prompts
- **Context Manager**: Mantém e gerencia o contexto das conversas
- **Prompt Engine**: Processa e prepara os prompts para os LLMs

### C. LLM PROVIDERS
Integrações com diferentes LLMs:
* Claude (Anthropic)
* GPT-4 (OpenAI)
* PaLM (Google)
* Gemini (Google)

### D. DATA LAYER
- **Database**: Armazenamento persistente
- **Redis Cache**: Cache para respostas e contextos
- **Message Queue**: Filas para processamento assíncrono

## Fluxo de Dados:
1. Requisição chega via API Gateway
2. Passa pela autenticação
3. Route Controller direciona para o Route Manager
4. Load Balancer verifica disponibilidade dos LLMs
5. Request Router seleciona o LLM mais apropriado baseado em:
   - Regras de negócio
   - Disponibilidade
   - Capacidades específicas
   - Custos
   - Performance
6. Prompt Engine prepara o prompt final
7. Resposta é processada e cacheada se necessário
8. Resultado retorna ao usuário

## Benefícios desta Arquitetura:
1. Escalabilidade horizontal e vertical
2. Alta disponibilidade
3. Isolamento de responsabilidades
4. Facilidade de manutenção
5. Possibilidade de failover entre LLMs
6. Gerenciamento eficiente de recursos
7. Cache inteligente de respostas
8. Processamento assíncrono quando necessário

Esta arquitetura é particularmente eficiente para sistemas de LLM Routing porque:
- Permite balanceamento de carga inteligente
- Facilita a adição de novos LLMs
- Gerencia eficientemente os custos
- Mantém o contexto das conversas
- Permite otimização de prompts
- Oferece alta disponibilidade
