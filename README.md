# SDKtools 3.19.9 / build 45 — Teste experimental da trava do armazém

Base: 3.19.8 (prioridade de missão preservada). WePlay US 6.6.2/build132. Cartas e Bilhar preservados. **Esta versão testa uma hipótese; não oferece desbloqueio permanente nem uso ilimitado.**

## Usar no iPhone

1. Assine/instale o IPA. Entre no Crazy Alpaca **em time**, antes de iniciar o autoplay. Espere qualquer jogada pendente terminar.
2. Deixe seu próprio slot **vazio e bloqueado**. No menu Alpaca, toque **Testar trava (1 tentativa)**.
3. O SDK escreve zero temporariamente no campo local de trava, executa a abertura original e restaura a trava antes de devolver o controle. Se o seletor abriu, **escolha UMA carta**. Essa escolha pode colocar uma carta real no armazém e alterar sua partida.
4. Reabra o menu e toque **Ver resultado do teste**. Repita apenas essa consulta se a resposta/movimentação ainda não chegou; ela não reenvia o pedido.
5. Exporte o relatório normal do SDKtools e envie o JSON. O resultado fica em `warehouseLockTest.diagnostic` e nos últimos16registros de `warehouseLockTest.events`.

O botão **Meu armazém** normal continua exigindo slot livre/destravado. O botão experimental é separado. O autoplay é pausado e não é retomado automaticamente. Encerre o teste pelo botão próprio; no resultado incerto de um pedido enviado, não há liberação para nova tentativa automática. Para outro teste independente, reinicie o aplicativo.

## Como interpretar

- `armed`: seletor original aberto; o teste ainda não observou pedido de colocação.
- `submitted`: foi observado o envelope original de uma escolha manual, sem alterar bytes/argumentos.
- `accepted`, `serverCode=200`: resposta de protocolo correspondente ao pedido observado. **Não prova por si só mudança do slot.**
- `slotEffectConfirmed=true`: além do200, a mesma carta apareceu no próprio slot, observada coerentemente no Store/componente. **Ainda não prova desbloqueio após retirar essa carta nem uso ilimitado.**
- `rejected`: o servidor devolveu um código diferente de200. Isso não identifica sozinho a causa da recusa.
- `uncertain`: envio/retorno/restauração não comprovados. Não repetir o pedido; confira ou reabra a partida.
- `expired`: expirou a seleção sem pedido observado.

O lease de seleção é30s; após pedido observado,15s para resposta. Não há envio automático, pacote fabricado, chamada de debug, alteração de saldo/poderes, repetição do pedido ou mudança no slot de outro jogador. O usuário ainda pode fazer ações normais no jogo; elas não são automaticamente atribuídas ao teste.

## O que é escrito e restaurado

Somente o descritor de dados de `commonBlock.lock_state` do próprio slot vazio é sobrescrito durante a chamada de abertura. Não são zeradas travas de cartas especiais. A restauração atua no objeto original, sem substituir um objeto novo recebido. Falhas de restauração são reportadas como incertas, nunca como sucesso.

Os observadores são temporários na instância de Socket, não no protótipo global. A escolha e o send originais preservam this/argumentos/retorno/exceções/Promise. A inspeção lê somente o cabeçalho da resposta correlacionada; corpos, UID/rid, segredo, IDs de carta e de pacote não são exportados. Eventos sintéticos de página não são aceitos como retorno de rede.

## Compilar e limites

ZIP `SDKtools_Fontes.zip` e workflow `compilar.yml` são um par por SHA-256/tamanho. Workflow Compilar SDKtools US, `base_source=release`, `release_tag=base-us-6.6.2`. Saída: `WePlay_US_6.6.2_SDKtools_v3_19_9_unsigned.ipa`. Requer assinatura.

O coletor foi preparado em Windows. Não há iPhone conectado nesta sessão. Testes com mocks e build iOS, quando aprovados, não comprovam aceitação real pelo servidor. Nenhuma tentativa real foi enviada por esta estação.
