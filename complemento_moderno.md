---
title: "Complemento — MVC, GoF, DI e os 5 Padrões Arquiteturais Modernos"
---

## ETAPA 1 — Introdução Conceitual (relação, não substituição)

O artigo original trata MVC, Singleton, Factory Method, Observer, Strategy, Adapter e Dependency Injection como mecanismos internos de alta coesão e baixo acoplamento. Os cinco padrões abaixo — MVVM, Clean Architecture / Hexagonal, Event-Driven Architecture (EDA), CQRS e DDD (Bounded Context) — não substituem esses mecanismos. Eles os escalam para sistemas distribuídos, frontends reativos e domínios complexos.

**Meta-relação complementar:** MVC + GoF + DI são ferramentas internas; MVVM + Clean + EDA + CQRS + DDD são arquiteturas que organizam essas ferramentas quando a aplicação cresce além de uma única camada. Nenhum substitui o outro — operam em camadas diferentes, reforçando o mesmo objetivo arquitetural.

---

## ETAPA 2 — MVVM (Model-View-ViewModel)

- **Sigla:** MVVM (Model–View–ViewModel) — padrão arquitetural de apresentação (derivado do MVC).
- **Definição:** A ViewModel atua como mediador entre Model e View; expõe dados e ações; a View é declarativa, sem conhecimento direto do Model. O Controller do MVC é substituído pela ViewModel.
- **Aplicabilidade:** Aplicações frontend ricas (React, Vue, Angular, WPF) onde a coordenação de entrada cresce além do que um Controller simples pode gerir sem perder coesão.
- **Exemplo estrutural:** A View (`ListaDePedidos`) renderiza componentes; a ViewModel (`PedidoViewModel`) expõe `pedidos: Observable[]` e `confirmar(id)`. O Model (`Pedido`) armazena regras de negócio. Nenhuma parte conhece detalhes internos das outras além do contrato de interface. A ViewModel usa DI para receber o Model; a reatividade (Observer) conecta mudanças do Model à View.
- **Relação com original:** Evolui o Controller (MVC) para um mediador declarativo; usa DI (original) para injetar o Model; usa Observer (original) para reatividade.

---

## ETAPA 3 — Clean Architecture / Hexagonal (Ports & Adapters)

- **Sigla:** Nenhuma sigla fixa além de Clean Architecture (Robert C. Martin) ou Hexagonal = HPA (Ports and Adapters, Alistair Cockburn).
- **Definição:** O domínio (entidades + regras de negócio) fica no centro da aplicação, independente de frameworks, bancos ou interfaces. Portas (ports) definem contratos; adaptadores (adapters) conectam o domínio ao mundo externo. As dependências apontam apenas para o centro.
- **Aplicabilidade:** Sistemas de longa vida, alta testabilidade, necessidade de trocar banco, framework ou interface sem reescrever regras de negócio. Quando o Model do MVC cresce e precisa ser isolado de detalhes técnicos.
- **Exemplo estrutural:** O domínio define `Pedido` com `calcularTotal()` e uma porta `IPedidoRepository`. Um adaptador PostgreSQL implementa `IPedidoRepository`; um adaptador HTTP (Controller) recebe requisições e delega ao domínio. O domínio não conhece SQL, HTTP ou framework — apenas suas próprias regras e contratos de porta. DI conecta adaptadores ao domínio.
- **Relação com original:** Amplia o isolamento do Model (MVC) para uma arquitetura completa; usa Adapter (GoF) como mecanismo interno; usa DI para conectar ports e adaptadores; garante alta coesão do domínio e baixo acoplamento com infraestrutura.

---

## ETAPA 4 — Event-Driven Architecture (EDA)

- **Sigla:** EDA (Event-Driven Architecture).
- **Definição:** Componentes comunicam-se por eventos assíncronos publicados num broker (Kafka, RabbitMQ, EventBridge); produtores publicam fatos; consumidores reagem de forma independente. Nenhum componente conhece os outros diretamente.
- **Aplicabilidade:** Microserviços, fluxos assíncronos, alta escalabilidade, necessidade de auditoria (cada evento é logado), sistemas onde a resposta imediata não é obrigatória.
- **Exemplo estrutural:** Quando o serviço `Vendas` processa um pedido, publica o evento `PedidoConfirmado` no broker. O serviço `Estoque` consome e reserva itens; o serviço `Notificacao` envia e-mail; o serviço `Financeiro` registra a transação. Nenhum serviço conhece os outros — todos dependem apenas do contrato do evento (`PedidoConfirmado`). O baixo acoplamento é preservado em nível distribuído; a coesão é mantida porque cada serviço tem uma única responsabilidade (reserva, notificação, registro).
- **Relação com original:** Evolui o Observer (GoF) de intra-processo para inter-processo; substitui a comunicação direta entre Model e View (MVC) por comunicação assíncrona; usa DI para injetar produtores e consumidores de eventos.

---

## ETAPA 5 — CQRS (Command Query Responsibility Segregation)

- **Sigla:** CQRS (Command Query Responsibility Segregation) — padrão arquitetural de persistência.
- **Definição:** Separa modelos, lógica e armazenamento de escrita (commands) dos de leitura (queries). Cada lado pode ser otimizado, escalado e mantido independentemente. Não é obrigatório usar bancos separados — pode ser o mesmo banco com esquemas diferentes.
- **Aplicabilidade:** Sistemas onde a leitura é muito maior que a escrita (catálogos, dashboards, históricos) ou onde o modelo de consulta diverge significativamente do modelo de transação (ex: consulta por múltiplos filtros vs. atualização de um pedido simples).
- **Exemplo estrutural:** A operação `ConfirmarPedido` (command) atualiza a tabela `pedidos` e publica `PedidoConfirmado`; a consulta `HistoricoCliente` (query) lê uma tabela denormalizada `clientes_historico` otimizada para busca rápida por período. Nenhuma operação mistura os dois modelos. A coesão é preservada: o comando tem uma responsabilidade (escrever); a query tem outra (ler otimizado). Strategy (GoF) pode trocar a estratégia de comando; DI injeta o repositório de comando ou consulta conforme necessário.
- **Relação com original:** Divide o Model (MVC) em dois modelos coesos; usa Strategy (GoF) para trocar implementações de persistência; usa DI para injetar o repositório correto; evita que o acoplamento de uma única estrutura de dados limite a evolução do sistema.

---

## ETAPA 6 — DDD: Bounded Context

- **Sigla:** DDD (Domain-Driven Design) — conceito-chave: Bounded Context (fronteira explícita de domínio).
- **Definição:** Uma fronteira explícita dentro da qual um modelo de domínio é consistente. Termos como "Pedido", "Cliente" ou "Produto" têm significado único dentro do contexto. Fora dele, esses termos podem ter significados diferentes. Cada contexto tem seu próprio Model coeso e se comunica com outros por eventos (EDA) ou APIs explícitas.
- **Aplicabilidade:** Sistemas complexos com múltiplas equipes; base para desenhar microserviços sem criar "nano-serviços" (serviços muito pequenos e acoplados) ou acoplamento acidental entre domínios diferentes.
- **Exemplo estrutural:** No contexto `Vendas`, `Pedido` tem `item`, `quantidade` e `total` e segue regras de desconto. No contexto `Logistica`, `Pedido` tem `peso`, `dimensoes` e `destino` e segue regras de roteirização. Cada contexto tem seu Model coeso; eles não compartilham classes diretamente. A comunicação ocorre por eventos (`PedidoConfirmado`) ou APIs explícitas. Adapter (GoF) implementa a integração entre contextos; DI injeta os adaptadores.
- **Relação com original:** Garante alta coesão do Model (MVC) ao evitar que ele cresça sem fronteiras; evita acoplamento acidental entre conceitos de domínio diferentes; usa Adapter e EDA (padrões originais/complementares) para integrar contextos sem quebrar a separação.

---

## ETAPA 7 — Relação Cruzada Completa (Original + Complemento)

| Elemento | Como preserva alta coesão | Como reduz acoplamento | Camada arquitetural |
|---|---|---|---|
| MVC | Cada camada tem responsabilidade única | Controller não conhece internos da View; View não acessa Model diretamente | Apresentação / Aplicação |
| Singleton | Estado global coeso, sem duplicação | Acesso centralizado, sem dependências espalhadas | Infraestrutura interna |
| Factory | Criação isolada, sem misturar regras de negócio | Cliente depende da fábrica abstrata, não da classe concreta | Criação (GoF) |
| Observer | Notificação focada no evento | Model não conhece observadores específicos | Comportamento (GoF) |
| Strategy | Algoritmo coeso, trocável | Contexto depende apenas da estratégia, não das implementações | Comportamento (GoF) |
| Adapter | Conversão isolada em uma classe | Cliente e serviço externo não se conhecem diretamente | Estrutural (GoF) |
| DI | Cada componente recebe apenas o que precisa | Nenhum componente cria dependências diretamente | Injeção (arquitetural) |
| MVVM | ViewModel coeso, View declarativa | View não conhece Model diretamente | Apresentação (moderno) |
| Clean/Hex | Domínio coeso no centro | Domínio independente de framework | Sistema (moderno) |
| EDA | Cada serviço tem responsabilidade única | Serviços não se conhecem diretamente, apenas eventos | Distribuição (moderno) |
| CQRS | Cada modelo (comando/query) coeso | Escrita e leitura independentes | Persistência (moderno) |
| DDD Context | Modelo coeso dentro de fronteiras claras | Contextos não compartilham modelos diretamente | Domínio (moderno) |

---

## ETAPA 8 — Conclusão Completa

Alta coesão e baixo acoplamento são os critérios que guiam tanto os mecanismos internos (MVC, Singleton, Factory, Observer, Strategy, Adapter, DI) quanto as arquiteturas modernas (MVVM, Clean/Hexagonal, EDA, CQRS, Bounded Context). Os mecanismos são as ferramentas; as arquiteturas são os sistemas que organizam essas ferramentas. Nenhum substitui o outro — eles operam em camadas complementares. A meta-relação completa é circular: o objetivo arquitetural (coerência e flexibilidade) guia a escolha dos mecanismos internos e das arquiteturas externas; e esses mecanismos e arquiteturas reforçam o objetivo, permitindo que o sistema cresça sem perder a clareza estrutural.

---

*Complemento técnico — sem código-fonte, apenas estruturas de arquitetura, definição de siglas, aplicabilidade, exemplos estruturais e relação conceitual com o artigo base.*
