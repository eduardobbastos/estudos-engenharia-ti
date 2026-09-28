# Estudos de Engenharia de TI — Arquitetura de Software

> Ecossistema de documentos técnicos para avaliação, planejamento e operação segura de projetos de software,
> sob as perspectivas de **Engenharia de Software (SE)**, **DevOps/DevSecOps** e **Full Stack (FS)**.

---

## Estrutura do Repositório

| Documento | Papel no Ecossistema | O que contém |
|---|---|---|
| [`SKILL.md`](./SKILL.md) | **Referência arquitetural e avaliação** | Artigo técnico completo (ETAPAS 1–19): HC/BA, MVC, GoF, DI, MVVM, Clean/Hex, EDA, CQRS, DDD, Observabilidade, Pragmatismo e QA Estático (Dead Code & Duplicação). Pseudo-algoritmo de avaliação (Passos 1 a 8 + 2.1), personas de agentes (Agente-SE/DevOps/Sec/Prag), modelo de relatório e tabela de risco. |
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
FASE 1 — Planejamento      →   ETAPAS 1 a 19 (Artigo)    Princípios 1-10 (postura)
FASE 2 — Tarefas           →   PARTE II (Passos 1-2.1)    Princípios no DoD (DoD QA)
FASE 3 — Organização       →   PARTE V (Tabela de Risco)  Princípios por sprint
FASE 4 — Revisão Contínua  →   PARTE IV/VI (Relatório)    Modelagem de ameaças
```

---

## Perfis e Papéis

| Perfil | Foco Principal | Documentos Primários |
|---|---|---|
| **Full Stack (FS)** | Features de ponta a ponta; UI + API + DB | SKILL.md (ETAPAS 3, 10); PLANNING_FRAMEWORK.md (FASE 2) |
| **Engenheiro de Software (SE)** | Arquitetura, coesão, padrões, domínio, segurança em código e QA | SKILL.md (ETAPAS 1–19); PRINCIPIOS_SEGURANCA.md |
| **DevOps / SRE** | Esteira CI/CD, observabilidade, infraestrutura, resiliência | SKILL.md (ETAPA 15, PARTE II Passo 8); PLANNING_FRAMEWORK.md (FASE 4) |

---

## Referência direta



---

## NOTA — Referência Visual (PRD: MD)

O arquivo de vídeo enviado (`video_6f930a6cc091.mp4`) contém uma referência visual com a marcação **"PRD: MD"**. No contexto deste projeto, isso indica que o documento consolidado (`README.md`) opera simultaneamente como:

- **PRD (Product Requirements Document)** — define os requisitos arquiteturais, padrões, observabilidade e segurança exigidos para sistemas de alta coesão e baixo acoplamento.
- **MD (Markdown/Documento técnico)** — entrega o conteúdo estruturado, com siglas, exemplos, impactos e visões SE/DevOps.

A referência visual confirma que este estudo não é apenas teórico: é um documento operacional, utilizável por agentes de IA e equipes de desenvolvimento para avaliar, planejar e executar arquitetura de software com critérios verificáveis.

---
*Nota adicionada com base na referência visual do vídeo — sem alteração no corpo técnico do artigo.*
