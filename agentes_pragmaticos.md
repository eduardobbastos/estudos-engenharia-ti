---
name: abordagem-pragmatica-agentes
version: 1.0
description: Planejamento sequencial com personas de agentes para conferência cruzada das tarefas e conclusões da skill analista-arquitetura-codigo. Referência: SKILL.md e ARTIGO_COMPLETO.md (https://github.com/eduardobbastos/estudos-engenharia-ti)
---

## Vale estabelecer personas? Sim.

Sem personas, agentes repetem conclusões; com personas, há conferência cruzada. Abaixo, a sequência pragmática.

---

## Personas dos Agentes

| Persona | Nome | Função | O que confere |
|---|---|---|---|
| Analista SE | Demerzel-SE | Avalia coesão, acoplamento, arquitetura, patterns | Se o código segue MVC, Clean, EDA, CQRS, DDD conforme artigo |
| Analista DevOps | Demerzel-DevOps | Avalia observabilidade, CI/CD, deploy, risco operacional | Se há tracing, métricas, automação, rollback seguro |
| Auditor de Segurança | Demerzel-Sec | Avalia classificação de risco, impacto de segurança | Se a tabela de risco está completa e precisa |
| Revisor Pragmático | Demerzel-Prag | Confere se há over-engineering, se padrões são necessários | Se cada padrão usado agrega valor real ao contexto |

---

## Sequência Pragmática das Tarefas (Conferência Cruzada)

PASSO 1 — Analista SE executa SKILL.md (PASSO 1-4): inventário, coesão/acoplamento, arquitetura, padrões.
PASSO 2 — Analista DevOps executa SKILL.md (PASSO 5): observabilidade, CI/CD, infraestrutura.
PASSO 3 — Auditor Sec executa SKILL.md (PASSO 4 e tabela): classifica gravidade de risco; confere se cada evidência está citada.
PASSO 4 — Revisor Pragmático confere PASSO 4: cada padrão está justificado? Há over-engineering?
PASSO 5 — Todos consolidam conclusões no relatório (texto corrido 3 parágrafos); se houver divergência, o Revisor decide com base no artigo de referência.
PASSO 6 — Continuidade: o relatório é atualizado a cada commit; os agentes reexecutam a sequência.

---

## Meta-Relação

A abordagem pragmática não substitui a skill — ela a opera. Os agentes são os executores; a skill é o contrato; o artigo é a referência. A conferência cruzada garante que nenhuma conclusão seja aceita sem verificação de outra perspectiva (SE, DevOps, Segurança, Pragmática). O endereço do artigo de referência está incluído na descrição da skill e neste arquivo, garantindo que todo agente tenha o contexto completo.
