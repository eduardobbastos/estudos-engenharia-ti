---
title: "Pragmatismo — Quando NÃO Usar o Padrão"
---

## Regra

A maturidade sênior se prova não pelo padrão usado, mas pelo padrão evitado quando não agrega valor.

- **Não use Factory** quando a criação é direta e imutável (ex: uma constante de configuração simples).
- **Não use Singleton** quando o estado pode ser injetado (DI é preferível; Singleton é acoplamento global disfarçado).
- **Não use Strategy** quando a variação é única e estática (um bloco condicional claro é mais coeso que uma árvore de classes).
- **Não use Adapter** quando o sistema externo já fala a mesma interface (adicionar uma camada de tradução sem razão aumenta acoplamento, não o reduz).
- **Não use EDA / CQRS / DDD Context** para um sistema simples com uma equipe pequena (a complexidade arquitetural deve pagar pelo benefício operacional).

## Reflexão

A simplicidade robusta vence a complexidade elegante. O artigo original mostra os mecanismos; este arquivo lembra que eles são ferramentas, não obrigações. A alta coesão exige também a coragem de não fragmentar o que é simples.
