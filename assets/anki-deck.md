# 🃏 Anki колода: devops-2026

> Импорт: Anki → File → Import → выбрать этот файл → Note type: Basic.

| Front | Back | Tags |
|---|---|---|
| Что такое PID 1 в Linux и зачем его менять? | PID 1 — первый процесс, init. Отвечает за запуск всех остальных. Меняют через systemd: замена PID 1 = замена системы инициализации (init → systemd, init → runit). | phase0 linux |
| В чём разница между TCP и UDP? | TCP — с установлением соединения, гарантия доставки, handshake (SYN, SYN-ACK, ACK), ordered. UDP — без соединения, без гарантий, быстрее. TCP для HTTP/SSH, UDP для DNS/VoIP/видео. | phase0 network |
| Что такое DNS и как работает резолвинг? | DNS — Domain Name System, переводит имена (google.com) в IP (142.250.190.46). Резолвинг: проверка /etc/hosts → рекурсивный запрос к резолверу (8.8.8.8) → корневые серверы → TLD (.com) → authoritative сервер. Кэшируется по TTL. | phase0 network |
| Что происходит при HTTPS handshake (TLS 1.3)? | 1) ClientHello (cipher suites, key share). 2) ServerHello + certificate + key share. 3) Клиент проверяет сертификат через CA. 4) Обмен ключами (X25519). 5) Зашифрованный канал. 0-RTT возможен. 1-RTT обычно. | phase0 network |
| В чём разница между git merge и git rebase? | merge — сохраняет историю веток, делает merge commit. rebase — переписывает историю, коммиты становятся линейными. Золотое правило: rebase только для локальных/feature-веток, никогда для shared/main. | phase0 git |
| Что делает git cherry-pick? | Берёт один конкретный коммит из другой ветки и применяет его к текущей. Используется для бэкпорта фикса из main в release-ветку. | phase0 git |
| В чём разница между Docker image и container? | Image — неизменяемый blueprint (слои FS + метаданные). Container — запущенный экземпляр image (image + writable layer + процесс). Один image → много контейнеров. | phase1 docker |
| Что такое multi-stage build и зачем он нужен? | Несколько FROM в одном Dockerfile. Первый этап — сборка (с dev-зависимостями, ~1GB). Второй — копирует артефакт в чистый runtime (alpine, ~50MB). Итог: маленький безопасный образ без dev-tools. | phase1 docker |
| В чём разница между CMD и ENTRYPOINT? | CMD — команда по умолчанию, легко переопределяется (docker run img bash). ENTRYPOINT — исполняемый файл, аргументы CMD становятся его аргументами. Best practice: ENTRYPOINT для бинаря, CMD для дефолтных аргументов. | phase1 docker |
| Что делает `if __name__ == '__main__'` в Python? | Проверяет, запущен ли файл напрямую, а не импортирован. Код внутри выполняется только при прямом запуске (python script.py). Позволяет использовать файл как модуль и как скрипт. | phase1 python |
| В чём разница между stage и job в GitLab CI? | Stage — группа (фаза pipeline: build, test, deploy). Job — конкретная задача внутри stage. Все jobs одного stage параллельны. Stages идут последовательно. Нужны needs — для параллельных job с зависимостями. | phase2 cicd |
| Что такое state в Terraform и зачем он нужен? | Файл terraform.tfstate — маппинг реальных ресурсов ↔ конфигурации. Terraform сравнивает desired (код) с actual (state) и планирует diff. Хранить в backend (S3/GCS/TFC), не локально. Sensitive: terraform.tfstate содержит секреты. | phase2 terraform |
| Из чего состоит Pod? | 1+ контейнеров с общим network namespace (один IP), shared volumes. Плюс init containers, ephemeral containers (для отладки). Pod — минимальная deployable единица, обычно 1 контейнер. | phase3 k8s |
| В чём разница между Deployment и StatefulSet? | Deployment — для stateless: replicas с одинаковыми именами, любой может заменить любой. StatefulSet — для stateful: стабильные имена (pod-0, pod-1), persistent volume per pod, ordered scaling. StatefulSet для БД, очередей, кластеров. | phase3 k8s |
| Что такое Service в Kubernetes и какие типы бывают? | Service — стабильная точка доступа к группе подов (через labels + selector). Типы: ClusterIP (внутри кластера), NodePort (порт на ноде), LoadBalancer (облачный LB), ExternalName (CNAME). Default: ClusterIP. | phase3 k8s |
| Что такое ConfigMap и чем отличается от Secret? | ConfigMap — несекретные конфиг-данные (env, файлы, конфиги). Secret — то же, но base64-encoded (для паролей, токенов, ключей). В продакшне Secret + encryption-at-rest + RBAC. В 2026: External Secrets + Vault. | phase3 k8s |
| Что такое liveness и readiness probes? | Liveness: kubelet рестартит pod, если probe падает (приложение зависло). Readiness: убирает pod из Service endpoints, если probe падает (не готов принимать трафик, но не убивать). Liveness — для лечения, Readiness — для временной изоляции. | phase3 k8s |
| В чём разница между Job, CronJob и Deployment? | Deployment — long-running под (web-сервер). Job — run-to-completion (миграция, бэкап). CronJob — Job по расписанию (cron: '*/5 * * * *'). Job гарантирует N успешных completions (completions, parallelism). | phase3 k8s |
| Что такое SLO, SLI и error budget? | SLI — метрика (latency p99, availability %). SLO — цель на период (99.9% за месяц). Error budget = 1 - SLO (0.1% = 43.2 мин/мес down). Если budget исчерпан — фиксим надёжность, не фичи. | phase4 observability |
| Что такое GitOps и зачем он нужен? | GitOps — declarative инфра из Git: git push → изменения применяются автоматически. Single source of truth (Git), audit trail, easy rollback (git revert). Инструменты: ArgoCD, Flux. Альтернатива ручному kubectl apply. | phase5 gitops |

---

## 📥 Как импортировать в Anki

1. Установить Anki: `flatpak install flathub net.ankiweb.Anki` или `sudo dnf install anki`
2. Anki → File → Import
3. Выбрать этот файл
4. Note type: **Basic**
5. Field 1 (Front): колонка Front
6. Field 2 (Back): колонка Back
7. Tags: колонка Tags
8. Import

Или вручную: 20 карточек, делай по 3-5 в день, чтобы не перегрузиться.
