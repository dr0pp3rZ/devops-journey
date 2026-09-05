# Week 1 — Linux Fundamentals

## Day 1: Processes & Init Systems
**Цель:** Понять PID 1, процессы, systemd

### Задания
1. **Изучи тему** (30 мин)
   - Прочитай: что такое PID 1, как работает init
   - Посмотри видео про systemd architecture

2. **Практика** (45 мин)
   ```bash
   # Найди PID 1
   ps -p 1 -o pid,comm,args
   
   # Посмотри дерево процессов
   pstree -asp | head -30
   
   # Найди процессы с высоким CPU
   top -bn1 | head -20
   
   # Посмотреть состояние сервисов
   systemctl status --type=service | head -30
   
   # Создай свой сервис
   cat > ~/.config/systemd/user/test.service << 'EOF'
   [Unit]
   Description=Test Service
   After=default.target
   
   [Service]
   ExecStart=/bin/sleep infinity
   User=%U
   
   [Install]
   WantedBy=default.target
   EOF
   
   systemctl --user daemon-reload
   systemctl --user start test.service
   systemctl --user status test.service
   ```

3. **Zadanie на закрепление** (30 мин)
   - Объясни разницу между systemd и init
   - Когда нужно менять PID 1?

### Anki (15 мин)
- Повтори карточки phase0 linux

---

## Day 2: Bash Scripting
**Цель:** Научиться писать простые скрипты

### Задания
1. **Изучи тему** (30 мин)
   - Variables, conditions, loops
   - Functions в bash
   - Error handling (`set -e`, `trap`)

2. **Практика** (60 мин)
   ```bash
   # Создай скрипт для мониторинга системы
   cat > ~/bin/sysmon.sh << 'EOF'
   #!/bin/bash
   set -euo pipefail
   
   echo "=== System Monitor ==="
   echo "Host: $(hostname)"
   echo "Uptime: $(uptime -p)"
   echo "CPU load: $(cat /proc/loadavg)"
   echo "Memory:"
   free -h | grep Mem
   echo "Disk:"
   df -h / | tail -1
   echo "Top 5 processes by memory:"
   ps aux --sort=-%mem | head -6
   EOF
   
   chmod +x ~/bin/sysmon.sh
   ~/bin/sysmon.sh
   ```

3. **Script challenge** (45 мин)
   - Напиши скрипт, который:
     - Скрипт проверяет свободное место на диске
     - Если < 10% — пишет в лог предупреждение
     - Показывает ТОП-10 процессов по CPU

---

## Day 3: User Management & Permissions
**Цель:** Разобраться в правах доступа

### Задания
1. **Практика** (60 мин)
   ```bash
   # Создай пользователя и группу
   sudo groupadd devops
   sudo useradd -m -g devops -s /bin/bash devops_user
   
   # Проверь права
   ls -la /home/devops_user
   id devops_user
   
   # Настрой sudo без пароля
   echo "devops_user ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/devops_user
   
   # Разберись с umask
   umask
   touch /tmp/test_perms
   ls -l /tmp/test_perms
   rm /tmp/test_perms
   ```

2. **Practice tasks** (45 мин)
   - Какие файлы в системе имеют SUID?
   - Как найти все файлы с правами 777?
   - Что делает `chmod +t /tmp`?

---

## Day 4: Networking Fundamentals
**Цель:** Понять основы сетей

### Задания
1. **Изучи теорию** (30 мин)
   - TCP vs UDP
   - DNS резолвинг
   - TLS handshake

2. **Практика** (60 мин)
   ```bash
   # Проверь DNS
   dig google.com
   nslookup yandex.ru
   
   # Посмотри сетевые соединения
   ss -tunlp | head -30
   
   # Проверь порт
   curl -v https://google.com 2>&1 | head -30
   
   # TCPdump (если есть доступ)
   # sudo tcpdump -i lo port 80
   ```

---

## Day 5: Disaster Friday 🧪
**Цель:** Сломать и починить

### Задания
1. **Сломай систему** (30 мин)
   - Удали/поврежди конфиг systemd сервиса
   - Измени права на критический файл
   - Переполни диск (опционально)

2. **Почини** (60 мин)
   - Восстанови сервис
   - Исправь права
   - Очисти место

3. **Зафиксируй** (15 мин)
   - Запиши в error journal что сломал и как чинил

---

## Day 6: Big Build
**Цель:** Собрать мини-проект

### Задание
Создай shell-скрипт `deploy-check.sh`, который:
- Проверяет доступность хоста (ping)
- Проверяет порт (nc/timeout)
- Проверяет SSL-сертификат (openssl s_client)
- Выводит красивую статистику

### Коммит
```bash
git add .
git commit -m "feat: deploy-check utility"
git push origin main
```

---

## Day 7: Review + Anki
**Цель:** Закрепить материал

### Задания
1. **Пройди Anki** (все карточки phase0)
2. **Наполни error journal** записями за неделю
3. **Составь weekly review** (шаблон в `_weekly-review-template.md`)

---

## Критерии завершения Week 1
- [ ] Все daily задания выполнены
- [ ] Anki прогресс ≥ 20 карточек
- [ ] Error journal заполнен
- [ ] Коммит сделан
- [ ] Weekly review написан
