# Diagramme d'architecture

## Vue générale

```mermaid
flowchart LR
    U[Direction et secrétariat\n4 utilisateurs autorisés]
    W[WhatsApp]
    B[Bot Baileys\nconnexion WhatsApp]
    A[Contrôle d'accès\nnuméro + rôle]
    C[Assistant scolaire]
    K[(Base de connaissances\nmodèles validés\nvocabulaire\nstyle officiel)]
    I[Provider IA\nGemini / autre provider]
    V[Validation éditoriale\northographe\nvariables\ncohérence]
    D[Brouillon proposé\naucun envoi automatique]
    H{Confirmation\nhumaine}
    G[Message final\nà envoyer]
    P[Groupes de parents\nou conversations autorisées]
    L[(Journal minimal\ndemandes et validations)]

    U --> W --> B --> A
    A -->|autorisé| C
    A -->|refusé| R[Accès refusé]
    C --> K
    C --> I
    K --> C
    I --> C
    C --> V --> D --> H
    H -->|corriger| C
    H -->|annuler| X[Fin sans envoi]
    H -->|valider| G --> P
    A -.-> L
    H -.-> L
```

## Flux d'une demande

```mermaid
sequenceDiagram
    actor Utilisateur as Direction / secrétariat
    participant WA as WhatsApp
    participant Bot as Baileys + assistant
    participant KB as Base de connaissances
    participant IA as Provider IA
    participant Parent as Groupe ou parent

    Utilisateur->>WA: ?ecole message absence classe 6e demain
    WA->>Bot: message reçu
    Bot->>Bot: vérifier numéro et rôle
    Bot->>KB: charger modèle « absence »
    KB-->>Bot: modèle + variables obligatoires
    Bot->>IA: rédiger selon le modèle et le style officiel
    IA-->>Bot: proposition
    Bot->>Bot: corriger, vérifier et détecter les champs manquants
    Bot-->>WA: brouillon à relire
    Utilisateur->>WA: ?ecole valider
    WA->>Bot: confirmation explicite
    Bot-->>Parent: message final autorisé
    Bot-->>WA: confirmation et référence du modèle utilisé
```

## Règle de sécurité principale

L'IA prépare un texte, mais ne décide pas seule de l'envoi. Une personne
autorisée doit confirmer le brouillon. Si une date, une classe, un montant ou
une autre information obligatoire manque, le bot demande la précision au lieu
de l'inventer.
