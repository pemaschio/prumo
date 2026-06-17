# Prumo - MVP (SaaS demo investidor)

Demo funcional da plataforma de compra inteligente para obra, no ar em **https://prumo.mondo-ia.com.br**.

## O que e
App de 3 telas para demonstrar o produto rodando aos investidores:
- **Agente** - o usuario descreve a demanda em uma frase e o agente de IA monta a lista de compra real (produto, marca, quantidade dimensionada por rendimento + folga, preco e cashback). Cada lista pode ser enviada no WhatsApp ou exportada em PDF.
- **Minha obra** - painel que acumula cashback, GMV de material e historico de listas.
- **Ofertas** - feed de produtos em destaque, estilo WhatsApp.

## Arquitetura
- SPA em arquivo unico (`prumo.html`), servido por um Cloudflare Worker (`prumo-mondo-ia`) a partir do Supabase Storage (`docs/prumo.html`).
- `POST /api/agent` chama a Claude API (haiku-4.5) com structured output. Chave protegida como secret no Worker.
- Fallback local por palavra-chave para a demo nunca quebrar offline.

## Deploy
O arquivo `prumo.html` e a fonte de verdade. Publicar via upsert no Supabase Storage `docs/prumo.html`; o Worker serve com cache zero, entao a atualizacao reflete na hora.
