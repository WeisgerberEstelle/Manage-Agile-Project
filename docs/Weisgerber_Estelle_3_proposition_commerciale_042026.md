# Projet évolution d'application
## Proposition commerciale

**Table des matières**

- [1. Contexte](#1-contexte) 
  - [1.1 Contexte global](#11-contexte-global)
  - [1.2 Fonctionnalités métier](#12-fonctionnalités-métier)
- [2. Réalisation du projet](#2-réalisation-du-projet)
  - [2.1 Définition des tâches techniques](#21-définition-des-tâches-techniques-par-epic)
  - [2.2 Gestion des points de complexité](#22-gestion-des-points-de-complexité)
  - [2.3 Coûts](#23-coûts)
  - [2.4 Risques identifiés](#24-risques-identifiés)
  - [2.5 Définition des objectifs de performance](#25-définition-des-objectifs-de-performance)
  - [2.6 Impact environnemental](#26-impact-environnemental)
- [3. Synthèse](#3-synthèse)
---

## 1. Contexte

### 1.1 Contexte global

**CATASTERRE** est une entreprise spécialisée dans la **visualisation de catastrophes naturelles via imagerie satellite**. Elle fournit une application web destinée aux **notaires et agences immobilières** pour évaluer les risques (inondations, séismes, zones nucléaires…) liés à des biens immobiliers.

**Problématique :** Lancée il y a moins d'un an, l'application souffre de :
- Lenteurs, erreurs fréquentes, instabilités signalées par les clients
- Code complexe, architecture difficile à faire évoluer
- Manque de roadmap technique claire

La direction lance un projet structurant d'évolution de l'application avec **trois objectifs produit** :

1. **Améliorer l'expérience utilisateur** (UX, accessibilité),
2. **Garantir la disponibilité** et améliorer la maintenabilité / évolutivité du produit,
3. **Fiabiliser l'organisation du développement** (CI/CD, environnement de test).

Le pilotage est confié à un Expert en développement logiciel, chargé d'encadrer l'équipe technique et de poser un cadre méthodologique Scrum clair afin de maîtriser coûts, délais et compétences.

| Membre | Rôle | Expertise |
|--------|------|-----------|
| **Estelle** | Expert dev / Chef de projet | Pilotage agile, coordination, dev d'appoint |
| **Dimitry** | Dev Front-end (3 ans) | Angular, RxJS, HTML/CSS/JS |
| **Rachida** | DevOps / Back (5 ans) | Java/Spring Boot, Docker, K8s, CI, AWS, OpenShift, MySQL |
| **Jorge** | UX Designer (12 ans) | Figma, Miro, wireframes, accessibilité |

### 1.2 Fonctionnalités métier

| # | Fonctionnalité | Description | Statut |
|---|----------------|-------------|--------|
| F1 | Visualisation des images satellites | Affichage interactif d'imagerie satellite haute résolution permettant aux utilisateurs de consulter visuellement les zones étudiées | Existant à fiabiliser |
| F2 | Évaluation des risques liés à un bien immobilier | Identification des risques (zones inondables, risques sismiques, périmètres nucléaires, etc.) associés à un bien | Existant - cœur de métier |
| F3 | Calcul du risque d'inondation | Calcul d'un score d'exposition au risque d'inondation, enrichi par l'intégration de sources de données géographiques officielles | Évolution - US9 |
| F4 | Génération d'un rapport au format PDF | Production d'un rapport synthétique d'analyse exploitable comme pièce d'un dossier client | Évolution - US11 |
| F5 | Export des données d'analyse au format CSV | Export des données brutes d'analyse pour traitement externe | Évolution - US11 |

---

## 2. Réalisation du projet

L'organisation est pensée en mode Scrum, par sprints de 2 semaines, avec une capacité de 15 story points / sprint maximum (vélocité plafond imposée, à recalibrer après le Sprint 1).

### 2.1 Définition des tâches techniques par epic

| US | Périmètre technique | Compétences mobilisées |
|----|---------------------|------------------------|
| **UX & Accessibilité** | | |
| US1 - Style CSS | Audit CSS global, refonte des fontes et de la palette, harmonisation visuelle | Front + UX |
| US2 - Messages d'erreur | Refonte du mapping des erreurs front ↔ back, messages utilisateurs explicites | Front + Back |
| US3 - Accessibilité | Audit WCAG AA, corrections sémantiques navigation clavier, contrastes, lecteur d'écran | Front + UX |
| US10 - Compatibilité navigateurs | Polyfills, tests cross-browser, ajustements CSS | Front |
| US4 - Nouveau thème (dépriorisé) | Architecture de thèmes, sélecteur, persistance utilisateur | Front + UX |
| **Architecture & Disponibilité** | | |
| US6 - Architecture micro-services | Spike préalable, découpage des bounded contexts, communication inter-services | DevOps + Back |
| US12 - Étude architecture micro-services | Cartographie des bounded contexts, comparatif d'architectures cibles | DevOps + Back |
| **Qualité & DevOps** | | |
| US5 - Conteneurisation Docker | Dockerfile, docker-compose, documentation de build et de run | DevOps |
| US7 - Pipeline CI | Mise en place GitHub Actions / Jenkins, intégration des tests, notifications | DevOps |
| US8 - Environnement de test | Infra séparée de la prod, BDD de test, déploiement automatisé, sécurisation | DevOps + Back |
| **Métier & Fonctionnalités** | | |
| US9 - Calcul risque inondation | Algorithme, intégration de sources de données externes, validation métier | Back + Métier |
| US11 - Export des données | Génération PDF/CSV, templates, gestion des volumes | Back + Front |

### 2.2 Gestion des points de complexité

**Méthode d'estimation**

Estimation sur la suite de Fibonacci (1, 2, 3, 5, 8, 13). Un story point mesure la complexité relative (technique + effort + incertitude), pas une durée. US de référence : **US2 = 3 pts** (effort faible, périmètre cadré).

Chaque US a été estimée en deux temps : une première passe par analogie avec l'US de référence, puis un Planning Poker avec un second expert technique pour croiser les points de vue et lever les biais. Les écarts ont été discutés jusqu'à convergence.

Marges appliquées selon l'incertitude : **+15 %** (cadré), **+20 %** (transverse), **+25 %** (forte incertitude ou dépendance externe).

| US | Complexité (SP) | Est. temps | Marge | Justification |
|----|-----------------|------------|-------|---------------|
| US1 - Style CSS | 5 | 4,5 j | +15 % | Audit + refactor + tests visuels, cadré |
| US2 - Messages d'erreur | 3 | 3 j | +15 % | Pas de surprise technique |
| US3 - Accessibilité (A11Y) | 8 | 7 j | +20 % | Transverse à toute l'app |
| US4 - Nouveau thème | 5 | 4 j | +15 % | Architecture + sélecteur + persistance |
| US5 - Docker | 5 | 4 j | +15 % | Compétences présentes dans l'équipe |
| US6 - Micro-services ⚠️ | 10 ⚠️ | 11 j | +25 % | Chantier majeur, à découper après spike |
| US7 - Pipeline CI | 5 | 4 j | +15 % | Compétences CI présentes |
| US8 - Environnement de test | 8 | 7 j | +20 % | Dépend de US5 + US7 |
| US9 - Calcul inondation | 8 | 8 j | +25 % | Forte incertitude sur les sources |
| US10 - Compatibilité navigateurs | 3 | 2,5 j | +15 % | Polyfills + cross-browser |
| US11 - Export PDF/CSV | 5 | 5 j | +15 % | Effort modéré |
| US12 - Spike - Étude µS | 3 | 3 j | | Étude préalable à US6 |
| Coordination + rituels | | 6 j (1/sprint) | | Animation des rituels Scrum (daily, planning, review, rétro) + suivi backlog + levée des points bloquants. ~10 % du sprint. |
| **Total backlog** | **68 SP** | **~69 j** | | |

### 2.3 Coûts

| Profil | Séniorité | TJM | Justification |
|--------|-----------|-----|---------------|
| Estelle (CP / Expert dev) | Senior | 550 € | Double casquette pilotage + dev senior |
| Rachida (DevOps / Back Java) | 5 ans | 500 € | Profil DevOps confirmé, compétences valorisées sur le marché |
| Dimitry (Front Angular) | 3 ans | 450 € | Profil front confirmé, stack Angular/RxJS |
| Jorge (UX Designer) | 12 ans | 400 € | UX senior mais intervention ponctuelle, pas de dev |

**Tableau de synthèse par sprint**

| User Story | Membre | Temps | TJM | Total |
|------------|--------|-------|-----|-------|
| **SPRINT 1** | | | | |
| US1 - Amélioration du style CSS | Jorge | 1 j | 400 € | |
| | Dimitry | 3 j | 450 € | 2 025 € |
| | Estelle | 0,5 j | 550 € | |
| US2 - Gestion des messages d'erreur | Dimitry | 2 j | 450 € | |
| | Rachida | 0,5 j | 500 € | 1 350 € |
| | Jorge | 0,5 j | 400 € | |
| US5 - Encapsuler l'application Docker | Rachida | 3,5 j | 500 € | 2 025 € |
| | Estelle | 0,5 j | 550 € | |
| Coordination + rituels Scrum | Estelle | 1 j | 550 € | 550 € |
| **Sous-total** | | **12,5 j** | | **5 950 €** |
| **SPRINT 2** | | | | |
| US3 - Accessibilité A11Y | Dimitry | 5,5 j | 450 € | 3 075 € |
| | Jorge | 1,5 j | 400 € | |
| US7 - Pipeline d'intégration continue | Rachida | 4 j | 500 € | 2 000 € |
| Coordination + rituels Scrum | Estelle | 1 j | 550 € | 550 € |
| **Sous-total** | | **12 j** | | **5 625 €** |
| **SPRINT 3** | | | | |
| US8 - Environnement de test | Rachida | 6 j | 500 € | 3 275 € |
| | Estelle | 0,5 j | 550 € | |
| US10 - Compatibilité navigateurs | Dimitry | 2 j | 450 € | 1 100 € |
| | Jorge | 0,5 j | 400 € | |
| US12 - Spike - Étude micro-services | Rachida | 1,5 j | 500 € | 1 575 € |
| | Estelle | 1,5 j | 550 € | |
| Coordination + rituels Scrum | Estelle | 1 j | 550 € | 550 € |
| **Sous-total** | | **13 j** | | **6 500 €** |
| **SPRINT 4** | | | | |
| US6 - Migration micro-services | Rachida | 8 j | 500 € | 5 350 € |
| | Dimitry | 3 j | 450 € | |
| Coordination + rituels Scrum | Estelle | 1 j | 550 € | 550 € |
| **Sous-total** | | **12 j** | | **5 900 €** |
| **SPRINT 5** | | | | |
| US4 - Créer un nouveau thème | Dimitry | 3,5 j | 450 € | 1 775 € |
| | Jorge | 0,5 j | 400 € | |
| US9 - Calcul du risque d'inondation | Rachida | 6 j | 500 € | 4 100 € |
| | Estelle | 2 j | 550 € | |
| Coordination + rituels Scrum | Estelle | 1 j | 550 € | 550 € |
| **Sous-total** | | **13 j** | | **6 425 €** |
| **SPRINT 6** | | | | |
| US11 - Export des données | Jorge | 1 j | 400 € | |
| | Rachida | 3 j | 500 € | 2 350 € |
| | Dimitry | 1 j | 450 € | |
| Coordination + rituels Scrum | Estelle | 1 j | 550 € | 550 € |
| **Sous-total** | | **6 j** | | **2 900 €** |
| **TOTAL PROJET** | | **69 j** | | **33 300 €** |

68 SP avec une vélocité plafond de 15 SP/sprint imposent un minimum de 5 sprints. Un sixième sprint est ajouté pour absorber l'incertitude sur l'US6 et préserver une marge en cas de vélocité réelle inférieure (cf. risque R1). Le plafond des 15 SP ne permet pas aux membres de l'équipe de travailler à 100% du temps sur tous les sprints. Le reste du temps des sprints est dédié à la formation (testing, éco-conception), et la maintenance.

### 2.4 Risques identifiés

| # | Risque | Probabilité | Impact | Criticité | Parade |
|---|--------|-------------|--------|-----------|--------|
| R1 | Vélocité réelle inférieure aux 15 pts | Forte | Moyen | **Critique** | Recalibrer après Sprint 1, ajuster le périmètre des sprints suivants |
| R2 | Échec du plan de formation testing (montée en compétences insuffisante) | Moyenne | Fort | **Critique** | Formation animée par le CP, binôme sur les premiers tests, suivi de la couverture sprint après sprint |
| R3 | Indisponibilité prolongée de Rachida (maladie, départ, congés) + bus factor | Faible | Fort | Modéré | Documentation systématique, binôme Rachida ↔ Estelle sur les tâches critiques, ne pas concentrer le chemin critique sur une seule personne |
| R4 | Surcharge du chef de projet | Forte | Moyen | Modéré | Déléguer le développement au maximum, prioriser le pilotage |
| R5 | Périmètre micro-services (US6) sous-estimé | Moyenne | Fort | **Critique** | Spike technique préalable au Sprint 3, découpage progressif après spike |
| R6 | Régressions en production (pas d'environnement de test) | Forte | Fort | **Critique** | Prioriser US7 (CI) + US8 (environnement de test) dans les premiers sprints |
| R7 | Indisponibilité des sources de données externes (US9) | Faible | Moyen | Faible | Cache + mode dégradé, choix de sources publiques stables (Géorisques, IGN) |
| R8 | Sécurité du projet (vulnérabilités applicatives, fuite de données clients, dépendances obsolètes, secrets exposés) | Moyenne | Fort | **Critique** | Analyse de faille SAST/DAST intégrée à la CI (US7), audit des dépendances (npm audit, Dependabot), gestion des secrets via variables d'environnement, revue de code systématique, conformité OWASP Top 10 |
| R9 | Dépassement du temps de développement estimé (charges sous-évaluées, imprévus techniques, congés/maladies) | Moyenne | Fort | **Critique** | Suivi du burndown et de la vélocité à chaque sprint, revue d'estimation en Sprint Review, marge de sécurité sur les US complexes (US6, US9) |

**Matrice Probabilité × Impact**

|  | Impact Faible | Impact Moyen | Impact Fort |
|---|---|---|---|
| **Probabilité Forte** | — | R1, R4 | R6 |
| **Probabilité Moyenne** | — | | R2, R5, R8, R9 |
| **Probabilité Faible** | — | R7 | R3 |

**Légende**
- 🔴 **Critique** - action immédiate requise
- 🟠 **Modéré** - à surveiller
- 🟢 **Faible** - acceptable

### 2.5 Définition des objectifs de performance

| KPI | Cible | Dimension | Outil de mesure |
|-----|-------|-----------|------------------|
| Score Lighthouse A11Y | ≥ 95 / 100 | UX / Accessibilité | Lighthouse |
| Couverture de tests | ≥ 70 % back / ≥ 50 % front | Qualité | JaCoCo / Istanbul |
| Uptime de l'application | ≥ 99.5 % | Disponibilité | Monitoring serveur |
| Vélocité moyenne de l'équipe | ≥ 12 pts / sprint | Pilotage équipe | Outil de gestion backlog |
| Durée de la pipeline CI | < 10 minutes | Processus DevOps | Logs GitHub Actions |

### 2.6 Impact environnemental

CATASTERRE manipule des données volumineuses (imagerie satellite, cartographie). L'éco-conception est intégrée dès le développement, sans surcoût.

**Cibles KPI**

| Indicateur | Cible | Outil |
|------------|-------|-------|
| Éco-score EcoIndex | ≥ B (≥ 70/100) | EcoIndex / ecoindex-cli |
| Poids moyen d'une page | < 1 Mo | Lighthouse |
| gCO₂ par visite | < 1 g | Website Carbon |
| Durée builds CI / semaine | < 5 h | GitHub Actions |

**Actions clés**

La majorité des actions est sans surcoût, et sont intégrées au développement :

| Action | Portée |
|--------|--------|
| Optimisation assets (WebP, lazy-loading, cache navigateur) | Front-end |
| CI sobre : builds incrémentaux + cache dépendances | DevOps |
| Env. de test éteint hors heures ouvrées | Infra |
| Compression (et éventuellement tuilage) des images satellites | Back-end |
| Hébergement bas carbone (Scaleway / OVHcloud) ⚠️ +10 % infra | Infra |

---

## 3. Synthèse

**Résumé et propositions chiffrées**

En l'absence de budget initial défini, nous proposons deux scénarios. La Proposition 1 (MVP) couvre les fonctionnalités indispensables pour un investissement maîtrisé. La Proposition 2 (Backlog complet) livre l'ensemble des améliorations identifiées pour un impact durable sur la qualité, la scalabilité et la satisfaction client.

### Proposition 1 - MVP

| Critère | Détail |
|---------|--------|
| Périmètre | US1 (CSS) + US2 (Erreurs) + US3 (A11Y) + US5 (Docker) + US7 (Pipeline CI) |
| Story points | 26 pts |
| Durée | 2 sprints - 4 semaines |
| Charge totale | 24.5 jours/homme |
| **Coût estimé** | **11 575 €** |
| Ce qu'on livre | Interface corrigée, accessibilité WCAG AA, application conteneurisée, pipeline CI opérationnelle |
| Ce qu'on ne livre pas | Environnement de test, micro-services, nouveau thème, export données, calcul inondation amélioré |

### Proposition 2 - Backlog complet

| Critère | Détail |
|---------|--------|
| Périmètre | 11 User Stories + 1 Spike technique (backlog intégral) |
| Story points | 68 pts |
| Durée | 6 sprints - 12 semaines |
| Charge totale | 69 jours/homme |
| **Coût estimé** | **33 300 €** |
| Ce qu'on livre | Tout le périmètre MVP + environnement de test dédié, architecture micro-services, nouveau thème, calcul de risque amélioré, export PDF/CSV |

### Comparatif des deux propositions

| | Proposition 1 - MVP | Proposition 2 - Complète |
|---|---|---|
| Périmètre | 5 US (Must) | 11 US + 1 Spike |
| Durée | 4 semaines | 12 semaines |
| **Coût** | **11 575 €** | **33 300 €** |
| UX corrigée | ✅ | ✅ |
| Accessibilité | ✅ | ✅ |
| Docker | ✅ | ✅ |
| Pipeline CI | ✅ | ✅ |
| Environnement de test | ❌ | ✅ |
| Micro-services | ❌ | ✅ |
| Compatibilité navigateurs | ❌ | ✅ |
| Nouveau thème | ❌ | ✅ |
| Calcul inondation amélioré | ❌ | ✅ |
| Export PDF / CSV | ❌ | ✅ |
