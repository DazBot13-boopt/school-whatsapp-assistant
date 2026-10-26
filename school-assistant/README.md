# Base éditoriale

Ce dossier contient la matière que l'assistant utilise pour rédiger : les
informations stables de l'école, les modèles approuvés, le guide de style et
les droits des utilisateurs. Il correspond à la **Phase 2 — base éditoriale**
du plan.

## Fichiers

| Fichier | Rôle | Versionné |
| --- | --- | --- |
| `knowledge.json` | informations stables, vocabulaire, interdits | non |
| `templates.json` | modèles approuvés par la direction | non |
| `access.json` | utilisateurs autorisés et droits | non |
| `style-guide.md` | ton, structure, conventions d'écriture | oui |

Les trois fichiers JSON sont **ignorés par git**. Seuls leurs équivalents
`*.example.json` sont publiés : ils montrent la structure attendue sans
exposer un seul numéro, nom ou montant réel. C'est la règle posée par le plan
— « les numéros et les droits ne seront pas écrits en dur dans le code
public ».

## Mise en route

```bash
cd school-assistant
cp access.example.json    access.json
cp knowledge.example.json knowledge.json
cp templates.example.json templates.json
```

Puis remplir les trois fichiers, et faire relire `templates.json` par la
direction avant tout usage réel.

## Schéma des fichiers

### `access.json`

- `roles` — un objet par rôle. Quatre droits indépendants : `corriger`,
  `redigerBrouillon`, `valider`, `envoyer`. `envoyer` est celui qui autorise
  l'écriture dans un groupe de parents ; il se donne séparément de `valider`.
- `utilisateurs` — numéro au format international, rôle, et `actif` pour
  retirer quelqu'un sans perdre la trace de son existence.
- `groupesAutorises` — identifiant WhatsApp du groupe et `envoiAutorise`, à
  `false` par défaut.
- `refusDiscret` — comportement envers un numéro inconnu. `repondre: false`
  ne renvoie rien du tout, `journaliser: true` garde la trace de la tentative.

### `knowledge.json`

- `etablissement`, `anneeScolaire`, `classes` — ce que l'assistant a le droit
  d'affirmer sans le demander.
- `vocabulaire` — remplacements à appliquer, avec la raison. La raison sert à
  la relecture : elle explique pourquoi la règle existe.
- `formules` — ouvertures et signatures autorisées.
- `interdits` — règles de non-invention, reprises telles quelles dans la
  consigne envoyée au modèle.

### `templates.json`

Chaque modèle porte un `id` stable, un `libelle` lisible, ses `variables` et
un `corps`.

- une variable a un `nom`, un `type` (`texte`, `date`, `heure`, `montant`),
  un drapeau `obligatoire` et un `exemple` ;
- le `corps` référence ses variables sous la forme `{{nom}}` ;
- **toute variable `obligatoire` manquante bloque la validation.** Le
  brouillon n'est pas produit : l'assistant demande la précision.
- `approuvePar` et `approuveLe` restent vides tant que la direction n'a pas
  relu le modèle. Un modèle non approuvé ne doit pas servir à un envoi.

### `style-guide.md`

Versionné parce qu'il ne contient aucune donnée personnelle. Les sections
**À compléter** attendent les conventions réelles de l'établissement.

## Ce que ce dossier ne fait pas

Il ne contient aucun code. Le module Baileys, l'autorisation par numéro et la
validation des variables relèvent de la Phase 3, et viendront séparément.
