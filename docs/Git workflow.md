Краткий стандарт работы с Git для проекта **AdGuard VPN Client for PS4**.

## 1. Ветки

Основные ветки:

- `main` — стабильная версия проекта.
    
- `develop` — основная ветка разработки.
    

Рабочие ветки создаются от `develop`:

- `feature/*` — новая функциональность.
    
- `fix/*` или `bugfix/*` — исправление ошибок.
    
- `hotfix/*` — срочные исправления `main`.
    
- `release/*` — подготовка релиза.
    

Примеры:

```
main
└── develop
    ├── feature/vpn-engine
    ├── feature/game-routing
    ├── feature/server-selection
    └── fix/ikev2-connection
```

## 2. Рабочий процесс

1. Создать рабочую ветку от `develop`.
    
2. Выполнить задачу и зафиксировать изменения коммитами.
    
3. Запушить ветку в удалённый репозиторий.
    
4. Создать Pull Request в `develop`.
    
5. Пройти code review.
    
6. После проверки выполнить merge.
    
7. При выпуске релиза перенести проверенные изменения в `main`.
    

Прямые push в `main` и `develop` запрещены.

## 3. Conventional Commits

Формат коммита:

```
<type>(scope): <description>
```

Основные типы:

|Type|Назначение|
|---|---|
|`feat`|Новая функциональность|
|`fix`|Исправление ошибки|
|`refactor`|Изменение структуры кода без изменения поведения|
|`docs`|Документация|
|`style`|Форматирование|
|`test`|Тесты|
|`chore`|Служебные изменения и зависимости|
|`perf`|Оптимизация производительности|
|`build`|Сборка и конфигурация сборки|
|`ci`|CI/CD|
|`revert`|Отмена предыдущего коммита|

### Scope проекта

Использовать scope, соответствующий затронутой части системы:

- `app` — Homebrew UI.
    
- `core` — основная логика приложения.
    
- `vpn-engine` — VPN, IKEv2, IPsec, криптография.
    
- `traffic-router` — маршрутизация игрового трафика.
    
- `goldhen-plugin` — интеграция с GoldHEN.
    
- `shared` — общие типы и IPC.
    
- `tests` — тестирование.
    
- `build` — сборка и toolchain.
    
- `docs` — документация.
    
- `ci` — CI/CD.
    

Примеры:

```
feat(app): add server selection screen
feat(vpn-engine): implement ikev2 negotiation
fix(traffic-router): prevent vpn endpoint routing loop
feat(goldhen-plugin): add process tracking
refactor(core): simplify connection manager
test(vpn-engine): add ikev2 negotiation tests
docs: describe vpn architecture
chore(build): configure ps4 toolchain
```

## 4. Правила коммитов

- Один коммит — одно логическое изменение.
    
- Описание должно быть коротким и конкретным.
    
- Использовать английский язык.
    
- Не использовать абстрактные сообщения (`update`, `fix bug`, `changes`).
    
- Не смешивать независимые изменения в одном коммите.
    

## 5. Rebase и Merge

Перед созданием PR необходимо обновить рабочую ветку относительно `develop`:

```
git checkout feature/vpn-engine
git fetch origin
git rebase origin/develop
git push --force-with-lease
```

Изменения интегрируются в `develop` только через Pull Request.

## 6. Инструменты и контроль качества

Рекомендуемые инструменты:

- `commitlint` — проверка формата коммитов.
    
- `Husky` — Git hooks.
    
- `lint-staged` — проверка изменённых файлов.
    
- Pull Request templates — единый формат PR.
    
- Branch protection — защита основных веток.
    
- Code review — обязательная проверка изменений.
    

## 7. Обязательные правила

1. `main` и `develop` защищены от прямого push.
    
2. Работа над задачами ведётся в отдельных ветках.
    
3. Все изменения проходят через PR.
    
4. Коммиты соответствуют Conventional Commits.
    
5. Перед PR выполняется rebase от актуального `develop`.
    
6. Один коммит содержит одно логическое изменение.
    
7. Перед merge необходимо проверить сборку и соответствующие тесты.