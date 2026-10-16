# SDKtools US 3.17.1 — Cartas

Revisão sobre SDKtools 3.17/build33, para WePlay US 6.6.2/build132. **Bilhar fica intacto**, incluindo recursos Lua, runtime, validações e testes. O núcleo do Alpaca também foi preservado.

## Compilar
Executar **Compilar SDKtools US** nesta branch, com `base_source=release` e `release_tag=base-us-6.6.2`. ZIP e workflow são um par verificado por hash e manifesto antes de executar fontes.

O resultado é um IPA **sem assinatura**, disponível no artefato do Actions. Releases automáticas ficam restritas à main.

## Cartas
- No lobby, armar **Capturar Cartas desde a entrada**, entrar em Ah, minha carta e jogar por 90 s.
- O menu mostra um histórico limitado de **cores recebidas**, sem inferir cartas desconhecidas. Depois do encerramento, exportar a captura.
- **Ativar marcadores de cores** é um modo separado, para a cena atual. Não altera as cartas originais.
- **Exportar JS baixado do jogo** prepara os arquivos já disponíveis no documento local; não faz download adicional.

O hook BOOL de loadCurrentGame preserva o retorno original. O analisador também aceita o booleano numérico legado da captura V3.12. As alterações são revisáveis em `patches/3.17.1.diff`. A assinatura e a confirmação no aparelho continuam etapas separadas.
