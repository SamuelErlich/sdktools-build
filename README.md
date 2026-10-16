# SDKtools3.19.7/build43 — Inject e amostragem direta para o menu

Base: SDKtools3.19.6, WePlayUS6.6.2/build132. Alpaca/Bilhar sem mudança funcional.

## Método novo

O menu deixa de depender de encontrar/desenhar Card nodes: lê `GameStore.gamers[].cards` diretamente e injeta3observadores temporários: `GameStore.sync`, `GameStore.updatePushMessage` e `Card.setup`. Copia valores permitidos antes da chamada original e só os conserva após a chamada terminar com sucesso. Observações Card.setup exigem componente e mão atuais coerentes. Retorno/exceção/this/argumentos do original preservados, sem repetir chamadas.

Isso captura exposições transitórias que desapareçam entre duas leituras de150ms. O sampler também lê localmente `select_give_card` e `look_over_cards` já recebidos. **Nunca chama `Socket.sync`, send, compra ou habilidade de revelação.** Forçar amostragem é forçar uma leitura local, não uma resposta diferente do servidor.

## Usar no aparelho

1. Abra Ah,minha carta. No menu SDKtools, toque **Injetar / amostrar agora no menu**, antes das compras ou da próxima rodada. Também é instalado junto com os marcadores.
2. Abra o menu e confira **Inject:3/3hooks**. `sync/setup` devem subir quando o próprio jogo executar esses métodos. `leituras` é atividade do sampler, não quantidade de cartas.
3. Cada linha mostra `Você` (quando identificável) ou `M1...`: total atual e distribuição `R/Az/Am/V/E/?`. R=rosa/vermelho do jogo; E=especial; ?=não recebida. M é índice do Store, não posição física da mesa.
4. O botão solicita uma leitura imediatamente; o timer mantém leitura periódica. Não ative captura early simultaneamente: são fluxos separados e ela encerra os marcadores/injeção.
5. Use **Exportar captura de Cartas** com o modo ativo. Conferir `samplerStatus`, `samplerHooks`, `samplerSyncs`, `samplerSetups`, `samplerHiddenKnown`, `handCounts`. `samplerRetained/Observed` também incluem faces já abertas; não são contagem de novas cores ocultas.

Se houver `sampler_only`, os dados continuam no menu mesmo sem layout reconhecido ou dentro do orçamento visual. Marcadores e etiquetas são opcionais; o censo não depende deles. Anel branco marca uma face ligada ao estado direto/observação validada.

## Limites

Os observadores não ressuscitam eventos anteriores à ativação. Não existe fórmula de ID→cor. Fatos são limitados à rodada/conexão/dono,120s,256entradas, com descarte em transferência/remoção/conflito. Lease600ms e limpeza restauram os métodos.

Se o servidor só envia Back0 e nenhuma etapa local contém a face verdadeira, `?` continua correto. Os novos testes provam captura de valores transitórios SIMULADOS; não provam que esta versão do WePlay revele todos eles. A captura885A anterior permanece sem novas cores de oponentes no replay dos41estados gravados.

## Compilar

Parear SDKtools_Fontes.zip e .github/workflows/compilar.yml. Workflow Compilar SDKtoolsUS, base_source=release, release_tag=base-us-6.6.2. Produto `WePlay_US_6.6.2_SDKtools_v3_19_7_unsigned.ipa`, requer assinatura. Validação visual no iPhone ainda pendente.
