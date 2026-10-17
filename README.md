# SDKtools 3.19.8 / build 44 — Autoplay: missão primeiro

Base: 3.19.7; WePlay US 6.6.2/build 132. Mudança funcional apenas no Alpaca. Recursos de Cartas e Bilhar preservados.

## O que mudou

- Identifica a missão pelo `GameStore.task_info`: `target_block_type`, `current_num`, `total_num`, com vínculo verificado ao Game/Task da cena atual.
- Prefere um **trio do tipo da missão**, mesmo havendo um par normal pronto. Também procura rotas que liberem o tipo-alvo por cartas bloqueadoras.
- Prioridade não significa clique arbitrário: toda rota precisa terminar em um trio, respeitar máscara/travas e caber nos sete slots. Não passa por cima das regras do jogo.
- Sem missão válida, com missão já concluída ou sem rota-alvo comprovada no limite de busca, usa o autoplay normal. Se a busca prioritária não tiver encontrado nem um trio normal, o algoritmo original ganha seu próprio orçamento de busca.
- Reavalia quando missão/progresso muda e a cada trio concluído. Uma mudança cancela ação preparada, mas **não reenvia** ação já enviada e ainda incerta.
- Menu/relatório distinguem missão identificada, prioridade, fallback normal e objetivo atingido. Progresso é o valor lido do jogo, não uma contagem inventada pelo SDK.

## Recompensas e poderes

O próprio jogo entrega recompensas pelo evento `UpdateCommonTask` (`reward_prop`) e atualiza o inventário. O autoplay não falsifica progresso, não reivindica recompensas por requisição própria, não compra e não gasta poderes automaticamente. Apenas prioriza jogadas normais para avançar a missão. O servidor continua sendo a autoridade.

A animação pode manter a missão antiga na tela enquanto o Store já contém a nova: a leitura usa o Store, não o texto/ícone animado. Janelas de recompensa continuam pausando ações conforme as guardas existentes.

## Usar e conferir no iPhone

1. Entre no Crazy Alpaca e inicie o autoplay pelo botão já existente.
2. Com missão disponível, confira **missão primeiro X/Y** no status. O tipo é ligado ao `Block.blockInfo.type`, não adivinhado pelo desenho.
3. Se não houver caminho-alvo, confira **missão sem rota: modo normal**. A busca é limitada; essa frase não prova impossibilidade global.
4. Após um trio, confira a missão/progresso do próprio jogo e o recebimento da recompensa. Não foi feita validação física dessa versão no iPhone.
5. Em uma captura SDKtools, consulte `autoplay.planning.mission`/diagnóstico de planejamento: `status`, `targetType`, `current`, `total`. Não há IDs de jogador ou conteúdo arbitrário nessa telemetria.

## Limites da validação

Contrato recuperado de uma exportação histórica do Alpaca, com hashes verificados; identidade byte a byte do módulo atualmente carregado no iPhone ainda não foi demonstrada. Testes locais cobrem estratégia, bloqueadores, fallback, troca de missão, ação pendente e alertas; um oráculo independente enumera 120 tabuleiros sintéticos pequenos. Isso não garante vitória ou recompensa em todos os modos.

## Compilar

O ZIP `SDKtools_Fontes.zip` e o workflow `compilar.yml` desta entrega formam um par por tamanho/SHA-256. Use o workflow **Compilar SDKtools US**, `base_source=release`, `release_tag=base-us-6.6.2`. Produto: `WePlay_US_6.6.2_SDKtools_v3_19_8_unsigned.ipa`; requer assinatura e teste no aparelho.

## Cartas preservado da 3.19.7



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

## Fluxo anterior (histórico)

Parear SDKtools_Fontes.zip e .github/workflows/compilar.yml. Workflow Compilar SDKtoolsUS, base_source=release, release_tag=base-us-6.6.2. Produto `WePlay_US_6.6.2_SDKtools_v3_19_8_unsigned.ipa`, requer assinatura. Validação visual no iPhone ainda pendente.
