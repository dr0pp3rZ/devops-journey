# Disaster Friday — Week 1 🧪

**Правило:** Каждый пятницы ломаем и чиним. Фиксируем в error journal.

---

## Сценарий 1: Сломанный systemd сервис (30 мин)

### Задание
1. Создай сервис `broken-service.service`:
```bash
cat > ~/.config/systemd/user/broken.service << 'EOF'
[Unit]
Description=Broken Test Service

[Service]
Type=simple
ExecStart=/usr/bin/false
Restart=always
EOF

systemctl --user daemon-reload
systemctl --user start broken.service
```

2. **Сломай его:**
```bash
# Измени ExecStart на несуществующую команду
sed -i 's|/usr/bin/false|/usr/bin/nonexistent-command|' ~/.config/systemd/user/broken.service
systemctl --user daemon-reload
systemctl --user restart broken.service
```

3. **Отладь и почини:**
- Посмотри логи: `journalctl --user -u broken.service -n 50`
- Определи причину падения
- Восстанови сервис

**Усложнение:** Добавь условие RestartCondition для graceful degradation

---

## Сценарий 2: Переполненный диск (30 мин)

### Задание
1. Создай мусорные файлы:
```bash
mkdir -p /tmp/fake-home/disk-filler
cd /tmp/fake-home/disk-filler
for i in {1..100}; do dd if=/dev/zero of="file_$i" bs=1M count=50; done
```

2. **Найди и исправь:**
```bash
# Найди большие файлы
du -sh * | sort -hr | head -20

# Очисти мусор
rm -rf /tmp/fake-home
df -h /
```

**Усложнение:** Настрой logrotate для автоматической очистки

---

## Сценарий 3: Потеря SSH доступа (45 мин)

### Задание
1. **Подготовь:**
```bash
# Создай тестового пользователя
sudo useradd -m -s /bin/bash test-ssh-user
sudo passwd test-ssh-user
```

2. **Сломай SSH конфиг:**
```bash
# Бекап оригинального конфига
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak

# Измени порт на несуществующий
sudo sed -i 's|#Port 22|Port 99999|' /etc/ssh/sshd_config
sudo systemctl restart sshd
```

3. **Восстанови доступ:**
- Если есть доступ через консоль — исправь конфиг
- Если нет — используй recovery mode
- Проверь: `sshd -t` перед restart

**Усложнение:** Настрой ключевой вход + отключи password auth

---

## Сценарий 4: Разбитый Git репозиторий (30 мин)

### Задание
1. **Инициализируй:**
```bash
mkdir -p /tmp/broken-git && cd /tmp/broken-git
git init
echo "test" > README.md
git add .
git commit -m "initial"
```

2. **Сломай:**
```bash
# Удали коммит из истории (но не gc)
rm -rf .git/objects/pack/*.pack
git status  # Теперь repo сломан
```

3. **Восстанови:**
```bash
# Попытайся восстановить
git fsck --full
git reflog  # Может помочь
```

**Усложнение:** Научись делать `git fsck` регулярно

---

## Рефлексия (15 мин)

Заполни в error journal:
- Что сломал?
- Как диагностировал проблему?
- Что помогло решить?
- Чему научился?

---

## Критерии успеха
- [ ] Все сценарии выполнены (хотя бы базово)
- [ ] Error journal заполнен
- [ ] Понимаешь основы диагностики системных ошибок
