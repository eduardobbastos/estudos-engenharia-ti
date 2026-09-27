# PLANO — Complemento: Relação entre MVC/GoF/DI e os 5 Padrões Modernos

ANÁLISE: O artigo original foca MVC (apresentação) + GoF (mecanismos internos: Singleton, Factory, Observer, Strategy, Adapter, DI). Os 5 modernos operam em camadas superiores ou paralelas:
- MVVM: evolução do Controller para frontend reativo (substitui a coordenação MVC no cliente).
- Clean/Hexagonal: evolução do isolamento do Model; o domínio fica no centro como uma camada coesa, independente de framework.
- EDA: evolução do Observer para comunicação distribuída (não apenas dentro do processo).
- CQRS: evolução do Model, separando leitura/escrita quando o acoplamento de uma única estrutura de dados limita a escala.
- DDD Bounded Context: evolução da coesão do Model, definindo fronteiras explícitas para evitar que o domínio cresça sem controle.

META-RELAÇÃO COMPLEMENTAR: MVC + GoF + DI são mecanismos internos; MVVM + Clean + EDA + CQRS + DDD são estratégias arquiteturais que usam esses mecanismos para escalar. Nenhum substitui o outro — operam juntos.

TAREFAS:
1. Escrever introdução complementar (relação, não substituição)
2. Descrever cada um dos 5 modernos (sigla, definição, aplicabilidade, exemplo estrutural)
3. Tabela cruzada: como cada moderno se relaciona com MVC e com os padrões originais
4. Conclusão complementar

EXECUÇÃO: arquivo `complemento_moderno.md` no projeto.
