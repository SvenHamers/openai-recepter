---
name: recepten
description: Zoek, lees, kies, maak en wijzig recepten in het persoonlijke gedigitaliseerde receptenarchief via de beveiligde Recepten MCP-server. Gebruik voor natuurlijke receptzoekvragen, koken met aanwezige ingrediënten, sectieoverzichten, willekeurige recepten, receptdetails, recepten uit tekst of foto, receptcorrecties en tags.
---

# Recepten

Gebruik uitsluitend deze negen Recepten MCP-tools voor handelingen in het receptenarchief:

- `search_recipes`
- `get_recipe`
- `whats_cookable`
- `list_sections`
- `random_recipe`
- `create_recipe`
- `update_recipe`
- `add_tag`
- `remove_tag`

Gebruik geen andere tool, browser, bestandstoegang of directe databaseactie om receptgegevens te lezen of te wijzigen. De server staat op `https://recepten.roanensven.nl/mcp` en gebruikt OAuth 2.1 met persoonlijke Recepten-accounts. Laat de normale koppel- of inloginterface van ChatGPT/Codex de OAuth-flow uitvoeren; vraag nooit om een wachtwoord, toegangscode of token in de chat en schrijf zulke gegevens niet naar bestanden.

Als authenticatie nodig is, vraag de gebruiker de Recepten-verbinding te koppelen en in te loggen met het account dat door de beheerder is aangemaakt. Bij een verlopen of ingetrokken sessie laat je de gebruiker opnieuw koppelen. Leg bij onvoldoende rechten uit of `recipes:read` dan wel `recipes:write` ontbreekt en adviseer opnieuw koppelen of contact opnemen met de beheerder. Als het account niet is toegestaan, leg uit dat de beheerder toegang moet verlenen. Als de server niet bereikbaar is, meld dat zonder resultaten te verzinnen of naar een andere bron uit te wijken.

Alle negen tools vereisen OAuth. De vijf leesacties gebruiken `recipes:read`; `create_recipe`, `update_recipe`, `add_tag` en `remove_tag` gebruiken `recipes:write`. Vertrouw op de scopes en gebruikersidentiteit die de MCP-server valideert en probeer authenticatie nooit te omzeilen met een gedeeld of handmatig Bearer-token.

## Kies de juiste tool

- Gebruik `search_recipes` als standaard voor natuurlijke zoekvragen zoals “ik wil iets met de oven maken”. Geef de vraag of relevante termen door en laat stopwoorden, spelling en zoeknormalisatie aan de server over. Gebruik het teruggegeven id met `get_recipe` zodra volledige ingrediënten of bereidingsstappen nodig zijn.
- Gebruik `whats_cookable` voor “ik heb deze ingrediënten”. Geef eenvoudige ingrediëntnamen door. Vertrouw op de serverlogica: voorraadkast-basics zoals zout, peper, olie, boter, suiker, bloem, water en azijn tellen niet als ontbrekende ingrediënten. Herbereken of overschrijf de serverrangschikking niet.
- Gebruik `list_sections` voor een archiefoverzicht of om een geldige sectie te kiezen.
- Gebruik `random_recipe` voor “verras me” of een willekeurig kookidee; geef eventuele filters mee.
- Gebruik `get_recipe` voor één volledig recept op basis van een id.
- Gebruik `create_recipe` voor een nieuw recept uit tekst, dictaat, plaktekst of foto.
- Gebruik `update_recipe` voor correcties aan een bestaand recept. Zoek en lees het recept eerst als het id of de bedoelde wijziging niet volkomen duidelijk is. Velden die niet worden meegegeven blijven ongewijzigd; lijsten voor ingrediënten, stappen, apparatuur en tags vervangen telkens de volledige bestaande lijst.
- Gebruik `add_tag` of `remove_tag` voor één tag, zodat de rest van het recept ongemoeid blijft.

## Alleen gedigitaliseerde recepten

Behandel het archief als een verzameling die nog door een extractiepipeline wordt gedigitaliseerd:

- Alle zoek-, lees- en wijzigingsacties werken alleen op recepten met reeds gestructureerde gegevens.
- `search_recipes`, `whats_cookable` en `random_recipe` tonen uitsluitend gedigitaliseerde recepten.
- `get_recipe`, `update_recipe`, `add_tag` en `remove_tag` kunnen een ouder, nog ongestructureerd recept niet behandelen.
- Behandel een servermelding met `nog niet gedigitaliseerd` als een verwachte toestand, niet als een defect. Leg helder uit dat het recept wel in het bronarchief staat, maar nog door de extractiepipeline moet worden omgezet voordat het via deze plugin kan worden gelezen of aangepast. Probeer het niet via een andere bron of tool te omzeilen; bied aan later opnieuw te proberen of naar een gedigitaliseerd alternatief te zoeken.

## Foto naar recept

Wanneer de gebruiker een foto of screenshot van een recept wil toevoegen:

1. Lees de afbeelding zelf visueel uit; `create_recipe` voert geen OCR uit.
2. Extraheer minimaal titel, alle ingrediënten met hoeveelheden/eenheden/notities en de bereidingsstappen. Behoud de taal en hoeveelheden van het recept.
3. Vraag alleen om ontbrekende informatie wanneer die niet betrouwbaar uit de afbeelding of context is af te leiden.
4. Roep `create_recipe` aan met de gestructureerde velden. Geef dezelfde afbeelding mee als `image_base64` en het juiste `image_media_type`, zodat deze als hero-afbeelding wordt opgeslagen.
5. Controleer met `search_recipes` op de nieuwe titel dat het recept direct vindbaar is; gebruik zo nodig `get_recipe` om de opgeslagen gegevens te tonen.

Maak geen recept aan als de afbeelding onvoldoende leesbaar is om minstens één ingrediënt en één stap betrouwbaar vast te leggen. Meld dan concreet welk deel opnieuw of scherper moet worden aangeleverd.

## Antwoorden

Antwoord standaard in het Nederlands, tenzij de gebruiker een andere taal gebruikt. Vat zoekresultaten compact samen en noem relevante serverinformatie zoals ontbrekende ingrediënten, bereidingstijd of sectie. Presenteer toolfouten in gewone taal zonder interne transportdetails.
