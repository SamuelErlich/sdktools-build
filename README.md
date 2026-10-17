# SDKtools 3.20.0 / build 46 — Alpaca Turbo

Base: 3.19.9. WePlay US 6.6.2/build132. Missões continuam prioritárias; Bilhar e Cartas preservados. O experimento de trava do armazém foi retirado do menu desta versão. O usuário relatou código500 no teste anterior; não é tratado como desbloqueio nem como identificação conclusiva da causa.

## Usar

No menu **Crazy Alpaca**, há três controles independentes, inicialmente desligados:

1. **Turbo**: agenda leituras a cada40ms em vez de100ms. Exige duas observações estáveis separadas por pelo menos40ms em vez de80ms. Não acelera o relógio do jogo, não corta suas animações e não envia jogadas em lote.
2. **Planejamento maior**: compara caminhos com vários trios, até18 seleções hipotéticas. Busca em feixe de24 estados, máximo12000 expansões/24 fatias de6ms. Mantém uma rota segura do planejador anterior como fallback. Executa apenas o primeiro trio provado e replaneja a partir da mesa real.
3. **Habilitar uso de poderes**: autoriza **consumir seu estoque existente** de Reserva/Storage, Desfazer/Withdraw e Embaralhar/Refresh, somente como resgate quando não há rota segura encontrada e a bandeja tem pelo menos4 cartas. Não compra, cria ou recarrega poderes.

Ative as opções desejadas e toque **Iniciar autoplay**. Nenhuma opção inicia o jogo sozinha. As permissões não ficam ligadas após reiniciar o aplicativo. Toque manual na partida, captura e segundo plano continuam pausando o autoplay.

## Como os poderes são escolhidos

- Primeiro tenta resolver com cartas, mantendo prioridade da missão.
- **Reserva**: somente com reserva vazia e previsão de trio acessível após liberar3 espaços. Como o servidor escolhe as cartas, verifica todas as possíveis combinações de3 cartas da bandeja, não presume quais serão movidas.
- **Desfazer**: exige a última carta identificada na bandeja, origem conhecida e um trio acessível após a volta. Considera a cobertura que essa carta pode criar ao voltar para a pilha.
- **Embaralhar**: último recurso. O resultado é desconhecido antes do uso; não promete uma combinação vencedora.
- Poderes direcionados (Penetrate/Bomb), tipos desconhecidos e estoque zero não são automatizados nesta versão. Continuam disponíveis pelos controles manuais já existentes quando compatíveis.
- No máximo um poder confirmado entre jogadas normais confirmadas: não gasta o inventário em uma sequência de tentativas de resgate sem progresso.

Abre a janela original e confirma em outra leitura, validando novamente identidade/tipo/estoque/contexto. Exige diminuição exata de1 no estoque e efeito correspondente, estável, na mesa. Uma solicitação não é contabilizada como carta jogada nem como efeito confirmado.

## Se parar aguardando um poder

Não há reenvio automático após erro, exceção ou timeout. Desabilitar poderes ou pausar impede nova confirmação, mas não desfaz um pedido já enviado. Se a página mudar com poder pendente, o autoplay fica bloqueado até conferir a partida e reiniciar o aplicativo; uma nova página não herda o latch JavaScript anterior.

Exporte o relatório normal e procure `autoplay.powers`, `autoplay.planning`, `autoplay.reading` e `autoplay.events`. Somente contadores, tipos numéricos e motivos enumerados são exportados; IDs de cartas, sala, usuário e poderes ficam apenas em memória.

## Compilar

`SDKtools_Fontes.zip` e `compilar.yml` formam um par por SHA-256 e tamanho. GitHub Actions **Compilar SDKtools US**, `base_source=release`, `release_tag=base-us-6.6.2`.

Saída: `WePlay_US_6.6.2_SDKtools_v3_20_0_unsigned.ipa`. **Requer assinatura para instalar.**

Os testes usam cenas/servidor simulados e capturas históricas. Compilação/linkagem Apple e integração no IPA são verificações separadas. Não há iPhone conectado nesta estação: velocidade, compatibilidade dos controles vivos e aceitação dos poderes ainda precisam de validação no aparelho. Não há garantia de vitória ou jogada perfeita.
