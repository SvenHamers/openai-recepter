# OpenAI Recepten

Plugin voor het persoonlijke, gedigitaliseerde receptenarchief. De plugin bevat de `recepten`-skill en verbindt met de met OAuth 2.1 beveiligde MCP-server op `https://recepten.roanensven.nl/mcp`.

## Installeren vanuit GitHub

Voeg deze repository als marketplace toe:

```bash
codex plugin marketplace add SvenHamers/openai-recepter --ref main
```

Herstart daarna de ChatGPT-desktopapp, open **Plugins**, kies **OpenAI Recepten** en installeer **Recepten** met de plusknop. Kies **Verbinden** wanneer daarom wordt gevraagd en log in met je persoonlijke Recepten-account. Start na installatie een nieuwe taak.

## Account koppelen

Er hoeft geen token of omgevingsvariabele te worden ingesteld. ChatGPT/Codex ontdekt de OAuth-server automatisch via `https://recepten.roanensven.nl/.well-known/oauth-protected-resource` en opent de beveiligde inlogpagina wanneer de verbinding wordt gekoppeld of een recepttool authenticatie nodig heeft.

Accounts worden door de beheerder van het receptenarchief aangemaakt. Vul je e-mailadres en wachtwoord alleen in op de beveiligde pagina onder `https://recepten.roanensven.nl/`; deel ze nooit in een chatbericht, issue of commit.

De rechten zijn verdeeld over twee scopes:

- `recipes:read` voor zoeken, receptdetails, kookideeën, secties en willekeurige recepten;
- `recipes:write` voor recepten maken of wijzigen en tags toevoegen of verwijderen.

Als de sessie is verlopen, het account is uitgeschakeld of een scope ontbreekt, koppel de Recepten-verbinding opnieuw. Neem contact op met de beheerder wanneer het account nog niet bestaat of niet is toegestaan.

## Beveiligingsmodel

Iedereen kan de publieke plugin installeren, maar alleen een geldig, toegestaan Recepten-account krijgt toegang. De server gebruikt OAuth 2.1 Authorization Code met PKCE, kortlevende toegangstokens en afzonderlijke lees- en schrijfrechten. Wachtwoorden en tokens staan niet in deze repository.
