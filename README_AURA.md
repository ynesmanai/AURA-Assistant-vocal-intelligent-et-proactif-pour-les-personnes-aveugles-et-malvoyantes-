# AURA --- Assistant vocal intelligent et proactif pour les personnes aveugles et malvoyantes

> **AURA** est un concept d'assistant personnel vocal conçu pour
> renforcer l'autonomie des personnes aveugles et malvoyantes. Il
> combine intelligence artificielle, automatisation et services
> connectés pour aider l'utilisateur à s'informer, organiser son
> quotidien et effectuer certaines actions par la voix.

**Statut :** concept / prototype en préparation\
**Type de projet :** application mobile accessible + assistant IA +
workflows d'automatisation\
**Approche de développement :** Vibe Coding, avec validation technique
et tests d'accessibilité

------------------------------------------------------------------------

## 1. Vision du projet

Les assistants vocaux classiques répondent principalement à des
commandes ponctuelles. AURA vise une expérience plus proactive :
l'assistant peut préparer des informations utiles, rappeler les tâches
importantes et accompagner l'utilisateur dans certaines démarches
quotidiennes.

L'objectif n'est pas de remplacer l'autonomie de la personne ni les
outils spécialisés de mobilité, mais de lui offrir un compagnon
numérique accessible, personnalisable et fiable.

### Proposition de valeur

-   **Vocal-first :** les fonctions essentielles doivent être
    utilisables sans regarder l'écran.
-   **Proactif :** l'assistant peut transmettre un briefing ou un rappel
    au bon moment.
-   **Orienté action :** il ne se limite pas à donner des réponses ; il
    peut préparer des actions via des services compatibles.
-   **Personnalisable :** l'utilisateur choisit ses sujets d'actualité,
    ses horaires, sa voix et ses préférences.
-   **Sécurisé :** les actions sensibles nécessitent une confirmation
    explicite.

------------------------------------------------------------------------

## 2. Fonctionnalités envisagées

### A. Briefing audio quotidien

À une heure choisie, AURA prépare un résumé vocal court (environ 1 à 2
minutes) qui peut inclure :

-   les principales actualités locales et internationales ;
-   la météo du jour et les prévisions ;
-   les alertes importantes disponibles ;
-   les tâches et rendez-vous prévus ;
-   les informations personnalisées selon les centres d'intérêt de
    l'utilisateur.

Les informations doivent provenir de sources identifiables. Le résumé
doit distinguer les faits confirmés, les prévisions et les informations
incertaines.

### B. Gestionnaire vocal de tâches

L'utilisateur peut ajouter, consulter, modifier ou terminer une tâche à
la voix.

Exemples : - « Rappelle-moi d'appeler le médecin demain à 10 heures. » -
« Quelles sont mes tâches aujourd'hui ? » - « Marque les courses comme
terminées. »

### C. Rappels et agenda

-   rappels ponctuels et récurrents ;
-   lecture vocale de l'agenda ;
-   rappels avant un rendez-vous ;
-   proposition de préparer un déplacement ;
-   synchronisation future avec un calendrier compatible, avec
    autorisation de l'utilisateur.

### D. Réservations et démarches

À terme, AURA pourra aider à rechercher et préparer :

-   un taxi ;
-   un rendez-vous médical ;
-   une table au restaurant ;
-   une pharmacie ou un service à proximité.

La réservation ne sera effectuée que si le service propose une
intégration autorisée ou un parcours accessible et si l'utilisateur
confirme les détails avant validation.

### E. Communication

Fonctionnalités envisagées selon les permissions et les capacités du
système :

-   appeler un contact choisi ;
-   dicter un message ;
-   lire les notifications compatibles ;
-   préparer un message et demander confirmation avant envoi.

### F. Accessibilité et sécurité

-   commandes vocales et retours audio ;
-   compatibilité avec les lecteurs d'écran ;
-   commandes simples pour répéter, interrompre ou annuler ;
-   réglage du débit, du volume et de la voix ;
-   mode de confirmation pour les actions sensibles ;
-   accès rapide à un contact de confiance, si configuré par
    l'utilisateur.

La reconnaissance de l'environnement par caméra (lecture de texte,
identification d'objets ou de panneaux) est une piste future. Elle ne
doit jamais être présentée comme un substitut fiable à une canne
blanche, un chien-guide ou une aide humaine.

------------------------------------------------------------------------

## 3. Expérience utilisateur --- exemple

**07:00 --- Briefing du matin**

AURA annonce :

> « Bonjour. Voici votre briefing du vendredi. Il fera 21 degrés
> aujourd'hui, avec un risque de pluie dans l'après-midi. Vous avez un
> rendez-vous à 14 h 30. Voici les trois actualités principales... »

Puis l'assistant demande :

> « Souhaitez-vous que je vous rappelle de préparer votre déplacement à
> 13 h 30 ? »

L'utilisateur répond « oui ». AURA crée le rappel et confirme
vocalement.

Cet exemple décrit l'expérience cible ; il ne signifie pas que toutes
ces intégrations sont déjà développées.

------------------------------------------------------------------------

## 4. Architecture technique envisagée

L'architecture est volontairement modulaire afin de pouvoir construire
et tester chaque fonctionnalité progressivement.

``` text
Application mobile accessible
        |
        v
Interface vocale
(Speech-to-Text / Text-to-Speech)
        |
        v
Backend API
        |
        v
Agent IA principal
(compréhension de l’intention et orchestration)
        |
        +---- Outil Actualités / RSS
        |
        +---- Outil Météo
        |
        +---- Outil Tâches et Agenda
        |
        +---- Outil Réservations
        |
        +---- Outil Communication
        |
        v
Base de données et préférences utilisateur
        |
        v
Réponse vocale / notification / demande de confirmation
```

### Stack technologique proposée

  -----------------------------------------------------------------------
  Couche                  Technologie envisagée   Rôle
  ----------------------- ----------------------- -----------------------
  Application mobile      Flutter                 Application Android/iOS
                                                  accessible

  Backend                 Python + FastAPI        API et logique métier

  Automatisation          n8n                     Workflows planifiés et
                                                  intégrations

  Base de données         Supabase / PostgreSQL   Comptes, tâches et
                                                  préférences

  Intelligence            API de modèle LLM       Compréhension et
  artificielle                                    synthèse

  Speech-to-Text          Whisper ou service      Conversion voix vers
                          équivalent              texte

  Text-to-Speech          Service TTS             Lecture vocale
                          configurable            

  Actualités              API d'actualités / flux Collecte des nouvelles
                          RSS                     

  Météo                   API météo               Conditions et
                                                  prévisions
  -----------------------------------------------------------------------

Les technologies pourront évoluer selon les coûts, la disponibilité des
API, la confidentialité et les contraintes des plateformes mobiles.

------------------------------------------------------------------------

## 5. Automatisation du briefing quotidien

Workflow cible :

``` text
Déclencheur planifié (heure choisie)
        |
        v
Récupérer les préférences utilisateur
        |
        +---- Récupérer les actualités
        |
        +---- Récupérer la météo
        |
        +---- Récupérer les tâches et rendez-vous
        |
        v
Vérifier et organiser les informations
        |
        v
Générer un résumé court avec l'IA
        |
        v
Convertir le texte en audio
        |
        v
Envoyer le briefing à l'application
        |
        v
Lecture audio selon les réglages de l'utilisateur
```

Le workflow devra gérer les erreurs : API indisponible, absence de
nouvelles pertinentes, données météo manquantes ou génération audio
échouée. L'assistant devra signaler clairement lorsqu'une information
n'a pas pu être vérifiée.

------------------------------------------------------------------------

## 6. MVP --- première version réalisable

Pour éviter un projet trop vaste, le premier prototype se concentrera
sur quatre fonctions :

1.  **Assistant vocal :** recevoir une commande, comprendre l'intention
    et répondre oralement.
2.  **Briefing quotidien :** combiner actualités, météo et agenda dans
    un résumé audio de 1 à 2 minutes.
3.  **To-do list vocale :** créer, consulter et terminer des tâches.
4.  **Rappels :** programmer et déclencher des rappels configurés par
    l'utilisateur.

Les réservations, appels, messages et fonctions de vision seront
développés dans des versions ultérieures, après validation du MVP.

------------------------------------------------------------------------

## 7. Feuille de route

-   [ ] Définir les besoins avec des personnes aveugles et malvoyantes.
-   [ ] Concevoir les parcours vocaux et les règles de confirmation.
-   [ ] Créer le squelette de l'application mobile.
-   [ ] Mettre en place le backend et la base de données.
-   [ ] Développer l'échange vocal.
-   [ ] Créer le workflow n8n du briefing quotidien.
-   [ ] Ajouter la gestion vocale des tâches.
-   [ ] Ajouter les rappels et notifications.
-   [ ] Tester avec des utilisateurs et corriger les problèmes
    d'accessibilité.
-   [ ] Étudier les intégrations de réservation et de communication.

------------------------------------------------------------------------

## 8. Sécurité, confidentialité et fiabilité

AURA peut traiter des informations personnelles, des rendez-vous et
potentiellement des données sensibles. La sécurité doit donc être
intégrée dès la conception.

Principes à respecter :

-   demander un consentement clair pour chaque intégration ;
-   collecter uniquement les données nécessaires ;
-   protéger les clés API côté serveur et ne jamais les publier dans le
    dépôt GitHub ;
-   chiffrer les données sensibles en transit et au repos lorsque la
    solution le permet ;
-   permettre à l'utilisateur de consulter et supprimer ses données ;
-   ne jamais effectuer une réservation, un paiement, un appel ou un
    envoi de message sensible sans confirmation explicite ;
-   annoncer les sources et la date des informations du briefing ;
-   ne pas inventer de nouvelles, de disponibilités ou de prévisions ;
-   prévoir des mécanismes d'annulation et de reprise en cas d'erreur.

AURA est un outil d'assistance. Il ne remplace pas les professionnels de
santé, les services d'urgence, les aides à la mobilité ni le jugement de
l'utilisateur.

------------------------------------------------------------------------

## 9. Accessibilité : une exigence centrale

L'accessibilité ne doit pas être ajoutée à la fin du développement.

Le produit devra être testé avec des utilisateurs concernés et viser
notamment :

-   une navigation compatible avec TalkBack et VoiceOver ;
-   des libellés accessibles pour tous les contrôles ;
-   une utilisation possible sans gestes visuels complexes ;
-   une structure de navigation cohérente ;
-   des annonces vocales courtes et compréhensibles ;
-   la possibilité de répéter, interrompre, ralentir ou couper la
    lecture ;
-   des confirmations explicites pour éviter les actions accidentelles.

Les tests avec des personnes aveugles et malvoyantes sont indispensables
pour valider les choix de conception.

------------------------------------------------------------------------

## 10. Développement avec le Vibe Coding

Le Vibe Coding sera utilisé pour accélérer :

-   la création des écrans et composants ;
-   la génération du backend ;
-   la mise en place des workflows n8n ;
-   les intégrations API ;
-   les tests et la documentation.

Toutefois, le code généré devra être relu, testé et sécurisé. Les
scénarios critiques --- permissions, données personnelles, réservations
et appels --- nécessitent une validation technique rigoureuse.

------------------------------------------------------------------------

## 11. Vision à long terme

À long terme, AURA ambitionne de devenir un compagnon numérique
personnel qui aide les personnes aveugles et malvoyantes à mieux
s'informer, organiser leurs journées, communiquer et accéder à des
services.

La réussite du projet sera mesurée non pas au nombre de fonctionnalités,
mais à son utilité réelle, sa fiabilité, son accessibilité et la
confiance de ses utilisateurs.

------------------------------------------------------------------------

## 12. Contribution et retours

Les retours de personnes aveugles et malvoyantes, d'associations, de
développeurs et de spécialistes de l'accessibilité seront essentiels.

Les contributions peuvent porter sur : - les besoins utilisateurs ; -
les parcours vocaux ; - les tests d'accessibilité ; - les intégrations
de services ; - la sécurité et la documentation.

------------------------------------------------------------------------

## Licence

Licence à définir avant toute diffusion publique du code.

------------------------------------------------------------------------

**Note :** ce dépôt présente la vision, les fonctionnalités envisagées
et l'architecture cible du projet. Il ne constitue pas encore une
application complète et opérationnelle. Les fonctions décrites comme
futures ou envisagées ne sont pas nécessairement implémentées.
