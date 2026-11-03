# herdr-copy-reference

Fonte da verdade do plugin de referência do Herdr. É uma feature com dois mods que trabalham juntos:

- `mods/ref-menu` — menu de contexto com **Copy reference**.
- `mods/tabs-ref` — barra de abas que abre o `ref-menu` no right-click da aba.

## Regra: sempre atualizar a pasta live do Herdr

O Herdr lê os mods de `~/.config/herdr-app/mods/<nome>`. Depois de **qualquer** mudança aqui:

```sh
./sync.sh
```

O script copia `mods/ref-menu` e `mods/tabs-ref` para a pasta live e roda `herdr-app check` nos dois. Não edite a pasta live diretamente.

## Ligação no layout

O layout pessoal `~/.config/herdr-app/layouts/main-ref.json` usa:

- bloco `tabs` -> `tabs-ref`
- root `terminal_menu` -> `ref-menu`

Mantenha os nomes das pastas. Se o layout for resetado, reponha esses dois pontos.

## Skill

A skill `herdr-publish` está em `.agents/skills/herdr-publish/SKILL.md`. Ela cobre validação, sync, `RECIPE.md`/`preview.png` e publicação em `herdr.dev/mods` com o tópico `herdr-mod`.
