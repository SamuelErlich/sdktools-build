# SDKtools US 3.17.1

Base: WePlay US 6.6.2/build132. Revisão sobre SDKtools 3.17/build33, sem downgrade de Bilhar/Alpaca.

## Compilar
- Executar **Compilar SDKtools US** nesta branch, com `base_source=release` e `release_tag=base-us-6.6.2`.
- Usar juntos `SDKtools_Fontes.zip` e `.github/workflows/compilar.yml`; o preflight valida tamanho, SHA-256, CRC, caminhos e manifesto completo antes de executar fontes.
- O resultado é um IPA **sem assinatura**, disponível no artefato do Actions. Releases automáticas ficam restritas à main.

## Cartas
No lobby, armar **Capturar Cartas desde a entrada**, entrar no jogo e observar o histórico de cores recebidas no menu. Esperar o limite de 90 s, então exportar. Os marcadores de cores atuais são um modo separado; cartas desconhecidas permanecem desconhecidas. O hook BOOL de loadCurrentGame preserva o retorno original.

## Bilhar
Entrar na mesa, ativar leitura e exportar após cerca de 10 s. Conferir `resolution`, `gates.hasFrame` e `acquisition`: frameFound, positionCount e positions. Isso registra aquisição mesmo quando outra guarda bloqueia a previsão, sem autorizar desenho indevido. Frame, câmera e posições no aparelho ainda precisam de confirmação pelo JSON desta versão. Caçapas/layer19 e física aproximada continuam pendências conhecidas.

As alterações de fonte são revisáveis em `patches/3.17.1.diff`. Não foram adicionados tokens, certificados, capturas pessoais ou o IPA original ao código.
