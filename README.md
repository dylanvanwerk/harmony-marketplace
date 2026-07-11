# Harmony Marketplace

Een Claude Code plugin-marketplace. De map `plugins/` bevat de plugins, en
`.claude-plugin/marketplace.json` registreert welke plugins beschikbaar zijn.

## Plugins

| Plugin | Omschrijving |
|--------|--------------|
| **harmony-handoff** | Bundel skills die de handoff van design naar development bij Somtoday versnelt: acceptatiecriteria schrijven/verscherpen (`acceptatie-criteria`) en een gebouwde PR/staging vergelijken met het design (`design-review`), met een Nederlandstalig rapport en JIRA-klare tickets. |

## Installeren

Voeg deze marketplace toe in Claude Code (of Cowork):

```
/plugin marketplace add dylanvanwerk/harmony-marketplace
```

Zodra er plugins in `marketplace.json` staan, installeer je er een met:

```
/plugin install <plugin-naam>
```

Collega's die deze repo kunnen zien (public repo) kunnen bovenstaande stappen zelf
uitvoeren om bij dezelfde marketplace te komen.

## Updaten

Wijzigingen in deze repo komen niet automatisch aan bij collega's — dit is
pull-based, niet push-based. Zij moeten zelf updaten:

1. **Marketplace-catalogus verversen** (haalt alleen de metadata uit
   `marketplace.json` opnieuw op, update geen geïnstalleerde plugins):

   ```
   /plugin marketplace update dylanvanwerk/harmony-marketplace
   ```

2. **Een al-geïnstalleerde plugin bijwerken** — dit gebeurt niet automatisch bij
   stap 1, dus opnieuw installeren:

   ```
   /plugin uninstall <plugin-naam>
   /plugin install <plugin-naam>
   ```

3. **Actieve sessie laten oppikken:**

   ```
   /reload-plugins
   ```

   Zonder deze stap blijft de oude versie van de plugin/skill actief in een
   lopende sessie.

Wil je dit niet elke keer handmatig doen? Zet auto-update aan per marketplace via
`/plugin` → **Marketplaces** → `harmony-marketplace` → **Enable auto-update**. Dat
verversert automatisch de catalogus, maar een al-geïnstalleerde plugin moet je
dan nog steeds zelf opnieuw installeren om de nieuwste versie te krijgen.

## Structuur

```
.
├── .claude-plugin/
│   └── marketplace.json    # registreert alle plugins in deze marketplace
├── README.md
└── plugins/
    └── <plugin-naam>/
        ├── .claude-plugin/
        │   └── plugin.json
        ├── README.md
        └── skills/
            └── <skill-naam>/
                └── SKILL.md
```

## Een plugin toevoegen

1. Maak `plugins/<plugin-naam>/.claude-plugin/plugin.json` aan:

   ```json
   {
     "name": "<plugin-naam>",
     "description": "Korte beschrijving van wat de plugin doet.",
     "author": {
       "name": "Dylan Foks"
     },
     "keywords": ["keyword1", "keyword2"]
   }
   ```

2. Voeg de skill(s) toe onder `plugins/<plugin-naam>/skills/<skill-naam>/SKILL.md`.
3. Registreer de plugin in `.claude-plugin/marketplace.json`:

   ```json
   {
     "name": "<plugin-naam>",
     "description": "Zelfde beschrijving als in plugin.json.",
     "source": "./plugins/<plugin-naam>"
   }
   ```

4. Commit en push. Iedereen die de marketplace al heeft toegevoegd krijgt de nieuwe
   plugin te zien na een marketplace-update (zie [Updaten](#updaten)) — daarna
   installeren ze de plugin zelf met `/plugin install <plugin-naam>`.
