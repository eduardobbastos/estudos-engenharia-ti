---
title: "Observabilidade Nativa — Do Código para Produção"
---

## Princípio

Observabilidade não é anexo — nasce com a arquitetura. Três pilares:

- **Logs estruturados:** cada evento (confirmação de pedido, falha de adapter, troca de strategy) deve produzir uma entrada com contexto (request_id, contexto, timestamp).
- **Métricas:** coesão e acoplamento são medidos indiretamente — tempo de resposta por adapter, taxa de erro por strategy, latência por contexto DDD.
- **Tracing distribuído:** quando EDA publica `PedidoConfirmado`, o trace deve seguir do produtor ao consumidor (Estoque, Notificação, Financeiro), sem que os serviços se conheçam.

## Aplicação ao artigo

- Cada adapter (Clean/Hex) deve expor uma métrica de saúde.
- Cada evento (EDA) deve carregar um trace_id.
- Cada estratégia (Strategy) deve registrar o tempo de execução.
- Nenhuma camada (MVC, MVVM, CQRS) deve ocultar o que está acontecendo — a coesão do código não justifica a opacidade da operação.
