# CATASTERRE - Agile Project Management Case Study


## Context

**CATASTERRE** is a fictional company providing a web application for visualizing natural disasters via satellite imagery. The application is used by notaries and real estate agencies to assess risks (floods, earthquakes, nuclear zones) associated with properties.

Launched less than a year ago, the application suffers from performance issues, frequent errors, a complex codebase, and a lack of technical roadmap. This project addresses three product objectives:

1. Improve user experience (UX, accessibility)
2. Guarantee availability and improve maintainability / scalability
3. Strengthen the development organization (CI/CD, test environment)

## Role

Expert Software Developer / Project Manager : responsible for leading the technical team and establishing a clear Scrum framework to manage costs, deadlines, and skills.

## Team

| Member | Role | Experience |
|--------|------|------------|
| Estelle | Expert dev / Project Manager | Agile leadership + development |
| Dimitry | Front-end Developer | 3 years - Angular, RxJS |
| Rachida | Back-end / DevOps Developer | 5 years — Java/Spring, Docker, K8s, CI |
| Jorge | UX Designer | 12 years - Figma, accessibility |

## Deliverables

| # | Document | Description |
|---|----------|-------------|
| 1 | [Technology watch](docs/01-veille.md) | Targeted watch on 4 themes: architectures, performance, technical debt, full-stack testing |
| 2 | [Commercial proposal](docs/02-proposition-commerciale.md) | Two scenarios (MVP / full backlog), estimation, risks, KPIs, environmental impact |
| 3 | [Steering committee deck](docs/03-support-coproj.md) | Sprint planning, blockers, evolving Definition of Done, risk matrix, training plan |

## Methods and Frameworks

- **Scrum** — 2-week sprints, velocity capped at 15 SP
- **Fibonacci** estimation (1, 2, 3, 5, 8, 13) with Planning Poker
- **MoSCoW** prioritization (Must / Should / Could / Won't)
- **Evolving Definition of Done** — progressive maturity across sprints
- **Risk matrix** Probability × Impact with mitigation strategies
- **Eco-design** integrated from development (EcoIndex, Lighthouse)

## Project KPIs

| KPI | Target | Tool |
|-----|--------|------|
| Lighthouse Accessibility score | ≥ 95 / 100 | Lighthouse |
| Test coverage | ≥ 70% back / ≥ 50% front | JaCoCo / Istanbul |
| Application uptime | ≥ 99.5% | Server monitoring |
| Average team velocity | 15 pts / sprint | Backlog management tool |
| CI pipeline duration | < 10 minutes | GitHub Actions logs |
| EcoIndex score | ≥ B (≥ 70 / 100) | EcoIndex / ecoindex-cli |


## Key Figures

- **6 sprints** over 12 weeks
- **68 story points** of backlog
- **69 person-days** of effort
- **€33,300** estimated total cost (full proposal)
- **€11,575** for MVP scenario (5 US, 4 weeks)

## License

Educational project - content provided for portfolio review purposes.
