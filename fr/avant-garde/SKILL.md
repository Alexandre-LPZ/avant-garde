---
name: avant-garde
description: À utiliser dès que l'utilisateur veut créer, démarrer ou prototyper un site web, une application ou un SaaS (vibe coding), ou demande du code pour un nouveau projet web. Établit les 6 documents de fondation et la porte de sécurité avant toute écriture de code.
---

# Avant-Garde — les fondations avant le code, la garde avant la mise en ligne

*Think before you build. Guard before you ship.*

## Principe — le contrat humain-IA

Je ne code pas un projet neuf sans fondations écrites. Ce que l'humain ne décide pas, je le devine — et je le devine mal. Ces documents ne sont pas de la paperasse : ils sont **notre mémoire commune**. Chaque session est une instance neuve ; les documents sont ce qui fait que le binôme humain-IA reprend le travail exactement où il s'était arrêté, sans rien réinventer. Règle d'or : **ce qui n'est pas écrit n'existe pas.**

Ce skill assume sa méthode. Si l'utilisateur veut coder sans fondations, je le dis une fois, clairement : ce qu'il risque (base ouverte, clés exposées, projet irreprenable) contre la demi-heure que coûtent les documents. S'il insiste, la seule voie que j'accepte est un **prototype jetable** : étiqueté comme tel dans le code et le README, jamais branché sur de vraies données personnelles, jamais mis en ligne. Pour un projet qui touche des données d'autrui, je ne saute pas la porte de sécurité.

## Étape 1 — Triage (30 secondes)

Poser UNE question : « Ton projet aura-t-il des comptes utilisateurs, une base de données, un paiement ou un appel à une IA ? »
- **Non** (page/site statique, vitrine, portfolio) → **parcours léger** : 3 documents (01-produit, 03-design, 06-plan) + checks secrets/Git de la porte de sécurité.
- **Oui** → **parcours complet** : 6 documents + porte de sécurité intégrale, non négociable.

## Étape 2 — Interview, document par document

Dans l'ordre de dépendance : 01 → 02 → 03 → 04 → 05 → 06 (le plan dépend de tout le reste). Méthode :
- 5 questions maximum à la fois, en langage simple, zéro jargon non expliqué.
- Si je peux déduire une réponse de ce qui a été dit, je la propose et je demande confirmation.
- Je n'invente AUCUNE fonctionnalité, AUCUN chiffre, AUCUN outil non validé. En cas de doute : `[À CONFIRMER]` dans le document.
- Chaque document est écrit dans `docs/` dès que ses réponses sont complètes — jamais tout d'un coup.

## Étape 3 — Les 6 documents (ce que chacun contient)

### docs/01-produit.md (PRD) — ce qu'on construit
- Le produit en 3 phrases : pour qui, quel problème, ce qui le distingue.
- Les types d'utilisateurs et ce que chacun veut faire.
- Les fonctionnalités UNE PAR UNE avec priorité : indispensable v1 / souhaitable / plus tard. Une fonctionnalité = une action complète (« réserver une table »), pas une page.
- **Hors périmètre v1, écrit noir sur blanc** — c'est la ligne anti-dérive.
- 1-2 critères mesurables de réussite.
- Erreur classique à éviter : mélanger la v1 avec les rêves — je construis tout ce que je lis.

### docs/02-parcours.md (app flow) — ce qui se passe au clic
- Liste des pages, leur adresse, qui y accède (visiteur / connecté / admin).
- Un parcours clic-par-clic par fonctionnalité du PRD, du départ à la fin.
- **Les états qu'on oublie** : vide, chargement, erreur, succès, retour arrière.
- Règles de navigation (non-connecté qui clique sur une page privée → où ?).
- Erreur classique : ne décrire que le chemin heureux — la majorité des bugs vivent dans les états non écrits.

### docs/03-design.md — à quoi ça ressemble
- Couleurs en hexadécimal (fond, texte, accent, succès, erreur) — jamais « un orange chaleureux », toujours `#C2410C`.
- Polices (titres, texte), tailles de base, où les charger.
- Composants de base en 3 lignes chacun : bouton, carte, formulaire, message d'erreur.
- L'allure de chaque page décrite en mots : ce qu'on voit en premier, l'ordre des blocs. Référence visuelle si disponible.
- Le ton (tutoiement/vouvoiement, humour ou non).
- Erreur classique : « moderne, épuré, premium » — ces mots produisent le même site que tout le monde.

### docs/04-technique.md (TRD) — avec quoi on construit
- UN outil par besoin, figé : framework, base de données, auth, e-mails, hébergement — et pourquoi. Si l'utilisateur ne sait pas, je propose, il valide, on fige.
- Services externes et leurs limites gratuites (e-mails/jour, lignes en base) — écrites.
- Variables d'environnement par leur NOM uniquement (`SUPABASE_URL`, …). Les valeurs vivent dans `.env`, jamais dans ce document, jamais dans une conversation.
- Les interdits : pas de nouvelle dépendance sans accord, pas de changement de base en cours de route, pas de clé en dur.
- Erreur classique : trois outils pour un besoin, ou un outil choisi parce qu'une vidéo en parlait.

### docs/05-donnees.md (schéma back-end) — où vivent les données, qui les voit
- Les tables champ par champ, avec les liens entre elles.
- **Les droits, table par table** : qui lit, qui écrit, qui supprime — par rôle. C'est ce qui devient les règles de sécurité de la base.
- Chaque donnée personnelle marquée : pourquoi on la collecte, peut-on s'en passer, où elle est stockée (région — choisir l'Europe à la création du projet pour le RGPD), combien de temps on la garde et ce qui se passe à la fin.
- Le schéma se modifie par MIGRATIONS, jamais à la main.
- Erreur classique : laisser l'IA créer les tables au fil de l'eau sans règles d'accès → base ouverte où tout utilisateur connecté lit tout. Les droits s'écrivent avant la première table.

### docs/06-plan.md — quoi construire, dans quel ordre
- Des étapes qui tiennent chacune en une session. Trop grosse ? On coupe.
- Ordre des dépendances : squelette + design → auth → données → fonctionnalités (ordre du PRD) → paiement → **porte de sécurité** → mise en ligne.
- Pour chaque étape, UNE phrase vérifiable par l'utilisateur : « je réserve et je reçois l'e-mail ». Tant que ce n'est pas vrai, l'étape n'est pas finie.
- Les étapes finies sont figées : on les change par une nouvelle étape, pas par une retouche en passant.
- Erreur classique : « construis tout » en une session — personne n'a rien vérifié.

## Étape 4 — La porte de sécurité (bloquante avant mise en ligne)

Dix vérifications, chacune faisable par un non-développeur en quelques minutes. Je les intègre au fil des documents (05 surtout) et je les rejoue TOUTES à l'étape finale du plan. **Je ne déclare jamais un projet prêt pour la mise en ligne tant qu'une case n'est pas cochée.**

1. **Étape 0 Git** : `.gitignore` créé AVANT le premier commit, `.env` dedans. Scan des secrets avant chaque push. Une clé a fuité (même une fois, même effacée ensuite) → rotation immédiate.
2. **Sécurité ligne par ligne (RLS) activée sur CHAQUE table** — sans exception, même « temporaire ».
3. **Le test des deux comptes** : créer deux utilisateurs, vérifier que A ne voit JAMAIS les données de B — en forçant les URLs et les identifiants dans l'adresse, pas seulement en cliquant.
4. **Aucune clé admin/secrète côté navigateur.** Tout ce qui est préfixé « public » (ex. `NEXT_PUBLIC_`) est lisible par la planète entière ; la clé `service_role` ou équivalente ne quitte jamais le serveur.
5. **Validation côté serveur** de tout ce qui arrive : un formulaire qui vérifie dans le navigateur ne protège rien.
6. **Auth du service** (Supabase Auth, Clerk…), jamais bricolée maison, jamais un simple jeton posé en localStorage par nos soins.
7. **CORS fermé** : la liste des domaines autorisés, jamais `*` en production.
8. **Si paiement** : signature de chaque webhook vérifiée — sinon n'importe qui peut déclarer des paiements.
9. **Si l'app appelle une IA** : rate limit obligatoire sur ces routes — une route IA sans limite, c'est la carte bleue du créateur en libre-service.
10. **Chasse finale** : aucun TODO/FIXME laissé par l'IA dans le code, aucun `console.log` de données personnelles, les routes admin protégées.

## Étape 5 — Clôture des fondations : le CLAUDE.md

Quand les documents sont complets, j'écris un `CLAUDE.md` à la racine qui : renvoie aux documents de `docs/`, interdit de coder une fonctionnalité absente du PRD, interdit de changer un outil figé dans le TRD, et rappelle la porte de sécurité. C'est lui qui fait respecter les fondations aux sessions suivantes sans que l'utilisateur recolle quoi que ce soit.

## Étape 6 — Construction

- **Une étape du plan par session, jamais plus.** Avant de commencer : résumer en 5 lignes ce que je vais faire et ce que je ne toucherai pas.
- Une fonctionnalité me semble manquer ? Je la note dans `docs/a-discuter.md`, je ne la code pas.
- Fin d'étape : la liste exacte de ce que l'utilisateur doit vérifier. **Si un outil navigateur est disponible (Playwright MCP, navigateur intégré…), je teste moi-même dans le navigateur avant de rendre la main** ; sinon je fournis les clics à faire.
- Jamais d'auto-validation sans preuve : une étape est finie quand sa phrase de vérification est vraie, pas quand le code compile.

## Documents vivants

L'utilisateur change d'avis → **le document d'abord, le code ensuite**. Je dis quels documents je mets à jour et pourquoi, puis je vérifie que 06-plan.md reste cohérent. Signe que ça marche : on reprend le projet après deux semaines et on sait tout en dix minutes de relecture. Signe que ça ne marche plus : on m'explique le projet dans le prompt au lieu de me montrer les documents.
