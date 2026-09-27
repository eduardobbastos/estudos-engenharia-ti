---
title: "Complemento — MVC/GoF/DI e os 5 Padrões Arquiteturais Modernos"
---

## Introdução (relação, não substituição)

O artigo base trata MVC, Singleton, Factory, Observer, Strategy, Adapter e Dependency Injection como mecanismos internos de coesão e baixo acoplamento. Os cinco padrões abaixo não substituem esses mecanismos — eles os escalam: operam no nível de sistemas distribuídos, frontends reativos e fronteiras de domínio. A meta-relação complementar é esta: MVC + GoF + DI são as ferramentas internas; MVVM, Clean/Hexagonal, Event-Driven, CQRS e DDD são as arquiteturas que organizam essas ferramentas quando a aplicação cresce além de uma única camada.

---

## ETAPA 1 — MVVM (Model-View-ViewModel)

- **Sigla:** MVVM (Model–View–ViewModel).
- **Definição:** A ViewModel atua como mediador entre Model e View, expondo dados e ações; a View é declarativa, sem conhecimento direto do Model.
- **Aplicabilidade:** Aplicações frontend ricas (React, Vue, Angular, WPF) onde o Controller do MVC se torna pesado.
- **Exemplo estrutural:** A View renderiza uma lista; a ViewModel expõe `pedidos` e `adicionarPedido()`; o Model armazena o estado real. Nenhuma parte conhece detalhes internos das outras além do contrato.
- **Relação com original:** Substitui o Controller no cliente; usa DI para injetar o Model na ViewModel; Observer (reatividade) conecta Model e ViewModel.

---

## ETAPA 2 — Clean Architecture / Hexagonal (Ports & Adapters)

- **Sigla:** Nenhuma sigla fixa; Hexagonal = Ports and Adapters (HPA).
- **Definição:** O domínio (regras de negócio) fica no centro, independente de frameworks; interfaces (ports) definem contratos; adaptadores (adapters) conectam o domínio ao mundo externo (banco, web, fila).
- **Aplicabilidade:** Sistemas de longa vida, alta testabilidade, necessidade de trocar banco ou framework sem reescrever regras.
- **Exemplo estrutural:** O domínio `Pedido` define `IPedidoRepository` (port); um adaptador PostgreSQL implementa o port; o Controller (adapter HTTP) chama o domínio. O domínio não conhece SQL nem HTTP.
- **Relação com original:** Amplia o isolamento do MVC; usa Adapter (GoF) como mecanismo interno; DI conecta ports e adaptadores.

---

## ETAPA 3 — Event-Driven Architecture (EDA)

- **Sigla:** EDA (Event-Driven Architecture).
- **Definição:** Componentes comunicam-se por eventos assíncronos publicados num broker; produtores não conhecem consumidores diretamente.
- **Aplicabilidade:** Microserviços, fluxos assíncronos, alta escalabilidade, necessidade de auditoria (log de eventos).
- **Exemplo estrutural:** Quando um pedido é criado, o serviço `Pedido` publica `PedidoCriado`; o serviço `Estoque` consome e reserva itens; o serviço `Notificacao` envia e-mail — nenhum conhece os outros diretamente, apenas o evento.
- **Relação com original:** Evolui o Observer de intra-processo para inter-processo; mantém baixo acoplamento em nível distribuído.

---

## ETAPA 4 — CQRS (Command Query Responsibility Segregation)

- **Sigla:** CQRS.
- **Definição:** Separa modelos de escrita (commands) e leitura (queries); cada lado pode ser otimizado independentemente.
- **Aplicabilidade:** Sistemas com leitura muito maior que escrita (catálogos, dashboards) ou onde o modelo de consulta diverge do modelo de persistência.
- **Exemplo estrutural:** A operação `ConfirmarPedido` (command) atualiza a tabela `pedidos`; a consulta `HistoricoCliente` (query) lê uma tabela denormalizada `clientes_historico` otimizada para busca. Nenhuma operação mistura os dois modelos.
- **Relação com original:** Divide o Model do MVC em dois; Strategy pode trocar a estratégia de persistência por comando; DI injeta o repositório de comando ou consulta conforme necessário.

---

## ETAPA 5 — DDD: Bounded Context

- **Sigla:** DDD (Domain-Driven Design) — conceito-chave: Bounded Context.
- **Definição:** Uma fronteira explícita dentro da qual um modelo de domínio é consistente; termos como "Pedido" têm significado único dentro do contexto.
- **Aplicabilidade:** Sistemas complexos com múltiplas equipes; base para desenhar microserviços sem criar "nano-serviços" ou acoplamento acidental.
- **Exemplo estrutural:** No contexto `Vendas`, `Pedido` tem `item` e `total`; no contexto `Logistica`, `Pedido` tem `peso` e `destino`. Cada contexto tem seu Model coeso; eles se comunicam por eventos (EDA) ou APIs explícitas.
- **Relação com original:** Garante alta coesão do Model no MVC; evita que o Model cresça sem fronteiras; usa Adapter para integrar contextos.

---

## Tabela Cruzada — Complementar

| Moderno | Relação com MVC | Relação com GoF/DI original | Como reforça coesão/acoplamento |
|---|---|---|---|
| MVVM | Substitui Controller no frontend | Usa Observer + DI | View não conhece Model diretamente |
| Clean/Hex | Isola o Model como domínio central | Usa Adapter + DI internamente | Domínio independente de framework |
| EDA | Substitui comunicação direta (como entre Model e View) | Evolui Observer para distribuído | Serviços não se conhecem diretamente |
| CQRS | Divide o Model (escrita/leitura) | Usa Strategy + DI para trocar repositórios | Cada modelo tem responsabilidade única |
| DDD Context | Define fronteiras do Model | Usa Adapter entre contextos | Modelo coeso dentro de fronteiras claras |

---

## Conclusão Complementar

MVC, Singleton, Factory, Observer, Strategy, Adapter e DI são mecanismos internos de baixo acoplamento e alta coesão. MVVM, Clean/Hexagonal, Event-Driven, CQRS e Bounded Context são arquiteturas que organizam esses mecanismos quando a aplicação cresce em escala, distribuição ou complexidade de domínio. A meta-relação completa é circular: os mecanismos internos sustentam as arquiteturas modernas, e as arquiteturas modernas justificam o uso disciplinado desses mecanismos. Nenhum padrão substitui o outro — operam juntos em camadas diferentes.
