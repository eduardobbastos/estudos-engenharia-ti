# Estudos de Engenharia de TI — Arquitetura de Software

> Ecossistema de documentos técnicos para avaliação, planejamento e operação segura de projetos de software,
> sob as perspectivas de **Engenharia de Software (SE)**, **DevOps/DevSecOps** e **Full Stack (FS)**.

---

## Estrutura do Repositório

| Documento | Papel no Ecossistema | O que contém |
|---|---|---|
| [`SKILL.md`](./SKILL.md) | **Referência arquitetural e avaliação** | Artigo técnico completo (ETAPAS 1–18): HC/BA, MVC, GoF, DI, MVVM, Clean/Hex, EDA, CQRS, DDD, Observabilidade, Pragmatismo. Pseudo-algoritmo de avaliação, personas de agentes (Agente-SE/DevOps/Sec/Prag), modelo de relatório e tabela de risco de segurança. |
| [`PLANNING_FRAMEWORK.md`](./PLANNING_FRAMEWORK.md) | **Planejamento e organização dinâmica de projetos** | Taxonomia de 5 tipos de projeto (MVP, Scale-up, Legado, Microserviços, Dados). FASE 0 a FASE 4: leitura de natureza, planejamento em 3 horizontes, template de tarefa coesa, organização dinâmica por tipo, revisão contínua com gatilhos e matriz de responsabilidade por perfil. |
| [`PRINCIPIOS_SEGURANCA.md`](./PRINCIPIOS_SEGURANCA.md) | **Segurança da informação** | 10 princípios fundamentais de SE e DevSecOps: prevenção de injeção de código (SQLi, XSS, Command Injection), secrets management, supply chain security, observabilidade de segurança, shift-left, zero trust e modelagem de ameaças. Cada princípio correlacionado às ETAPAs do SKILL.md. |
| `README.md` | **Índice e mapa do ecossistema** | Este arquivo. |

---

## Como o Ecossistema Funciona

Os três documentos são complementares e se referenciam mutuamente:

```
PLANNING_FRAMEWORK.md          SKILL.md                  PRINCIPIOS_SEGURANCA.md
─────────────────────          ────────────────────────   ──────────────────────────
FASE 0 — Natureza          →   ETAPA 2 (Meta-Relação)    Princípios por Tipo
FASE 1 — Planejamento      →   ETAPAS 1 a 18 (Artigo)    Princípios 1-10 (postura)
FASE 2 — Tarefas           →   PARTE II (Pseudo-algo)     Princípios no DoD
FASE 3 — Organização       →   PARTE V (Tabela de Risco)  Princípios por sprint
FASE 4 — Revisão Contínua  →   PARTE IV/VI (Relatório)    Modelagem de ameaças
```

---

## Perfis e Papéis

| Perfil | Foco Principal | Documentos Primários |
|---|---|---|
| **Full Stack (FS)** | Features de ponta a ponta; UI + API + DB | SKILL.md (ETAPAS 3, 10); PLANNING_FRAMEWORK.md (FASE 2) |
| **Engenheiro de Software (SE)** | Arquitetura, coesão, padrões, domínio, segurança em código | SKILL.md (ETAPAS 1–18); PRINCIPIOS_SEGURANCA.md |
| **DevOps / SRE** | Esteira CI/CD, observabilidade, infraestrutura, resiliência | SKILL.md (ETAPA 15, PARTE II Passo 8); PLANNING_FRAMEWORK.md (FASE 4) |

---

## Referência direta

- Arquitetura + Avaliação: https://github.com/eduardobbastos/estudos-engenharia-ti/blob/main/SKILL.md
- Planejamento dinâmico: https://github.com/eduardobbastos/estudos-engenharia-ti/blob/main/PLANNING_FRAMEWORK.md
- Segurança: https://github.com/eduardobbastos/estudos-engenharia-ti/blob/main/PRINCIPIOS_SEGURANCA.md
