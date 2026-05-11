# 🔮 Gerador Sarah Kali — Banho

## O que é

Um painel HTML simples onde admins criam, revisam e enviam banhos personalizados pros clientes ANTES de mandar via ManyChat.

## Como funciona

```
1. Cliente preenche flow no ManyChat
   ↓
2. ManyChat manda OBSERVAÇÃO INTERNA pro admin (link único):
   https://gerador.sarahkali.com.br/?subscriber_id=954238352&nome=Mariane&intencao=amor&problema=ficar%20irresistivel
   ↓
3. Admin clica no link → abre o gerador JÁ com dados preenchidos
   ↓
4. Admin clica "Gerar Prévia do Banho" → AI gera texto
   ↓
5. Admin LÊ o texto na tela
   ↓
6a. SE TÁ BOM → clica "Enviar pro Cliente" → PDF + mensagem vai pro WhatsApp
6b. SE TÁ RUIM → clica "Regenerar" (ou edita os dados e regenera)
```

## Hospedagem no Easypanel

### Passo 1 — Subir os arquivos
1. Cria um repositório no GitHub (público ou privado) com os 2 arquivos:
   - `index.html`
   - `Dockerfile`

### Passo 2 — Criar serviço no Easypanel
1. Acessa seu Easypanel
2. Clica em **"+ Service"** → **"App"**
3. Nome do serviço: `gerador-sarah`
4. **Source:** GitHub (escolhe o repo que você criou)
5. **Build:** Dockerfile (deixa como tá)
6. **Port:** 80
7. **Domain:** configure um subdomínio tipo `gerador.sarahkalitarot.com.br`
8. Clica em **Deploy**

Pronto, o gerador tá no ar.

### Passo 3 — Testar
Acessa o domínio. Deve aparecer o painel.

## Próximos passos no n8n

Pra esse gerador funcionar, você precisa de **2 webhooks no n8n** que ainda preciso criar:

1. **`banho-sarah-kali-gerar-texto`** — recebe POST do gerador, roda AI, devolve texto pra mostrar na prévia (Workflow A — já criei na entrega anterior)

2. **`banho-sarah-kali-aprovar`** — recebe POST do gerador (incluindo o texto aprovado), gera PDF, manda pro cliente via ManyChat (Workflow B — preciso ajustar pra receber texto via payload em vez de buscar do ManyChat)

## Próximo passo no ManyChat

No final do flow `Banho - Coleta`, depois das 3 perguntas, adicionar uma **Solicitação Externa** que monta a URL e manda como OBSERVAÇÃO INTERNA pra você ver na Caixa de Entrada.

URL exemplo a montar (no flow ManyChat):
```
https://gerador.sarahkalitarot.com.br/?subscriber_id={{user_id}}&nome={{banho_nome}}&intencao={{banho_intencao}}&problema={{banho_problema}}
```

## Como adicionar OUTROS produtos (depois do Banho funcionar)

Quando você quiser adicionar Simpatia, Mapa Astral, etc:

**Opção A — Página separada por produto:**
- `index.html` continua sendo Banho
- `simpatia.html` é o gerador de Simpatia
- `mapa.html` é o gerador de Mapa Astral

**Opção B — Página única com seletor de produto:**
- Logo no topo, dropdown "Qual produto?"
- Os campos mudam conforme o produto escolhido
- 1 URL pra tudo

Me fala qual você prefere quando chegar a hora.
