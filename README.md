# OpenAI Recepten

Codex-plugin voor het persoonlijke, gedigitaliseerde receptenarchief. De plugin bevat de `recepten`-skill en verbindt met de lokale MCP-server op `http://127.0.0.1:3210/mcp`.

## Installeren vanuit GitHub

Voeg deze repository als marketplace toe:

```bash
codex plugin marketplace add SvenHamers/openai-recepter --ref main
```

Herstart daarna de ChatGPT-desktopapp, open **Plugins**, kies **OpenAI Recepten** en installeer **Recepten** met de plusknop. Start na installatie een nieuwe taak.

## Vereiste lokale server

De plugin bevat niet de persoonlijke receptendatabase. Start de bestaande MCP-server voordat je de plugin gebruikt:

```bash
cd /Users/svenhamers/recepter/recipe-mcp
npm start
```

De server moet bereikbaar zijn op `http://127.0.0.1:3210/mcp`.
