# Assistant WhatsApp de rédaction — école

## Objectif

Créer un assistant interne sur WhatsApp pour aider la direction et le
secrétariat à rédiger des messages clairs, uniformes et relus avant leur
envoi aux parents, aux élèves ou aux groupes de l'école.

Le bot doit produire un brouillon prêt à relire. Il ne doit jamais envoyer
automatiquement un message aux parents sans confirmation explicite d'un
membre autorisé.

## Principe retenu

Le bot reste basé sur Baileys et utilise la connexion WhatsApp déjà en place.
La fonction sera ajoutée au bot existant comme un module séparé, afin de ne
pas mélanger l'assistant scolaire avec les fonctions de statuts, d'anti-
suppression et de téléchargement.

La qualité reposera sur quatre niveaux :

1. des modèles de messages validés par l'école ;
2. une base de connaissances contenant le vocabulaire, les règles et le ton
   officiels de l'établissement ;
3. une correction linguistique avec consigne stricte de ne rien inventer ;
4. une confirmation humaine avant toute copie ou envoi.

Une IA seule ne peut pas garantir mathématiquement zéro faute. Le système
réduira le risque avec des modèles verrouillés, une vérification finale et un
mode « doute » qui demande une relecture au lieu de compléter une information
manquante.

## Accès des utilisateurs

Les quatre membres autorisés seront enregistrés dans une liste dédiée,
distincte du propriétaire technique du bot. Chaque utilisateur pourra :

- demander la correction d'un texte ;
- demander un message à partir d'un type connu ;
- modifier le brouillon proposé ;
- confirmer la copie ou l'envoi, selon les droits qui lui sont attribués.

Les autres numéros recevront un refus discret. Les numéros et les droits ne
seront pas écrits en dur dans le code public : ils resteront dans la
configuration locale ou seront administrés par une commande propriétaire.

## Commandes prévues

Les noms pourront être ajustés après validation par l'école.

```text
?ecole                         → aide et état du module
?ecole corriger <texte>        → corrige sans changer le sens
?ecole modele                  → liste les modèles disponibles
?ecole message <type> <infos>  → prépare un brouillon depuis un modèle
?ecole revoir                  → reformule le dernier brouillon
?ecole valider                 → confirme le dernier brouillon
?ecole annuler                 → supprime le brouillon en cours
```

Par défaut, `valider` renverra le texte final dans la conversation de travail.
L'envoi dans un groupe de parents nécessitera un droit séparé et une
confirmation explicite, par exemple `?ecole envoyer`.

## Base de connaissances

Elle sera organisée en fichiers versionnés et relus :

```text
school-assistant/
  knowledge.json       règles, vocabulaire et informations stables
  templates.json       modèles approuvés par l'école
  style-guide.md       ton, formules et conventions
  access.json          utilisateurs autorisés et droits locaux
```

Les messages historiques serviront à extraire les modèles, mais ne seront
pas réutilisés aveuglément : les noms, dates, montants, classes et liens
seront remplacés par des variables obligatoires.

## Garde-fous contre les fautes et les inventions

- correction orthographique et grammaticale en français ;
- conservation stricte des dates, heures, montants et noms fournis ;
- refus si une donnée obligatoire manque ;
- interdiction d'inventer une décision de la direction ou une information
  scolaire ;
- vérification des variables avant confirmation ;
- aperçu du texte final avec marqueurs visibles pour les champs à compléter ;
- journal local des demandes et validations, sans enregistrer inutilement
  les conversations privées.

## Plan de réalisation

### Phase 1 — cadrage

- récupérer les quatre numéros et leurs rôles ;
- classer les exemples par type de message ;
- identifier les informations sensibles et les modèles officiels ;
- choisir qui peut seulement corriger et qui peut envoyer.

### Phase 2 — base éditoriale

- créer les fichiers `knowledge.json`, `templates.json` et `style-guide.md` ;
- transformer les exemples en modèles avec variables ;
- faire relire et approuver les modèles par la direction.

### Phase 3 — module Baileys

- ajouter le module assistant au bot ;
- ajouter l'autorisation par numéro WhatsApp ;
- implémenter correction, génération, aperçu, validation et annulation ;
- conserver un brouillon séparé par utilisateur et par conversation ;
- désactiver tout envoi automatique par défaut.

### Phase 4 — vérification

- tests unitaires sur les droits, variables, dates et montants ;
- tests avec des fautes réelles issues des anciens messages ;
- tests de non-invention avec informations volontairement incomplètes ;
- test de redémarrage PM2 et de persistance contrôlée ;
- validation humaine par la direction.

### Phase 5 — mise en service progressive

- mode brouillon uniquement pendant la première période ;
- activation de l'envoi uniquement après validation ;
- suivi des corrections demandées et amélioration des modèles ;
- revue régulière de la base de connaissances.

## Critères d'acceptation

Le module sera considéré prêt quand :

- les quatre utilisateurs autorisés peuvent l'utiliser ;
- un numéro non autorisé ne peut pas obtenir de brouillon ;
- les modèles approuvés produisent toujours les formules attendues ;
- les champs manquants bloquent la validation ;
- aucune demande ne déclenche un envoi sans confirmation ;
- les tests de correction et de non-invention passent ;
- la direction a relu un échantillon représentatif de messages.

## Données nécessaires pour commencer

- les quatre numéros WhatsApp au format international ;
- les rôles de chaque personne ;
- les exemples de messages classés par type ;
- les formulations à conserver absolument ;
- la liste des groupes où un envoi pourrait être autorisé ;
- les règles de confidentialité et de conservation des brouillons.
