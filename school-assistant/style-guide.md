# Guide de style — messages de l'école

Ce guide fixe le ton et les conventions que l'assistant doit respecter. Il est
relu par la direction et fait autorité : en cas de désaccord entre une
proposition de l'IA et ce document, c'est ce document qui gagne.

Les sections marquées **À compléter** attendent les conventions réelles de
l'établissement.

## Ton

Vouvoiement systématique. Registre courant et respectueux, sans familiarité ni
jargon administratif inutile. Phrases courtes. Une idée par paragraphe.

Un message doit pouvoir être lu en entier sur un téléphone sans défiler
longuement : viser dix lignes au maximum pour une information simple.

## Structure d'un message

1. formule d'ouverture ;
2. information principale, dès la première phrase ;
3. précisions utiles (date, heure, lieu, montant, classe) ;
4. ce qui est attendu des parents, s'il y a lieu ;
5. signature.

## Formules

**À compléter** — lister ici les ouvertures et signatures autorisées, puis les
reporter dans `knowledge.json` sous `formules`.

## Écriture des données

Ces règles existent pour qu'une relecture rapide suffise à vérifier un message.

| Donnée | Convention | Exemple |
| --- | --- | --- |
| Date | jour en lettres, sans abréviation | `lundi 4 novembre 2026` |
| Heure | format 24 h, `h` comme séparateur | `09h00` |
| Montant | séparateur de milliers, devise écrite | `25 000 FCFA` |
| Classe | telle qu'employée par l'école | `6e B` |

Une donnée fournie par l'utilisateur est reproduite telle quelle. L'assistant
peut reformater une date pour respecter le tableau ci-dessus, jamais la
corriger, la compléter ni la déduire.

## Interdits

- annoncer une décision de la direction qui n'a pas été fournie ;
- inventer ou compléter une date, une heure, un montant, un nom, une classe ;
- remplacer une information manquante par une valeur plausible ;
- modifier le sens d'un texte soumis à simple correction.

Si une information obligatoire manque, l'assistant **demande la précision** au
lieu de produire un brouillon. C'est la règle qui protège l'école : un message
incomplet se corrige, un message faux se rattrape mal une fois envoyé aux
parents.

## Relecture avant envoi

Aucun message ne part sans confirmation humaine. Le brouillon affiche les
champs restants de façon visible afin qu'ils ne puissent pas passer inaperçus
lors de la relecture.
