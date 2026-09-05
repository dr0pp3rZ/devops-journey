# 🚀 DevOps Journey 2026

**Старт:** 5 сентября 2026
**Цель:** Middle DevOps / Platform Engineer за 6 месяцев
**Темп:** 6+ часов/день
**Канал:** [t.me/devops_journey_dr0pp3r](https://t.me/devops_journey_dr0pp3r)
**GitHub:** https://github.com/dr0pp3rZ/devops-journey

---

## Что это

Публичный лог обучения. Каждый день — коммит. Каждую неделю — отчёт. Каждый месяц — ретроспектива.

Вилка через 6 мес: 250–350 тыс ₽ (РФ) / €60–85k (EU remote) / фриланс.

---

## Целевая вакансия

```
Middle DevOps / Platform Engineer
- Kubernetes (CKA) + Helm + GitOps
- Terraform / OpenTofu
- GitLab CI/CD
- Python + Bash automation
- Observability: Prometheus + Grafana + Loki
- Linux, Docker, Ansible
```

---

## Roadmap (26 недель)

| Phase | Нед | Тема | Артефакт | Сертификация |
|---|---|---|---|---|
| 0 | 1–2 | Linux + Git + сети | VM + nginx + TLS | — |
| 1 | 3–5 | Docker + Python | docker-utils | — |
| 2 | 6–9 | CI/CD + Terraform | pipeline push→apply | **HashiCorp TA-003** |
| 3 🔥 | 10–16 | **Kubernetes** | 3-нодовый кластер | **CKA** |
| 4 | 17–19 | Observability + SRE | observability-стек | **PCA**  |
| 5 | 20–23 | Platform Engineering | IDP-прототип | **AWS SAA-C03** |
| 6 | 24–26 | AI/LLM Ops | 2 AI-проекта | **AWS MLA-C01** |

Подробный визуальный план — в Obsidian canvas: `01_Projects/devops-journey-2026.canvas`.

---

## Методики

1. **Learn → Build → Teach** — теория 1ч, практика 2–3ч, объяснение 30 мин
2. **Anki daily** — 20–30 мин/день, retention 85%+
3. **Публичный коммит каждый день**
4. **Error journal** — каждая поломка в `00-journal/error-journal.md`
5. **Disaster Friday** — ломаю кластер намеренно, чиню, записываю
6. **Interleaving** — чередование k8s / Terraform / Python

---

## Структура репо

```
devops-journey/
├── 00-journal/         # weekly reviews, error journal
├── 01-linux/           # Phase 0
├── 02-docker/          # Phase 1
├── 03-cicd/            # Phase 2
├── 04-terraform/       # Phase 2
├── 05-k8s/             # Phase 3 (ядро)
├── 06-observability/   # Phase 4
├── 07-gitops/          # Phase 5
├── 08-ai-ops/          # Phase 6
├── 09-go/              # bonus
├── assets/             # anki-deck.md, anki .tsv
├── CHANGELOG.md
└── README.md
```

---

## Anki

Файл для импорта: `assets/devops-2026.tsv` (20 карточек).

Импорт: Anki → File → Import → выбрать TSV → Note type: Basic → Fields: Tab → Deck: `devops-2026`. Включить маппинг 3 полей (Front, Back, Tags). Allow HTML in fields: ON.

---

## Связанные ресурсы

- Рабочая директория: `~/projects/devops-journey/`
- Obsidian canvas: `01_Projects/devops-journey-2026.canvas`
- Obsidian project note: `01_Projects/devops-journey-2026.md`
- Command Center: `00_Command_Center/Active.md`

---

## Публичное обещание

Беру обязательство за 6 месяцев (до 5 марта 2027) вырасти до уровня Middle DevOps / Platform Engineer. Буду публиковать прогресс в [t.me/devops_journey_dr0pp3r](https://t.me/devops_journey_dr0pp3r) и здесь. Каждый день — минимум 1 коммит. Каждую неделю — отчёт. Каждый месяц — ретроспектива.
