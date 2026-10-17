# SDK Client 3.22.0 — build 48

Base: SDKtools 3.21.0/build 47, commit `27e76d6c15341f79aec7d725c31142208cb59baf`, branch `codex/sdktools-3-21-0-billiards` do repositório oficial. A atualização para esse marco foi autorizada pelo usuário durante o trabalho de marca.

O popup UIKit usa os logos originais SDK, Syne, Geist e Martian Mono SemiCondensed, com registro de fontes em CoreText, recursos locais e respectivas licenças OFL. Cores, ícones, proporções dos logos, raios, alvos de toque e espaçamentos seguem o brandbook entregue. Não baixa fontes, imagens ou código ao abrir.

Somente o minijogo identificado libera controles. O cartão ativo fica primeiro, destacado; os demais ficam escurecidos e recolhidos. A identidade é conferida novamente no início de cada ação. Alpaca/Cartas reutilizam a verificação nativa do controlador/WebView; Bilhar exige uma UnityView visível e a cena carregada BilliardInGame/BilliardTutorial, pela ponte já validada da base. A pequena consulta `billiards_context.lua` não inicia o observador, não instala hooks, não carrega módulos e não acessa estado da partida. Sem identidade válida, todos os controles ficam bloqueados. A consulta é limitada, ocorre no máximo a cada 0,75 s na interface e o timer para quando não há menu, função ou aviso ativo. As ações sempre revalidam sem cache.

Ao sair do jogo correspondente, autoplay, X-ray, marcadores e guia do Bilhar são interrompidos. Operações físicas já enviadas mantêm os bloqueios e callbacks existentes. O layout acompanha a área segura, orientação e Dynamic Type; a lista rola em telas pequenas. O popup não toma a janela principal do jogo. Reabrir o menu pausa Aim/Auto do Bilhar, como na base 3.21.0.

Funções preservadas: autoplay com missões, Turbo, planejamento ampliado, uso explícito de poderes existentes, X-ray/profundidade, três poderes originais, confirmação e armazém do Alpaca; marcadores de Cartas; guia, Aim e autoplay da partida atual do Bilhar. Os algoritmos de jogo, contratos, limites e proteções da base 3.21.0 permanecem inalterados. O uso de poderes informa que pode consumir estoque existente.

Ferramentas de diagnóstico, captura, injeção/amostragem manual, exportação de fontes/relatórios e teste experimental do armazém não têm botões na interface do cliente. Os componentes internos permanecem no coletor para manutenção. YouTube e Website aparecem como “Coming soon”, sem destinos fictícios. Instagram, Discord e Telegram não são exibidos, conforme a confirmação do usuário.

Para atualizar a identidade visual, use `STBrandTheme` e `Resources/Brand/`. Os canais futuros usam `Brand/client-links.json`: somente HTTPS válido habilita uma ação, sempre mediante toque. Novos jogos devem ter identidade comprovada, uma entrada em `STClientGamePolicy` e seu próprio adaptador; não liberar um jogo com base na última seleção.

Verificação local: 688 testes JavaScript; 96 testes Python (92 aprovados, quatro dependentes de compilador pulados no Windows). A prévia HTML foi inspecionada em 320×568, 390×844, 844×390 e 1024×768, sem largura excedente e com as três fontes carregadas. É uma prévia de design, não execução UIKit. O workflow oficial executa também as políticas C, contratos Foundation, suítes Lua e compilação iPhoneOS. Assinatura, instalação e teste físico no iPhone são verificações separadas.

O workflow compila exclusivamente o ZIP com manifesto SHA-256. Fontes, ZIP, versão, tamanho e hash do workflow são atualizados juntos. O pacote de entrega deve conter o IPA sem assinatura e o mesmo `SDKtools_Fontes.zip` diretamente na conversa.
