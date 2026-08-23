# OpenAI Recepten

Codex-plugin voor het persoonlijke, gedigitaliseerde receptenarchief. De plugin bevat de `recepten`-skill en verbindt met de beveiligde MCP-server op `https://recepten.roanensven.nl/mcp`.

## Installeren vanuit GitHub

Voeg deze repository als marketplace toe:

```bash
codex plugin marketplace add SvenHamers/openai-recepter --ref main
```

Herstart daarna de ChatGPT-desktopapp, open **Plugins**, kies **OpenAI Recepten** en installeer **Recepten** met de plusknop. Start na installatie een nieuwe taak.

## Toegangstoken instellen

De repository bevat geen toegangstoken. Vraag het token privé aan de beheerder en stel het lokaal in als `RECEPTEN_MCP_TOKEN`. Deel het token nooit in een issue, chatbericht of commit.

### ChatGPT-desktopapp op macOS

Sluit de app volledig. Voer daarna dit uit; de verborgen invoer voorkomt dat het token in je shellgeschiedenis terechtkomt:

```bash
read -s "RECEPTEN_TOKEN?Recepten-token: "; echo
launchctl setenv RECEPTEN_MCP_TOKEN "$RECEPTEN_TOKEN"
unset RECEPTEN_TOKEN
```

Open de ChatGPT-desktopapp opnieuw. De plugin leest het token uit deze omgevingsvariabele en stuurt het als een Bearer-token naar de MCP-server.

Wil je het token later verwijderen:

```bash
launchctl unsetenv RECEPTEN_MCP_TOKEN
```

### Codex vanuit een terminal

Stel het token in voordat je Codex vanuit diezelfde terminal start:

```bash
read -s "RECEPTEN_MCP_TOKEN?Recepten-token: "; echo
export RECEPTEN_MCP_TOKEN
codex
```

## Beveiligingsmodel

Iedereen kan deze plugin installeren, maar alleen gebruikers met een geldig token krijgen toegang tot de receptendatabase. De huidige server gebruikt een gedeelde Bearer-token. Voor zelfstandig aanmelden per gebruiker is OAuth 2.1 nodig; dat is niet onderdeel van versie 0.1.1.
