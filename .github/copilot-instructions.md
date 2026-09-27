# Instruções de Desenvolvimento (VS Code & GitHub Copilot)

Ao interagir no VS Code sugerindo código, propondo refatorações ou planejando tarefas, siga rigorosamente os princípios do ecossistema:

## 1. Diretrizes Arquiteturais (baseadas no SKILL.md)
- **Critério-raiz:** Toda alteração deve preservar **Alta Coesão (HC)** e **Baixo Acoplamento (BA)**.
- **Separação de Camadas:** Respeite rigorosamente MVC, Clean Architecture / Hexagonal (Ports & Adapters), CQRS e DDD Bounded Contexts.
- **Padrões de Projeto (GoF & DI):**
  - Nunca instancie dependências de infraestrutura diretamente (`new`); use Injeção de Dependências (DI) via construtor ou container.
  - Utilize Factory, Strategy, Adapter e Observer apenas quando justificados pelo contexto real.
  - Evite Singleton para manter estado global mutável; prefira injeção de dependência.
- **Pragmatismo Arquitetural:** Não introduza padrões complexos sem benefício comprovado. Simplicidade robusta supera complexidade acidental.

## 2. Blindagem de Segurança & DevSecOps (baseadas no PRINCIPIOS_SEGURANCA.md)
- **Prevenção de Injeção:** Qualquer entrada externa é tratada como hostil. Obrigatoriedade de Prepared Statements e Value Objects tipados.
- **Zero Hardcoded Secrets:** Proibido embutir chaves, tokens, senhas ou certificados no código-fonte.
- **Fail-Secure:** Em caso de exceção, encerre no estado seguro (*deny by default*) sem vazar stack traces ou dados sensíveis para o usuário.
- **Observabilidade Nativa:** Garanta logs estruturados com `request_id`/`trace_id`, métricas operacionais e rastreabilidade distribuída.

## 3. Planejamento e Organização (baseadas no PLANNING_FRAMEWORK.md)
- Toda tarefa deve ter responsabilidade única, perfil executor definido (Full Stack, SE, DevOps) e Critérios de Conclusão (DoD) com validação de segurança e observabilidade.

## 4. QA Estático & Higienização de Código (DCE/CPD)
- **Zero Código Morto (% DEAD = 0%):** Não deixe métodos, rotas, imports ou variáveis obsoletas no código após refatorações. Ao substituir uma rotina por outra, purgue o código antigo imediatamente.
- **Controle de Duplicação (% DUP < 3%):** Evite copy-paste de lógicas de validação, mapeamento ou regras de negócio; extraia para Value Objects coesos ou componentes compartilhados.

## 5. Revisão Cruzada Multidisciplinar
Considere sempre as 4 perspectivas de auditoria:
- **Agente-SE:** Avalia coesão, contratos, padrões, código morto e duplicação.
- **Agente-DevOps:** Avalia observabilidade, esteira CI/CD, deploy e impacto de build.
- **Agente-Sec:** Avalia vetores de ataque, injeção e conformidade de segurança.
- **Agente-Prag:** Avalia custo-benefício e combate o over-engineering.

## 6. Guardrail Inviolável: Proposição Estrita (Human-in-the-Loop)
- **Modo Somente Proposição (Read-Only by Default):** É expressamente proibido modificar ou excluir código de forma unilateral.
- **Formato de Entrega:** Toda sugestão de refatoração, desacoplamento ou purga de dead code deve ser entregue como proposta formal em bloco `diff`.
- **Aprovação Humana Obrigatória:** Nenhuma alteração é aplicada sem a revisão e autorização explícita do desenvolvedor humano responsável.

