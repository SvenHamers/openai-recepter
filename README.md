# OpenAI Recepten en Second Brain

Persoonlijke Git-marketplace met twee plugins:

- **Recepten** voor het persoonlijke, gedigitaliseerde receptenarchief via `https://recepten.roanensven.nl/mcp`.
- **Second Brain** voor persoonlijk geheugen, geselecteerde Home Assistant-bronnen, bevestigde tv/media-acties en cameraweergave via `https://mcp.roanensven.nl/mcp`.

## Installeren vanuit GitHub

Voeg deze repository als marketplace toe:

```bash
codex plugin marketplace add SvenHamers/openai-recepter --ref main
```

Herstart daarna de ChatGPT-desktopapp, open **Plugins**, kies **OpenAI Recepten** en installeer **Recepten** of **Second Brain** met de plusknop. Kies **Verbinden** wanneer daarom wordt gevraagd en rond de beveiligde accountkoppeling af. Start na installatie een nieuwe taak.

Voor Second Brain kun je daarna `brain_setup` gebruiken om Home Assistant privé te koppelen en expliciet camera's, bronnen en vaste acties te selecteren.

## Account koppelen

Er is geen handmatige configuratie nodig. ChatGPT/Codex opent automatisch de beveiligde inlogpagina wanneer je de verbinding koppelt of voor het eerst een recepttool gebruikt.

Accounts worden door de beheerder van het receptenarchief aangemaakt. Vul je e-mailadres en wachtwoord alleen in op de beveiligde pagina onder `https://recepten.roanensven.nl/`; deel ze nooit in een chatbericht, issue of commit.

De rechten zijn verdeeld over twee scopes:

- `recipes:read` voor zoeken, receptdetails, kookideeën, secties en willekeurige recepten;
- `recipes:write` voor recepten maken of wijzigen en tags toevoegen of verwijderen.

Als de sessie is verlopen, het account is uitgeschakeld of een scope ontbreekt, koppel de Recepten-verbinding opnieuw. Neem contact op met de beheerder wanneer het account nog niet bestaat of niet is toegestaan.

## Beveiligingsmodel

Iedereen kan de publieke plugins installeren, maar alleen een geldig, toegestaan account krijgt toegang. De servers gebruiken OAuth 2.1 Authorization Code met PKCE. Inloggegevens staan niet in deze repository. Dit geldt ook voor Home Assistant-tokens, Second Brain-pairing keys, OAuth-sessies en persoonlijke Second Brain-data.
