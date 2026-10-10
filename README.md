# School WhatsApp Assistant

Assistant WhatsApp interne pour aider la direction et le secrétariat à
préparer des messages scolaires corrects, cohérents et validés avant envoi.

Le projet sera connecté à Baileys, mais restera séparé du bot personnel
`botpdg`. L'assistant fonctionnera d'abord en mode brouillon : aucune
communication aux parents ne sera envoyée sans confirmation explicite d'un
utilisateur autorisé.

## Architecture

Le fonctionnement est décrit dans [`ARCHITECTURE.md`](ARCHITECTURE.md), avec
un diagramme général et le déroulement d'une demande jusqu'à la validation.

## État

Le cadrage fonctionnel et technique est disponible dans
[`SCHOOL_ASSISTANT_PLAN.md`](SCHOOL_ASSISTANT_PLAN.md).

La prochaine étape est d'intégrer les exemples réels de messages de l'école,
les quatre utilisateurs autorisés et les rôles associés.
