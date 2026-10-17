# SDK Client 3.23.0 — build 50

Base oficial: main `634e9734c39d1e5ed79b115ae75b0ceba5874332`, SDKtools 3.22.1/build 49. Esta versão atende ao feedback sobre o menu grande, texto cortado e tarjas sobre a partida.

O popup UIKit tem até **288 × 380 pt**, com altura ajustada ao conteúdo e à área segura. Exibe uma aba por vez: Alpaca, Cartas ou Bilhar. A aba do jogo identificado recebe destaque laranja; as outras ficam escurecidas e seus comandos permanecem bloqueados. Consultar uma aba não muda a identidade do jogo. Ao trocar de minijogo, a aba correspondente é selecionada automaticamente.

Usa logos e ícones locais SDK, Syne nas abas, Geist nos controles e Martian Mono na versão. Fontes do popup têm escala limitada para evitar que ultrapassem os controles. Alvos de toque têm pelo menos 44 pt e conteúdo adicional rola dentro do painel. O ícone flutuante de 44 × 44 pt pode ser arrastado e acompanha a área segura. O popup recolhe esse ícone enquanto aberto e tem botão próprio para minimizar.

Alpaca apresenta Auto, Raio X e uma barra de ícones para três poderes, confirmação e armazém. A engrenagem abre Turbo, planejamento e uso de poderes do estoque. A profundidade aparece com o Raio X ativo. Cartas tem marcadores; Bilhar tem Guia, Mira e Auto. Ícones possuem nomes traduzidos para VoiceOver. Indicações de consumo de estoque e pausa após toque manual continuam acessíveis.

O globo abre uma lista pequena English/Português dentro do popup. A preferência salva em `SDKClient.language` permanece; mudar idioma atualiza as views existentes sem reiniciar módulos, apresentar outro controlador ou emitir comandos. O catálogo tipado cobre os rótulos curtos e mensagens de todos os módulos. Website e YouTube são somente ícones discretos, desabilitados e identificados como Em breve na acessibilidade; destinos futuros continuam em `Brand/client-links.json`. Não há Instagram, Discord ou Telegram.

Minimizado, o estado aparece somente em texto verde, sem fundo, junto ao símbolo: Auto, Raio X, Cartas, Guia ou Mira; Auto e Raio X podem aparecer juntos. Avisos completos ficam dentro do popup. A tarja detalhada do Bilhar também foi removida; o estado é apresentado uma única vez. O texto não recebe toques nem bloqueia a partida.

Os métodos originais de ação de STOverlay foram preservados integralmente. Recursos JavaScript/Lua, algoritmos, políticas de comandos, identidade e proteções de ações incertas continuam os da 3.22.1. A identidade é revalidada em cada ação. Sair do jogo correspondente interrompe os recursos; reabrir o menu pausa a automação do Bilhar. A janela permanece não principal e deixa toques fora do popup passarem ao jogo. Ferramentas internas não têm botões de debug, captura ou exportação no menu do cliente.

Validação: 691 testes JavaScript; catálogo bilíngue e cobertura das bindings; prévia HTML em seis tamanhos, quatro contextos e dois idiomas (48 casos), incluindo controles bloqueados, preferência persistida, ajustes e indicadores sem tarja. STCompactMenuLayout.h é usado pelo layout UIKit e por testes C de limites e estados executados na CI. A prévia é referência de design, não execução UIKit. Build iPhoneOS e integração no IPA são verificados pelo workflow oficial. Assinatura, instalação e teste físico são etapas separadas.

O workflow compila exclusivamente SDKtools_Fontes.zip com manifesto SHA-256. ZIP, versão/build, manifesto, tamanho e hash do workflow são atualizados juntos. Cada entrega inclui o IPA e o mesmo coletor diretamente na conversa.
