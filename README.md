# SDKtools V3.19.6 US — contagem atual de Cartas

WePlay US 6.6.2/build132. SDKtools 3.19.6/build42, baseado na V3.19.5.

## Correção

- Cada mão recebe etiqueta `N cartas · ?U`: N é o tamanho atual de `gamers[].cards`; U é a quantidade cuja face não foi recebida/confirmada. A etiqueta só aparece quando há vínculo atual de dono e espaço; o menu/relatório conservam os totais mesmo sem espaço para etiqueta.
- Círculos e X continuam **marcadores parciais**, limitados por sobreposição e geometria. Não representam a quantidade da mão. Descarte e compra fora da mão não entram no total.
- O menu diferencia total atual, faces confirmadas (incluindo especiais) e desconhecidas. O relatório exporta por slot `handCounts` e totais; slots não são posições físicas da tela.
- Captura inicial/histórico de renderização e marcadores são ferramentas separadas. Os 35 argumentos vistos no relatório antigo não são 35 cartas atuais.

## Limite comprovado das cores

`select_give_card` não revela toda mão oculta. No relatório 885A, só expôs uma compra vermelho/4 que foi descartada sem entrar numa mão. Portanto não acrescentou cor persistente a nenhum oponente. A V3.19.6 não inventa essas cores nem promete recuperá-las. O mecanismo passivo anterior é preservado, com escopo por rodada/conexão/dono.

## Validar no aparelho

1. Entre numa rodada e ative **Marcadores de cores** antes das compras. Não arme **Capturar Cartas desde a entrada** simultaneamente.
2. Compare o N da etiqueta com a mão atual; `?U` não é erro: indica faces desconhecidas. O número grande sobre o avatar é o cronômetro do próprio jogo, não contagem de cartas.
3. Com os marcadores ativos, use **Exportar captura de Cartas** (agora disponível também nesse modo). Não comece uma captura inicial para diagnosticar marcadores: ela os desativa.
4. Confira `cardHints.events`, `handsStatus=ready`, `handCounts`, `handTotal/handKnown/handUnknown` e `selected*`. Se `handsStatus=unavailable`, não interpretar zeros como total real.

## Compilar

Atualizar juntos `SDKtools_Fontes.zip` e `.github/workflows/compilar.yml`; executar **Compilar SDKtools US** no branch/commit correto com `base_source=release`, `release_tag=base-us-6.6.2`.
Produto: `WePlay_US_6.6.2_SDKtools_v3_19_6_unsigned.ipa`, sem assinatura.

Alpaca e Bilhar não receberam mudança funcional. Compilação e testes simulados não substituem validação das etiquetas no iPhone. Consulte `Analysis/V3_19_6-counts.md` e `Validation/V3_19_6-validation.json`.
