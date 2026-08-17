# sdd-universal-template

Портативний стартовий шаблон Spec-Driven Development (SDD) для
мультиагентної розробки (Claude Code / Codex CLI / AGY Antigravity CLI),
з підтримкою greenfield (новий проєкт) і brownfield (ретрофіт на
існуючий код).

Дистильовано з робочої SDD-імплементації [vydra-swiss-survey](https://github.com/maxfraieho/vydra-swiss-survey)
(`specs/021-multiagent-sdd-extension`), генералізовано через Jinja-плейсхолдери.

## Швидкий старт (greenfield)

```bash
uvx copier copy --trust gh:maxfraieho/sdd-universal-template /path/to/new-project
cd /path/to/new-project
# заповни .specify/constitution.md власними фактами (секція 1 — вручну, не токенами)
git add -A && git commit -m "chore: bootstrap SDD via sdd-universal-template"
```

Copier поставить питання про твій стек (мова, БД, hot-path бюджет, набір
агентів тощо) і згенерує `.specify/`, `.agents/skills/sdd-*`,
`.codex/prompts/`, `.claude/commands/sdd/`, `bin/sdd_verify.sh`,
`scripts/sdd_llm_judge.py`, `.githooks/pre-commit`.

## Brownfield (існуючий проєкт)?

Спочатку `docs/brownfield-migration-guide.md` (після `copier copy` — файл
буде в новому проєкті, генерується разом з рештою). Це НЕ "просто
скопіювати файли" — 4-фазний roadmap з gate'ами.

## Оновлення згенерованого проєкту

```bash
cd /path/to/existing-project
uvx copier update --trust
```

`.specify/constitution.md`, `.specify/feature.json`, `AGENTS.md`
захищені (`_skip_if_exists`) — твої кастомізації не перезаписуються.

## Структура репо

```
sdd-universal-template/
├── copier.yml                     # питання генерації
├── docs/
│   └── prior-art.md               # на що спирається цей шаблон
├── .github/workflows/
│   └── template-ci.yml            # smoke-test: генерує проєкт, ганяє sdd_verify.sh
└── template/                      # ← все звідси йде в згенерований проєкт
    ├── .specify/constitution.md.jinja
    ├── .agents/skills/sdd-*/SKILL.md.jinja
    ├── .codex/prompts/sdd-*.md.jinja
    ├── .claude/commands/sdd/*.md.jinja
    ├── docs/for-agents/sdd-development-methodology.md.jinja
    ├── docs/brownfield-migration-guide.md.jinja
    ├── bin/sdd_verify.sh
    ├── scripts/sdd_llm_judge.py.jinja
    └── .githooks/pre-commit.jinja
```

## Чому Copier, не Cookiecutter

Cookiecutter генерує один раз і забуває. Copier тримає
`.copier-answers.yml` у згенерованому проєкті — `copier update` тягне
оновлення шаблону з часом (three-way merge), без ручного copy-paste
кожного разу коли методологія в цьому репо зміниться.

## Що НЕ входить у шаблон

Ніякого прикладного коду (Flask/routes/моделі/т.д.) — лише SDD-скаффолдинг.
Немає hard-залежностей на community Spec Kit extensions (MAQA/agent-assign)
— вони маленькі й непровірені, дивись `docs/prior-art.md`.
