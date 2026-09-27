---
name: analista-arquitetura-codigo
version: 1.1
description: Skill para agentes de IA avaliarem aderência de código fonte aos princípios do artigo (coerência, acoplamento, MVC, patterns, DevOps, pragmatismo) e gerar relatório percentual com classificação de risco de segurança. Artigo de referência: https://github.com/eduardobbastos/estudos-engenharia-ti/blob/main/README.md
---

## Pseudo-Algoritmo (Sequência de Prompts)

PASSO 1 — INVENTÁRIO: Liste todos os arquivos do sistema; identifique a tecnologia predominante (linguagem, framework, banco, container). Classifique se a organização é monolito, modular, microserviço ou híbrida.

PASSO 2 — ACOPLAMENTO / COESÃO: Para cada arquivo, identifique: quantas responsabilidades tem (coesão); quantas dependências diretas tem (acoplamento). Marque evidências (nomes de classes, imports, chamadas). Confronte com o artigo: alta coesão (responsabilidade única) e baixo acoplamento (dependência apenas de abstrações/DI) estão presentes?

PASSO 3 — MODELO DE ARQUITETURA: Identifique se há MVC, MVVM, Clean/Hex, EDA, CQRS, DDD. Verifique se há ports/adapters, eventos, bounded contexts, separação de command/query. Registre a aderência percentual.

PASSO 4 — PADRÕES E PRAGMATISMO: Verifique Singleton, Factory, Observer, Strategy, Adapter, DI. Registre se estão presentes; marque se há over-engineering (padrão usado sem necessidade). Classifique gravidade de risco.

PASSO 5 — DEVOPS / OBSERVABILIDADE: Verifique CI/CD (GitHub Actions, testes), logs estruturados, métricas, tracing distribuído. Registre aderência operacional.

PASSO 6 — RELATÓRIO: Consolide em texto corrido (3 parágrafos) + tabela de risco de segurança. Calcule percentual de aderência por camada.

---

## Personas dos Agentes (Conferência Cruzada — Pragmático)

| Persona | Nome | Função | Confere |
|---|---|---|---|
| Analista SE | Demerzel-SE | Avalia coesão, acoplamento, arquitetura, patterns | Se código segue MVC, Clean, EDA, CQRS, DDD conforme artigo |
| Analista DevOps | Demerzel-DevOps | Avalia observabilidade, CI/CD, deploy, risco operacional | Se há tracing, métricas, automação, rollback seguro |
| Auditor de Segurança | Demerzel-Sec | Avalia classificação de risco, impacto de segurança | Se tabela de risco está completa e precisa |
| Revisor Pragmático | Demerzel-Prag | Confere over-engineering, justifica cada padrão | Se cada padrão agrega valor real ao contexto |

PASSO 1 — SE: inventário + coesão/acoplamento.
PASSO 2 — DevOps: observabilidade + CI/CD.
PASSO 3 — Sec: classifica risco; confere evidências.
PASSO 4 — Prag: confere over-engineering; decide divergências.
PASSO 5 — Todos consolidam relatório; se divergência, Prag decide com base no artigo de referência.
PASSO 6 — Continuidade: relatório atualizado a cada commit; agentes reexecutam sequência.

---

## Pitfalls (regras imperativas + mecanismo)

- Sempre confronte evidências com o artigo de referência antes de classificar risco — conclusões sem citação do artigo são especulação e geram falsos positivos no relatório.
- Nunca aceite uma conclusão de um único agente sem conferência cruzada — o mecanismo é a divergência de perspectiva (SE vê coesão, DevOps vê operabilidade, Sec vê risco); sem conferência, o viés do agente domina.
- Se o código não tem observabilidade nativa (logs estruturados, tracing), classifique automaticamente como risco Crítico — o mecanismo é a invisibilidade de falhas em produção; sem observabilidade, rollback e resposta a incidentes são impossíveis de avaliar.
- Se um padrão (Singleton, Factory, Strategy, Adapter, DI) está presente mas não serve a uma responsabilidade coesa do módulo, registre como over-engineering e reduza a classificação de aderência — o mecanismo é a complexidade acidental que aumenta a superfície de ataque sem ganho arquitetural.
- Sempre mantenha o artigo de referência (README.md) atualizado — se o artigo muda, o pseudo-algoritmo deve ser revalidado; caso contrário, a avaliação perde a base de verdade.

---

## Texto Corrido (Modelo de Relatório — 3 Parágrafos)

O sistema analisado opera sob a tecnologia predominante [X] e organiza-se como [monolito/modular/microserviço/híbrido]; a aderência ao modelo arquitetural previsto no artigo é de [Y]% na camada de apresentação, [Z]% no domínio e [W]% na infraestrutura. Os princípios de alta coesão e baixo acoplamento estão parcialmente presentes: [evidência de coesão alta] demonstra coesão preservada, enquanto [evidência de acoplamento direto] revela acoplamento residual entre [camada A] e [camada B], violando o contrato de separação estabelecido pelo MVC e pela Clean Architecture.

No que se refere às tecnologias e sua organização, a predominância de [framework] impõe uma estrutura [descreva], que se opõe ao modelo proposto no artigo no nível [especifique]: enquanto o artigo propõe [padrão/arquitetura], o código adota [prática alternativa], resultando em [impacto — ex: acoplamento direto ao banco, falta de ports, Controller com lógica de negócio]. Os padrões GoF e DI estão presentes em [percentual] dos módulos analisados, com Singleton aplicado de forma [correta/excessiva], Factory isolando criação em [módulos], Strategy permitindo troca de algoritmos em [contextos], Adapter protegendo integrações em [pontos], e DI conectando componentes em [nível]. A ausência de [padrão] em [camada] aumenta o risco de regressão e limita a escalabilidade independente.

Do ponto de vista da segurança da informação, o nível de risco é [baixo/médio/alto/crítico] devido a [fatores: acoplamento excessivo que impede rollback independente, falta de observabilidade que oculta falhas, over-engineering que aumenta superfície de ataque, ou ausência de separação de contexto que expõe domínios sensíveis]. A continuidade no processo de desenvolvimento exige que [medidas: introduzir DI nos pontos de acoplamento direto, implementar tracing distribuído, extrair bounded contexts, reduzir Singleton em favor de injeção configurável, automatizar testes por adapter] sejam priorizadas para que a arquitetura sustente tanto a evolução funcional quanto a operação segura em produção.

---

## Tabela — Classificação de Gravidade de Risco (Segurança da Informação)

| Elemento Analisado | Evidência no Código | Gravidade do Risco | Impacto de Segurança | Ação Recomendada |
|---|---|---|---|---|
| Acoplamento direto entre camadas | Controller chama SQL diretamente; Model conhece framework | Alto | Falha em uma camada expõe dados sensíveis; rollback impossível de isolar | Introduzir Adapter + DI entre Controller e banco |
| Coesão baixa (módulo com múltiplas responsabilidades) | Classe `Pedido` calcula frete, envia notificação, salva no banco | Médio | Superfície de ataque ampliada; mudança em uma função expõe outras | Extrair responsabilidades em módulos coesos |
| Ausência de Observabilidade | Nenhum log estruturado, métrica ou trace_id nos eventos | Crítico | Falhas de segurança invisíveis; resposta a incidentes bloqueada | Implementar logs, métricas e tracing por evento |
| Singleton global sem controle | Estado compartilhado não injetado; testes não determinísticos | Médio | Estado corrompido pode ser explorado por múltiplos processos | Substituir Singleton por DI configurável por ambiente |
| Over-engineering (padrão sem propósito) | Factory usada para criar constantes; Strategy para cálculo estático | Baixo-Médio | Complexidade aumenta a superfície de erro; código difícil de auditar | Simplificar; remover padrão onde não agrega valor |
| Falta de Bounded Context | Modelo `Pedido` mistura regras de Vendas e Logística | Alto | Exposição cruzada de dados de domínio; acesso não autorizado a informações de outra área | Definir fronteiras explícitas; usar eventos entre contextos |
| EDA sem tracing distribuído | Eventos publicados sem `trace_id` ou confirmação | Crítico | Eventos perdidos ou duplicados; audit trail incompleto | Adicionar `trace_id` a todos os eventos; implementar confirmação |
| CQRS sem separação física ou de acesso | Command e Query usam mesmo repositório com permissões idênticas | Médio | Escrita acidental via query expõe dados; falta de controle de acesso diferenciado | Separar repositórios; definir permissões por operação |
| DI ausente em pontos críticos | Controller cria instâncias diretamente (`new`) | Alto | Troca de implementação exige alteração do código fonte; deploy arriscado | Injetar todas as dependências via construtor/container |
| Pragmatismo ignorado (padrão usado sem necessidade) | Adapter entre interfaces idênticas; Factory para objeto único | Baixo | Custo operacional e de manutenção aumenta sem benefício | Auditar cada padrão; remover se não agrega coesão/acoplamento |

---

## Meta-Relação — Continuidade no Processo

A avaliação não é um evento pontual. O pseudo-algoritmo deve ser executado a cada mudança significativa no código (commit, pull request, deploy). A classificação de risco deve ser atualizada; o percentual de aderência deve ser monitorado; as ações recomendadas devem ser priorizadas no backlog de desenvolvimento. Quando o artigo é a referência arquitetural, o código é a prova; o agente de IA é o analista que conecta os dois, garantindo que a teoria não permaneça no papel.
