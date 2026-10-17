# SDKtools 3.21.0 / build 47 — Bilhar inteligente

WePlay **US 6.6.2/build132**. Base SDK3.20.0. Alpaca e Cartas preservados;
os15 JavaScripts não mudaram. A nova versão adiciona controles do Bilhar.

## Usar

1. Abra a **partida atual** e o menu SDKtools → Bilhar.
2. **Ativar leitura**: somente guia/diagnóstico, sem ações.
3. **Aim automático · sem disparar**: escolhe bola/caçapa, ajusta mira e força;
   você dispara manualmente. O primeiro toque pausa a automação, preservando a mira.
4. **Autoplay inteligente · partida atual**: escolhe diretas/tabelas e força,
   confirma o caminho e usa uma vez o release original, esperando o turno seguinte.
5. Toque na mesa, abra o menu ou vá para segundo plano para pausar. Rearme
   explicitamente. Fim da partida para: **sem revanche e sem fila automática**.

O HUD mostra alvo, força, estado, tacadas solicitadas, amostras de calibração e
tempo desde início da leitura. Exporte a leitura para conferir `automation`.

## Física, calibração e limites

Impulso original `0.031*p*sqrt(p/CUE_POWER_MAX)`, massa/inércia e geometria
vivas, busca limitada de força por contato-slip/rolamento, trajetória direta
ou tabela de uma reflexão, oclusão e proteção da bola8. Os casts vivos validam
rota/primeiro contato. Calibração só ajusta lançamento após3 trechos medidos
qualificados, com ganho limitado0.9–1.1.

É modelo reduzido, não o solver PhysX completo nem aim perfeito. Sem rota
segura confirmada, aguarda. Bola na mão requer colocação manual e reativação;
spin selecionado, tutorial/offline e contrato incompatível não são automatizados.
Leia `Analysis/V3_21_0-billiards-strategy.md` para regras, fontes, REA e limites.

## Compilar e instalar

`SDKtools_Fontes.zip` e `compilar.yml` formam um par fixado por tamanho/SHA256.
Workflow **Compilar SDKtools US**, branch desta versão, `base_source=release`,
`release_tag=base-us-6.6.2`. Saída:
`WePlay_US_6.6.2_SDKtools_v3_21_0_unsigned.ipa` — **precisa assinar para instalar**.

Testes Lua5.3/mocks, regressões Python/JavaScript e CI Apple são verificados
separadamente. **Sem iPhone conectado nesta estação: precisão e compatibilidade
viva da automação ainda exigem teste no aparelho.** Não há vitória/ganho garantido.

Alpaca mantém missão primeiro, Turbo, planejamento maior e poderes próprios
opt-in, todos inicialmente desligados. O experimento de armazém continua oculto.
Cartas mantém cores efetivamente recebidas, sem inventar faces ocultas.
