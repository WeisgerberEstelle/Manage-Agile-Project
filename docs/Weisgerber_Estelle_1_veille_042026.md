# 🔍 Veille technologique ciblée - Projet CATASTERRE

## Présentation

### Justification du choix des 4 thématiques

| Thématique | Justification |
|------------|---------------|
| **Architectures applicatives** | Directement liée à US5 (Docker) + US6 (µS) : chantier majeur du backlog. |
| **Performance applicative** | Réponse aux lenteurs signalées par les clients + KPI « temps de chargement < 2 s ». |
| **Gestion de la dette technique** | Réponse à la complexité du code mentionnée dans la mission. |
| **Tests Full-Stack** | Réponse au point bloquant remonté par Rachida (manque compétences testing) + KPI couverture. |

> **NB :** Dans le cadre de cette veille, certains choix se sont portés sur des publications de Martin Fowler plutôt que sur des articles plus récents identifiés lors des recherches. Ces derniers s'appuient en effet largement sur ses travaux fondateurs, dont ils constituent essentiellement des reprises ou des vulgarisations.

---

## 1. Architectures applicatives

**Objectif :** Comparer les approches monolithe modulaire / micro-services

| Approche | Source | Date | Synthèse + comparaison | Apport CATASTERRE |
|----------|--------|------|------------------------|-------------------|
| Monolithe modulaire - contre-courant | [Martin Fowler - MonolithFirst](https://martinfowler.com/bliki/MonolithFirst.html) | [2015 / Position toujours débattue dans cet article 2024](https://medium.com/@mehmetozkaya/starting-point-for-microservices-modular-monoliths-gradually-transition-with-incremental-0e8f6a147e36) | Argumentaire contre la migration µS prématurée. Recommande de partir d'un monolithe modulaire avant de découper. Le coût d'un µS prématuré dépasse souvent le bénéfice. | Justifie potentiellement de **NE PAS migrer US6** et d'opter pour un monolithe modulaire intermédiaire. À arbitrer en Spike S3. |
| État de l'art trimestriel | [ThoughtWorks Technology Radar](https://www.thoughtworks.com/radar) | 2024 / Trimestriel | Positionne les outils en Adopt / Trial / Assess / Hold. Compare µS vs serverless vs event-driven vs modular monolith. | Argument neutre pour le comité projet : choix d'architecture appuyé par un analyste reconnu. |

---

## 2. Performance applicative

**Objectif :** Adresser les lenteurs signalées par les clients : leviers front, back.

| Approche | Source | Date | Synthèse + comparaison | Apport CATASTERRE |
|----------|--------|------|------------------------|-------------------|
| Signals (modèle réactif moderne) | [Angular Guide - Signals](https://angular.dev/guide/signals) | 2026 - Angular v21 | Doc officielle qui explique comment le modèle Signals d'Angular permet de mettre à jour uniquement les composants concernés par un changement de donnée plutôt que toute l'application. | Cadre pour atteindre la cible KPI « temps de chargement < 2 s ». Cohérent avec la mesure Lighthouse déjà prévue. Si l'audit Lighthouse confirme que les lenteurs viennent du runtime côté front et non du réseau ou du back. |
| Performance pipeline CI - caching Gradle | [Gradle Caching Reduced Spring Boot CI Time by 65%](https://medium.com/@codingplainenglish/gradle-caching-reduced-spring-boot-ci-time-by-65-bf2109fe1988) | 2026 | Compare une CI Spring Boot sans cache (18-20 min/build, dont 4-5 min de download Maven Central) vs avec Gradle dual-cache (dépendances + build cache) → 6-7 min/build (**-65 %**). | Levier direct pour le KPI « durée pipeline CI < 10 min ». Si on retient Gradle pour le build Spring Boot, Rachida peut paramétrer le dual-cache dès US7. Retour d'expérience chiffré utile en comité projet. |

---

## 3. Gestion de la dette technique

**Objectif :** Adresser la complexité du code mentionnée dans la mission, sans big bang.

| Approche | Source | Date | Synthèse + comparaison | Apport CATASTERRE |
|----------|--------|------|------------------------|-------------------|
| Refactor techniques | [Code Refactoring in 2025: Best Practices & Popular Techniques](https://marutitech.medium.com/best-practices-code-refactoring-19c81263ac43) | 2024 | Article qui présente les bénéfices, les moments clés et six techniques populaires de refactoring de code pour améliorer la lisibilité, la maintenabilité et la performance d'une base de code sans en modifier le comportement externe. | Stratégie applicable à notre code complexe : nettoyage continu pendant les sprints (code review + DoD). |
| Pattern de migration | [Martin Fowler - Strangler Fig Application](https://martinfowler.com/bliki/StranglerFigApplication.html) | [2004 - Toujours actuel (article 2026)](https://medium.com/@ravipatel.it/defeat-the-monolith-your-guide-to-the-strangler-fig-migration-pattern-74fe4e2fd394) | Migration progressive : on remplace les fonctionnalités du monolithe par des services neufs sans big bang. Compare avec l'approche « rewrite ». | Croisement avec US6 : la dette du monolithe peut être traitée en parallèle de la migration plutôt qu'en étape préalable. |

---

## 4. Tests Full-Stack

**Objectif :** Combler le manque de compétences testing remonté par Rachida + atteindre les KPIs.

| Approche | Source | Date | Synthèse + comparaison | Apport CATASTERRE |
|----------|--------|------|------------------------|-------------------|
| Cadre méthodologique | [Medium - Testing Pyramid and Testing Ice Cream Cone \| What is the difference?](https://medium.com/@k-hartanto/testing-pyramid-and-testing-ice-cream-cone-what-is-the-difference-6ddde3876c20) | 2023 | Équilibre tests unitaires / intégration / E2E. Compare la pyramide saine (base unitaire large) vs « ice cream cone » (trop d'E2E, lent et fragile). | Cadre de répartition de l'effort : Jest (front, base large), JUnit (back, base large), Cypress (E2E, sommet réduit). |
| Front - Jest vs Karma vs Vitest | [Angular Blog - Testing](https://medium.com/javascript-in-plain-english/leaving-karma-and-jest-behind-an-architectural-shift-in-angular-21-testing-2e5576f4dd8d) | MAJ continue | Karma déprécié dans Angular 17+. Compare Jest (mature, écosystème large) vs Vitest (plus rapide, ESM natif). | Décision pour Dimitry : Jest reste le plus sûr (formation F1 alignée). Vitest à évaluer en Spike futur. |
