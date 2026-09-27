---
title: "Alta Coesão e Baixo Acoplamento — MVC e os 5 Design Patterns Fundamentais"
---

## ETAPA 1 — Introdução conceitual

A arquitetura de software busca duas metas complementares: **alta coesão** (cada parte faz uma única coisa, com foco claro) e **baixo acoplamento** (partes dependem minimamente umas das outras). Essas metas não são técnicas isoladas; são critérios de qualidade que guiam a escolha de padrões arquiteturais como o MVC e padrões de design estruturais.

**Meta-relação:** MVC organiza a aplicação em camadas; os design patterns resolvem problemas recorrentes dentro dessas camadas. Ambos existem para sustentar coesão e reduzir acoplamento.

---

## ETAPA 2 — Alta Coesão / Baixo Acoplamento

- **Sigla:** HC/BA (High Cohesion / Low Coupling) — termo de engenharia de software, sem sigla padronizada além da expressão.
- **Definição:** Coesão mede o quanto as responsabilidades de um módulo estão relacionadas entre si; acoplamento mede a dependência de um módulo em relação a outros.
- **Aplicabilidade:** Todo sistema modular; essencial em manutenção, testes e evolução de código.
- **Exemplo estrutural:** Em um sistema de pedidos, o módulo "Calcular Frete" contém apenas regras de frete (alta coesão) e recebe dados via interface abstrata, sem conhecer o banco de dados diretamente (baixo acoplamento).

---

## ETAPA 3 — MVC (Model–View–Controller)

- **Sigla:** MVC (Model, View, Controller) — padrão arquitetural de separação de responsabilidades.
- **Definição:** Divide a aplicação em três camadas: Model (dados e regras), View (apresentação), Controller (coordenação de entrada e fluxo).
- **Aplicabilidade:** Aplicações interativas (web, desktop, mobile); quando a interface precisa mudar frequentemente sem afetar a lógica.
- **Exemplo estrutural:**
  - **Model:** Entidades Pedido, Cliente, Estoque e suas regras de negócio.
  - **View:** Tela de listagem, formulário de cadastro; apenas renderiza dados recebidos.
  - **Controller:** Recebe a requisição de listar pedidos, consulta o Model, entrega o resultado à View. Nenhuma das três camadas conhece detalhes internos das outras além do contrato necessário.

---

## ETAPA 4 — 5 Design Patterns Comprovados

### 4.1 Singleton
- **Sigla:** Nenhuma sigla além do nome; padrão criacional (GoF).
- **Definição:** Garante que uma classe tenha apenas uma instância e fornece um ponto de acesso global a ela.
- **Aplicabilidade:** Estado compartilhado que deve ser único no sistema (ex: configuração, log, pool de conexões).
- **Exemplo estrutural:** Uma classe Configuração armazena parâmetros da aplicação; qualquer módulo solicita Configuração.getInstancia() sem criar objetos duplicados, mantendo coesão no gerenciamento de estado.

### 4.2 Factory Method (Método Fábrica)
- **Sigla:** Nenhuma sigla padrão; padrão criacional (GoF).
- **Definição:** Define uma interface para criar objetos, permitindo que subclasses decidam qual classe instanciar, sem expor a lógica de criação ao cliente.
- **Aplicabilidade:** Quando o sistema precisa criar objetos cujo tipo exato só é conhecido em tempo de execução ou varia por contexto.
- **Exemplo estrutural:** Uma fábrica de Relatórios recebe o tipo (PDF, CSV) e retorna o gerador adequado; o Controller solicita o relatório sem conhecer a implementação concreta.

### 4.3 Observer (Observador)
- **Sigla:** Nenhuma sigla padrão; padrão comportamental (GoF).
- **Definição:** Define uma dependência um-para-muitos entre objetos, de modo que quando um objeto muda de estado, todos os seus dependentes são notificados automaticamente.
- **Aplicabilidade:** Eventos, notificações, atualização de interface quando o Model muda (como no MVC reativo).
- **Exemplo estrutural:** Quando o estoque de um item muda no Model, o sistema notifica automaticamente a View de disponibilidade e o Controller de alerta, sem que o Model conheça os detalhes dos observadores.

### 4.4 Strategy (Estratégia)
- **Sigla:** Nenhuma sigla padrão; padrão comportamental (GoF).
- **Definição:** Encapsula uma família de algoritmos, tornando-os intercambiáveis sem alterar o contexto que os utiliza.
- **Aplicabilidade:** Cálculos variáveis (desconto, frete, impostos) que mudam conforme regras de negócio ou região.
- **Exemplo estrutural:** O módulo Pedido recebe uma estratégia de cálculo de frete; para frete padrão, usa EstratégiaPadrão; para frete expresso, substitui por EstratégiaExpresso, sem modificar o Pedido.

### 4.5 Adapter (Adaptador)
- **Sigla:** Nenhuma sigla padrão; padrão estrutural (GoF).
- **Definição:** Permite que interfaces incompatíveis trabalhem juntas, traduzindo a interface de uma classe para outra esperada pelo cliente.
- **Aplicabilidade:** Integração com sistemas legados, APIs de terceiros, bibliotecas com contratos diferentes.
- **Exemplo estrutural:** O sistema interno usa uma interface de pagamento própria; um Adaptador converte as chamadas para uma API externa de cartão, sem que o Controller ou o Model conheçam os detalhes externos.

### 4.6 Dependency Injection (Inversão de Controle)
- **Sigla:** DI (Dependency Injection) — padrão arquitetural complementar (não GoF, mas essencial para baixo acoplamento).
- **Definição:** Em vez de um componente criar suas dependências, ele as recebe de um container ou construtor externo, dependendo apenas de abstrações.
- **Aplicabilidade:** Quando o Controller precisa trocar implementações do Model, Strategy ou Adapter sem alterar seu código interno; base para frameworks modernos.
- **Exemplo estrutural:** O Controller recebe um `IPedidoService` via construtor; se o serviço muda de cálculo padrão para cálculo expresso, a injeção substitui a instância sem tocar no Controller, preservando coesão e eliminando acoplamento direto.

---

## ETAPA 5 — Relação Cruzada (Coesão / Acoplamento × MVC × Patterns)

| Elemento | Como preserva alta coesão | Como reduz acoplamento |
|---|---|---|
| MVC | Cada camada tem responsabilidade única | Controller não conhece detalhes internos da View; View não acessa Model diretamente |
| Singleton | Estado global coeso, sem duplicação | Acesso centralizado, sem múltiplas dependências espalhadas |
| Factory | Criação isolada, sem misturar regras de negócio | Cliente depende da fábrica abstrata, não da classe concreta |
| Observer | Notificação focada no evento, sem lógica extra | Model não conhece os observadores específicos, apenas a interface |
| Strategy | Algoritmo coeso, trocável | Contexto depende apenas da estratégia, não das implementações |
| Adapter | Conversão isolada em uma classe | Cliente e serviço externo não se conhecem diretamente |
| DI | Cada componente recebe apenas o que precisa | Nenhum componente cria suas dependências diretamente; tudo passa por abstrações |

**Meta-relação com MVC:** Os patterns atuam dentro das camadas. O Factory pode criar objetos do Model; o Strategy pode variar cálculos no Controller; o Observer conecta Model e View; o Adapter isola integrações externas; o Singleton pode gerenciar recursos compartilhados; a DI conecta Controller, Model, Strategy e Adapter via abstrações, eliminando criação direta.

---

## ETAPA 6 — Conclusão Sintética

Alta coesão e baixo acoplamento não são apenas princípios abstratos: são a razão de existir do MVC e dos design patterns clássicos. O MVC organiza a aplicação em camadas coesas; os patterns (Singleton, Factory, Observer, Strategy, Adapter, DI) resolvem problemas recorrentes dentro ou entre essas camadas, sempre com o objetivo de reduzir dependências rígidas e manter cada módulo focado em uma única responsabilidade. A meta-relação é circular: o objetivo (coerência e flexibilidade) guia a escolha dos meios (MVC + patterns), e os meios reforçam o objetivo.

---

*Artigo técnico — sem código-fonte, apenas estruturas de arquitetura e relação conceitual.*
Projeto: Estudos e Engenharia de TI
