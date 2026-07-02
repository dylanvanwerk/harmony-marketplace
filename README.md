# Harmony Marketplace

Een Claude Code plugin-marketplace. Deze repo bevat (nog) geen plugins — de map
`plugins/` is de plek waar nieuwe plugins bijkomen, en `.claude-plugin/marketplace.json`
registreert welke plugins beschikbaar zijn.

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
   plugin te zien bij `/plugin marketplace update`.
