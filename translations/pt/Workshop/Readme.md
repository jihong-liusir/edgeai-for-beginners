<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "48d0fb38be925084a6ebd957d4b045e5",
  "translation_date": "2025-10-08T20:48:36+00:00",
  "source_file": "Workshop/Readme.md",
  "language_code": "pt"
}
-->
# EdgeAI para Iniciantes - Workshop

> **Percurso Prático para Construção de Aplicações Edge AI Prontas para Produção**
>
> Domine a implementação de IA local com Microsoft Foundry Local, desde a primeira conclusão de chat até a orquestração de múltiplos agentes em 6 sessões progressivas.

---

## 🎯 Introdução

Bem-vindo ao **Workshop EdgeAI para Iniciantes** - o seu guia prático e prático para construir aplicações inteligentes que funcionam inteiramente em hardware local. Este workshop transforma conceitos teóricos de Edge AI em competências reais através de exercícios progressivamente desafiantes utilizando Microsoft Foundry Local e Modelos de Linguagem Pequenos (SLMs).

### Porquê Este Workshop?

**A Revolução Edge AI Já Chegou**

Organizações em todo o mundo estão a mudar de IA dependente da cloud para computação na edge por três razões críticas:

1. **Privacidade e Conformidade** - Processar dados sensíveis localmente sem transmissão para a cloud (HIPAA, GDPR, regulamentos financeiros)
2. **Desempenho** - Eliminar latência de rede (50-500ms local vs 500-2000ms ida e volta na cloud)
3. **Controlo de Custos** - Remover custos por token de API e escalar sem despesas na cloud

**Mas Edge AI é Diferente**

Executar IA localmente requer novas competências:
- Seleção e otimização de modelos para restrições de recursos
- Gestão de serviços locais e aceleração de hardware
- Engenharia de prompts para modelos menores
- Padrões de implementação em produção para dispositivos edge

**Este Workshop Ensina Essas Competências**

Em 6 sessões focadas (~3 horas no total), irá progredir de "Hello World" até à implementação de sistemas multi-agentes prontos para produção - tudo a funcionar localmente na sua máquina.

---

## 📚 Objetivos de Aprendizagem

Ao completar este workshop, será capaz de:

### Competências Principais
1. **Implementar e Gerir Serviços de IA Locais**
   - Instalar e configurar o Microsoft Foundry Local
   - Selecionar modelos apropriados para implementação na edge
   - Gerir o ciclo de vida dos modelos (download, carregamento, cache)
   - Monitorizar o uso de recursos e otimizar o desempenho

2. **Construir Aplicações com IA**
   - Implementar conclusões de chat compatíveis com OpenAI localmente
   - Projetar prompts eficazes para Modelos de Linguagem Pequenos
   - Lidar com respostas em streaming para uma melhor experiência de utilizador
   - Integrar modelos locais em aplicações existentes

3. **Criar Sistemas RAG (Geração Aumentada por Recuperação)**
   - Construir pesquisa semântica com embeddings
   - Basear respostas de LLM em conhecimento específico do domínio
   - Avaliar a qualidade de RAG com métricas padrão da indústria
   - Escalar de protótipo para produção

4. **Otimizar o Desempenho de Modelos**
   - Testar múltiplos modelos para o seu caso de uso
   - Medir latência, throughput e tempo do primeiro token
   - Selecionar modelos ótimos com base em trade-offs de velocidade/qualidade
   - Comparar trade-offs entre SLM e LLM em cenários reais

5. **Orquestrar Sistemas Multi-Agentes**
   - Projetar agentes especializados para diferentes tarefas
   - Implementar memória de agentes e gestão de contexto
   - Coordenar agentes em fluxos de trabalho complexos
   - Roteamento inteligente de pedidos entre múltiplos modelos

6. **Implementar Soluções Prontas para Produção**
   - Implementar lógica de tratamento de erros e tentativas
   - Monitorizar o uso de tokens e recursos do sistema
   - Construir arquiteturas escaláveis com padrões de modelo como ferramentas
   - Planear caminhos de migração de edge para híbrido (edge + cloud)

---

## 🎓 Resultados de Aprendizagem

### O Que Irá Construir

No final deste workshop, terá criado:

| Sessão | Entregável | Competências Demonstradas |
|--------|------------|---------------------------|
| **1** | Aplicação de chat com streaming | Configuração de serviço, conclusões básicas, UX de streaming |
| **2** | Sistema RAG com avaliação | Embeddings, pesquisa semântica, métricas de qualidade |
| **3** | Suite de benchmarking multi-modelo | Medição de desempenho, comparação de modelos |
| **4** | Comparador SLM vs LLM | Análise de trade-offs, estratégias de otimização |
| **5** | Orquestrador multi-agente | Design de agentes, gestão de memória, coordenação |
| **6** | Sistema de roteamento inteligente | Deteção de intenção, seleção de modelos, escalabilidade |

### Matriz de Competências

| Nível de Competência | Sessão 1-2 | Sessão 3-4 | Sessão 5-6 |
|-----------------------|------------|------------|------------|
| **Iniciante**         | ✅ Configuração & básicos | ⚠️ Desafiador | ❌ Demasiado avançado |
| **Intermédio**        | ✅ Revisão rápida | ✅ Aprendizagem principal | ⚠️ Objetivos ambiciosos |
| **Avançado**          | ✅ Fácil de completar | ✅ Refinamento | ✅ Padrões de produção |

### Competências Preparadas para a Carreira

**Após este workshop, estará preparado para:**

✅ **Construir Aplicações com Foco na Privacidade**
- Aplicações de saúde que lidam com PHI/PII localmente
- Serviços financeiros com requisitos de conformidade
- Sistemas governamentais com necessidades de soberania de dados

✅ **Otimizar para Ambientes Edge**
- Dispositivos IoT com recursos limitados
- Aplicações móveis offline-first
- Sistemas em tempo real de baixa latência

✅ **Projetar Arquiteturas Inteligentes**
- Sistemas multi-agentes para fluxos de trabalho complexos
- Implementações híbridas edge-cloud
- Infraestrutura de IA otimizada para custos

✅ **Liderar Iniciativas de Edge AI**
- Avaliar a viabilidade de Edge AI para projetos
- Selecionar modelos e frameworks apropriados
- Arquitetar soluções de IA locais escaláveis

---

## 🗺️ Estrutura do Workshop

### Visão Geral das Sessões (6 Sessões × 30 Minutos = 3 Horas)

| Sessão | Tópico | Foco | Duração |
|--------|--------|------|---------|
| **1** | Introdução ao Foundry Local | Instalar, validar, primeiras conclusões | 30 min |
| **2** | Construção de Soluções de IA com RAG | Engenharia de prompts, embeddings, avaliação | 30 min |
| **3** | Modelos Open Source | Descoberta de modelos, benchmarking, seleção | 30 min |
| **4** | Modelos de Última Geração | SLM vs LLM, otimização, frameworks | 30 min |
| **5** | Agentes com IA | Design de agentes, orquestração, memória | 30 min |
| **6** | Modelos como Ferramentas | Roteamento, encadeamento, estratégias de escalabilidade | 30 min |

---

## 🚀 Início Rápido

### Pré-requisitos

**Requisitos de Sistema:**
- **OS**: Windows 10/11, macOS 11+, ou Linux (Ubuntu 20.04+)
- **RAM**: Mínimo de 8GB, recomendado 16GB+
- **Armazenamento**: 10GB+ de espaço livre para modelos
- **CPU**: Processador moderno com suporte AVX2
- **GPU** (opcional): Compatível com CUDA ou Qualcomm NPU para aceleração

**Requisitos de Software:**
- **Python 3.8+** ([Download](https://www.python.org/downloads/))
- **Microsoft Foundry Local** ([Guia de Instalação](../../../Workshop))
- **Git** ([Download](https://git-scm.com/downloads))
- **Visual Studio Code** (recomendado) ([Download](https://code.visualstudio.com/))

### Configuração em 3 Passos

#### 1. Instalar Foundry Local

**Windows:**
```powershell
winget install Microsoft.FoundryLocal
```

**macOS:**
```bash
brew tap microsoft/foundrylocal
brew install foundrylocal
```

**Verificar Instalação:**
```bash
foundry --version
foundry service status
```

#### 2. Clonar Repositório e Instalar Dependências

```bash
# Clone repository
git clone https://github.com/microsoft/edgeai-for-beginners.git
cd edgeai-for-beginners/Workshop

# Create virtual environment
python -m venv .venv

# Activate virtual environment
# Windows:
.\.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

#### 3. Executar o Primeiro Exemplo

```bash
# Start Foundry Local and load a model
foundry model run phi-4-mini

# Run the chat bootstrap sample
cd samples/session01
python chat_bootstrap.py "What is edge AI?"
```

**✅ Sucesso!** Deve ver uma resposta em streaming sobre Edge AI.

---

## 📦 Recursos do Workshop

### Exemplos em Python

Exemplos práticos progressivos demonstrando cada conceito:

| Sessão | Exemplo | Descrição | Tempo de Execução |
|--------|---------|-----------|-------------------|
| 1 | [`chat_bootstrap.py`](../../../Workshop/samples/session01/chat_bootstrap.py) | Chat básico & streaming | ~30s |
| 2 | [`rag_pipeline.py`](../../../Workshop/samples/session02/rag_pipeline.py) | RAG com embeddings | ~45s |
| 2 | [`rag_eval_ragas.py`](../../../Workshop/samples/session02/rag_eval_ragas.py) | Avaliação de qualidade RAG | ~60s |
| 3 | [`benchmark_oss_models.py`](../../../Workshop/samples/session03/benchmark_oss_models.py) | Benchmarking multi-modelo | ~2-3m |
| 4 | [`model_compare.py`](../../../Workshop/samples/session04/model_compare.py) | Comparação SLM vs LLM | ~45s |
| 5 | [`agents_orchestrator.py`](../../../Workshop/samples/session05/agents_orchestrator.py) | Sistema multi-agente | ~60s |
| 6 | [`models_router.py`](../../../Workshop/samples/session06/models_router.py) | Roteamento baseado em intenção | ~45s |
| 6 | [`models_pipeline.py`](../../../Workshop/samples/session06/models_pipeline.py) | Pipeline multi-etapas | ~60s |

### Notebooks Jupyter

Exploração interativa com explicações e visualizações:

| Sessão | Notebook | Descrição | Dificuldade |
|--------|----------|-----------|-------------|
| 1 | [`session01_chat_bootstrap.ipynb`](./notebooks/session01_chat_bootstrap.ipynb) | Básicos de chat & streaming | ⭐ Iniciante |
| 2 | [`session02_rag_pipeline.ipynb`](./notebooks/session02_rag_pipeline.ipynb) | Construir sistema RAG | ⭐⭐ Intermédio |
| 2 | [`session02_rag_eval_ragas.ipynb`](./notebooks/session02_rag_eval_ragas.ipynb) | Avaliar qualidade RAG | ⭐⭐ Intermédio |
| 3 | [`session03_benchmark_oss_models.ipynb`](./notebooks/session03_benchmark_oss_models.ipynb) | Benchmarking de modelos | ⭐⭐ Intermédio |
| 4 | [`session04_model_compare.ipynb`](./notebooks/session04_model_compare.ipynb) | Comparação de modelos | ⭐⭐ Intermédio |
| 5 | [`session05_agents_orchestrator.ipynb`](./notebooks/session05_agents_orchestrator.ipynb) | Orquestração de agentes | ⭐⭐⭐ Avançado |
| 6 | [`session06_models_router.ipynb`](./notebooks/session06_models_router.ipynb) | Roteamento por intenção | ⭐⭐⭐ Avançado |
| 6 | [`session06_models_pipeline.ipynb`](./notebooks/session06_models_pipeline.ipynb) | Orquestração de pipeline | ⭐⭐⭐ Avançado |

### Documentação

Guias e referências abrangentes:

| Documento | Descrição | Quando Usar |
|-----------|-----------|-------------|
| [QUICK_START.md](./QUICK_START.md) | Guia de configuração rápida | Começando do zero |
| [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) | Resumo de comandos & APIs | Precisa de respostas rápidas |
| [FOUNDRY_SDK_QUICKREF.md](./FOUNDRY_SDK_QUICKREF.md) | Padrões & exemplos de SDK | Escrevendo código |
| [ENV_CONFIGURATION.md](./ENV_CONFIGURATION.md) | Guia de variáveis de ambiente | Configurando exemplos |
| [SAMPLES_UPDATE_SUMMARY.md](./SAMPLES_UPDATE_SUMMARY.md) | Melhorias recentes nos exemplos | Compreendendo mudanças |
| [SDK_MIGRATION_NOTES.md](./SDK_MIGRATION_NOTES.md) | Guia de migração | Atualizando código |
| [notebooks/TROUBLESHOOTING.md](./notebooks/TROUBLESHOOTING.md) | Problemas comuns & soluções | Depurando problemas |

---

## 🎓 Recomendações de Percurso de Aprendizagem

### Para Iniciantes (3-4 horas)
1. ✅ Sessão 1: Introdução (foco na configuração e chat básico)
2. ✅ Sessão 2: Básicos de RAG (ignorar avaliação inicialmente)
3. ✅ Sessão 3: Benchmarking simples (apenas 2 modelos)
4. ⏭️ Ignorar Sessões 4-6 por agora
5. 🔄 Retornar às Sessões 4-6 após construir a primeira aplicação

### Para Desenvolvedores Intermédios (3 horas)
1. ⚡ Sessão 1: Validação rápida da configuração
2. ✅ Sessão 2: Pipeline completo de RAG com avaliação
3. ✅ Sessão 3: Suite completa de benchmarking
4. ✅ Sessão 4: Otimização de modelos
5. ✅ Sessões 5-6: Foco em padrões de arquitetura

### Para Praticantes Avançados (2-3 horas)
1. ⚡ Sessões 1-3: Revisão rápida e validação
2. ✅ Sessão 4: Mergulho profundo na otimização
3. ✅ Sessão 5: Arquitetura multi-agente
4. ✅ Sessão 6: Padrões de produção e escalabilidade
5. 🚀 Extensão: Construir lógica de roteamento personalizada e implementações híbridas

---

## Pacote de Sessões do Workshop (Laboratórios Focados de 30 Minutos)

Se estiver a seguir o formato condensado de 6 sessões do workshop, utilize estes guias dedicados (cada um complementa os módulos mais amplos acima):

| Sessão do Workshop | Guia | Foco Principal |
|--------------------|------|----------------|
| 1 | [Session01-GettingStartedFoundryLocal](./Session01-GettingStartedFoundryLocal.md) | Instalar, validar, executar phi & GPT-OSS-20B, aceleração |
| 2 | [Session02-BuildAISolutionsRAG](./Session02-BuildAISolutionsRAG.md) | Engenharia de prompts, padrões RAG, grounding em CSV & documentos, migração |
| 3 | [Session03-OpenSourceModels](./Session03-OpenSourceModels.md) | Integração com Hugging Face, benchmarking, seleção de modelos |
| 4 | [Session04-CuttingEdgeModels](./Session04-CuttingEdgeModels.md) | SLM vs LLM, WebGPU, Chainlit RAG, aceleração ONNX |
| 5 | [Session05-AIPoweredAgents](./Session05-AIPoweredAgents.md) | Funções de agentes, memória, ferramentas, orquestração |
| 6 | [Session06-ModelsAsTools](./Session06-ModelsAsTools.md) | Roteamento, encadeamento, caminho de escalabilidade para Azure |
Cada ficheiro de sessão inclui: resumo, objetivos de aprendizagem, fluxo de demonstração de 30 minutos, projeto inicial, lista de verificação de validação, resolução de problemas e referências ao SDK oficial Foundry Local Python.

### Scripts de Exemplo

Instalar dependências do workshop (Windows):

```powershell
cd Workshop
py -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
```

macOS / Linux:

```bash
cd Workshop
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Se estiver a executar o serviço Foundry Local numa máquina ou VM diferente (Windows) a partir de macOS, exporte o endpoint:

```bash
export FOUNDRY_LOCAL_ENDPOINT=http://<windows-host>:5273/v1
```

| Sessão | Script(s) | Descrição |
|--------|-----------|-----------|
| 1 | `samples/session01/chat_bootstrap.py` | Serviço inicial e chat em streaming |
| 2 | `samples/session02/rag_pipeline.py` | RAG mínimo (embeddings em memória) |
|   | `samples/session02/rag_eval_ragas.py` | Avaliação RAG com métricas ragas |
| 3 | `samples/session03/benchmark_oss_models.py` | Benchmarking de latência e throughput multi-modelo |
| 4 | `samples/session04/model_compare.py` | Comparação SLM vs LLM (latência e saída de exemplo) |
| 5 | `samples/session05/agents_orchestrator.py` | Pipeline de investigação → editorial com dois agentes |
| 6 | `samples/session06/models_router.py` | Demonstração de routing baseado em intenções |
|   | `samples/session06/models_pipeline.py` | Cadeia de planeamento/execução/refinamento em múltiplos passos |

### Variáveis de Ambiente (Comuns a Todos os Exemplos)

| Variável | Finalidade | Exemplo |
|----------|------------|---------|
| `FOUNDRY_LOCAL_ALIAS` | Alias padrão de modelo único para exemplos básicos | `phi-4-mini` |
| `SLM_ALIAS` / `LLM_ALIAS` | Modelo SLM explícito vs modelo maior para comparação | `phi-4-mini` / `gpt-oss-20b` |
| `BENCH_MODELS` | Lista de aliases para benchmarking | `qwen2.5-0.5b,gemma-2-2b,mistral-7b` |
| `BENCH_ROUNDS` | Repetições de benchmark por modelo | `3` |
| `BENCH_PROMPT` | Prompt usado no benchmarking | `Explain retrieval augmented generation briefly.` |
| `EMBED_MODEL` | Modelo de embeddings de sentence-transformers | `sentence-transformers/all-MiniLM-L6-v2` |
| `RAG_QUESTION` | Substituir consulta de teste para pipeline RAG | `Why use RAG with local inference?` |
| `AGENT_QUESTION` | Substituir consulta para pipeline de agentes | `Explain why edge AI matters for compliance.` |
| `AGENT_MODEL_PRIMARY` | Alias de modelo para agente de investigação | `phi-4-mini` |
| `AGENT_MODEL_EDITOR` | Alias de modelo para agente editor (pode ser diferente) | `gpt-oss-20b` |
| `SHOW_USAGE` | Quando `1`, imprime uso de tokens por conclusão | `1` |
| `RETRY_ON_FAIL` | Quando `1`, tenta novamente em caso de erros transitórios no chat | `1` |
| `RETRY_BACKOFF` | Segundos de espera antes de tentar novamente | `1.0` |

Se uma variável não estiver definida, os scripts utilizam valores padrão sensatos. Para demonstrações de modelo único, normalmente só precisa de `FOUNDRY_LOCAL_ALIAS`.

### Módulo de Utilidade

Todos os exemplos agora partilham um helper `samples/workshop_utils.py` que fornece:

* Criação de cliente OpenAI + `FoundryLocalManager` com cache
* Helper `chat_once()` com opção de retry + impressão de uso
* Relatórios simples de uso de tokens (ativar via `SHOW_USAGE=1`)

Isto reduz duplicação e destaca boas práticas para orquestração eficiente de modelos locais.

## Melhorias Opcionais (Entre Sessões)

| Tema | Melhoria | Sessões | Env / Alternância |
|------|----------|---------|-------------------|
| Determinismo | Temperatura fixa + conjuntos de prompts estáveis | 1–6 | Definir `temperature=0`, `top_p=1` |
| Visibilidade de Uso de Tokens | Ensino consistente de custo/eficiência | 1–6 | `SHOW_USAGE=1` |
| Primeiro Token em Streaming | Métrica de latência percebida | 1,3,4,6 | `BENCH_STREAM=1` (benchmark) |
| Resiliência a Retries | Lida com cold-start transitório | Todas | `RETRY_ON_FAIL=1` + `RETRY_BACKOFF` |
| Agentes Multi-Modelo | Especialização de papéis heterogéneos | 5 | `AGENT_MODEL_PRIMARY`, `AGENT_MODEL_EDITOR` |
| Routing Adaptativo | Heurísticas de intenção + custo | 6 | Expandir router com lógica de escalonamento |
| Memória Vetorial | Recall semântico de longo prazo | 2,5,6 | Integrar índice de embeddings FAISS/Chroma |
| Exportação de Traços | Auditoria e avaliação | 2,5,6 | Adicionar linhas JSON por passo |
| Rubricas de Qualidade | Acompanhamento qualitativo | 3–6 | Prompts de pontuação secundária |
| Testes de Fumo | Validação rápida pré-workshop | Todas | `python Workshop/tests/smoke.py` |

### Início Rápido Determinístico

```powershell
set FOUNDRY_LOCAL_ALIAS=phi-4-mini
set SHOW_USAGE=1
python Workshop\tests\smoke.py
```

Espere contagens de tokens estáveis em entradas idênticas repetidas.

### Avaliação RAG (Sessão 2)

Utilize `rag_eval_ragas.py` para calcular relevância da resposta, fidelidade e precisão de contexto num pequeno conjunto de dados sintético:

```powershell
python samples/session02/rag_eval_ragas.py
```

Expanda fornecendo um JSONL maior de perguntas, contextos e verdades base, convertendo depois para um `Dataset` do Hugging Face.

## Apêndice de Precisão de Comandos CLI

O workshop utiliza deliberadamente apenas comandos CLI Foundry Local atualmente documentados/estáveis.

### Comandos Estáveis Referenciados

| Categoria | Comando | Finalidade |
|-----------|---------|------------|
| Core | `foundry --version` | Mostrar versão instalada |
| Core | `foundry init` | Inicializar configuração |
| Serviço | `foundry service start` | Iniciar serviço local (se não automático) |
| Serviço | `foundry status` | Mostrar estado do serviço |
| Modelos | `foundry model list` | Listar catálogo / modelos disponíveis |
| Modelos | `foundry model download <alias>` | Transferir pesos do modelo para cache |
| Modelos | `foundry model run <alias>` | Lançar (carregar) um modelo localmente; combinar com `--prompt` para one-shot |
| Modelos | `foundry model unload <alias>` / `foundry model stop <alias>` | Descarregar um modelo da memória (se suportado) |
| Cache | `foundry cache list` | Listar modelos em cache (transferidos) |
| Sistema | `foundry system info` | Snapshot de capacidades de hardware e aceleração |
| Sistema | `foundry system gpu-info` | Informações de diagnóstico de GPU |
| Configuração | `foundry config list` | Mostrar valores de configuração atuais |
| Configuração | `foundry config set <key> <value>` | Atualizar configuração |

### Padrão de Prompt One-Shot

Em vez de um subcomando `model chat` descontinuado, utilize:

```powershell
foundry model run <alias> --prompt "Your question here"
```

Isto executa um ciclo único de prompt/resposta e depois sai.

### Padrões Removidos / Evitados

| Descontinuado / Não Documentado | Substituição / Orientação |
|---------------------------------|---------------------------|
| `foundry model chat <model> "..."` | `foundry model run <model> --prompt "..."` |
| `foundry model list --running` | Utilizar `foundry model list` simples + atividade recente / logs |
| `foundry model list --cached` | `foundry cache list` |
| `foundry model stats <model>` | Utilizar script de benchmark Python + ferramentas do SO (Task Manager / `nvidia-smi`) |
| `foundry model benchmark ...` | `samples/session03/benchmark_oss_models.py` |

### Benchmarking e Telemetria

- Latência, p95, tokens/segundo: `samples/session03/benchmark_oss_models.py`
- Latência do primeiro token (streaming): definir `BENCH_STREAM=1`
- Uso de recursos: monitores do SO (Task Manager, Activity Monitor, `nvidia-smi`) + `foundry system info`.

À medida que novos comandos de telemetria CLI estabilizam, podem ser incorporados com edições mínimas nos markdowns das sessões.

### Linter Automático de CLI

Um linter automático impede a reintrodução de padrões CLI descontinuados dentro de blocos de código delimitados em ficheiros markdown:

Script: `Workshop/scripts/lint_markdown_cli.py`

Padrões descontinuados são bloqueados dentro de blocos de código.

Substituições recomendadas:
| Descontinuado | Substituição |
|---------------|-------------|
| `foundry model chat <a> "..."` | `foundry model run <a> --prompt "..."` |
| `model list --running` | `model list` |
| `model list --cached` | `cache list` |
| `model stats` | Script de benchmark + ferramentas do sistema |
| `model benchmark` | `samples/session03/benchmark_oss_models.py` |
| `model list --available` | `model list` |

Executar localmente:
```powershell
python Workshop\scripts\lint_markdown_cli.py --verbose
```

GitHub Action: `.github/workflows/markdown-cli-lint.yml` executa em cada push e PR.

Hook opcional de pré-commit:
```bash
echo "python Workshop/scripts/lint_markdown_cli.py" > .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

## Tabela Rápida de Migração CLI → SDK

| Tarefa | Comando CLI | Equivalente SDK (Python) | Notas |
|-------|-------------|--------------------------|-------|
| Executar um modelo uma vez (prompt) | `foundry model run phi-4-mini --prompt "Hello"` | `manager=FoundryLocalManager("phi-4-mini"); client=OpenAI(base_url=manager.endpoint, api_key=manager.api_key or "not-needed"); client.chat.completions.create(model=manager.get_model_info("phi-4-mini").id, messages=[{"role":"user","content":"Hello"}])` | O SDK inicializa automaticamente o serviço e o cache |
| Transferir (cache) modelo | `foundry model download qwen2.5-0.5b` | `FoundryLocalManager("qwen2.5-0.5b")  # triggers download/load` | O Manager escolhe a melhor variante se o alias mapear para múltiplas builds |
| Listar catálogo | `foundry model list` | `# use manager for each alias or maintain known list` | CLI agrega; SDK atualmente por instância de alias |
| Listar modelos em cache | `foundry cache list` | `manager.list_cached_models()` | Após inicialização do manager (qualquer alias) |
| Ativar aceleração GPU | `foundry config set compute.onnx.enable_gpu true` | `# CLI action; SDK assumes config already applied` | Configuração é efeito externo |
| Obter URL do endpoint | (implícito) | `manager.endpoint` | Usado para criar cliente compatível com OpenAI |
| Aquecer um modelo | `foundry model run <alias>` e depois primeiro prompt | `chat_once(alias, messages=[...])` (utilitário) | Utilitários lidam com aquecimento inicial de latência fria |
| Medir latência | `python benchmark_oss_models.py` | `import benchmark_oss_models` (ou novo script de exportação) | Preferir script para métricas consistentes |
| Parar / descarregar modelo | `foundry model unload <alias>` | (Não exposto – reiniciar serviço/processo) | Normalmente não necessário para fluxo de workshop |
| Recuperar uso de tokens | (ver saída) | `resp.usage.total_tokens` | Fornecido se o backend retornar objeto de uso |

## Exportação Markdown de Benchmark

Utilize o script `Workshop/scripts/export_benchmark_markdown.py` para executar um benchmark fresco (mesma lógica que `samples/session03/benchmark_oss_models.py`) e emitir uma tabela Markdown amigável para GitHub mais JSON bruto.

### Exemplo

```powershell
python Workshop\scripts\export_benchmark_markdown.py --models "qwen2.5-0.5b,gemma-2-2b,mistral-7b" --prompt "Explain retrieval augmented generation briefly." --rounds 3 --output benchmark_report.md
```

Ficheiros gerados:
| Ficheiro | Conteúdo |
|----------|----------|
| `benchmark_report.md` | Tabela Markdown + dicas de interpretação |
| `benchmark_report.json` | Array de métricas bruto (para comparação/detecção de tendências) |

Defina `BENCH_STREAM=1` no ambiente para incluir latência do primeiro token, se suportado.

---

**Aviso**:  
Este documento foi traduzido utilizando o serviço de tradução por IA [Co-op Translator](https://github.com/Azure/co-op-translator). Embora nos esforcemos pela precisão, esteja ciente de que traduções automáticas podem conter erros ou imprecisões. O documento original na sua língua nativa deve ser considerado a fonte autoritária. Para informações críticas, recomenda-se uma tradução profissional realizada por humanos. Não nos responsabilizamos por quaisquer mal-entendidos ou interpretações incorretas decorrentes do uso desta tradução.