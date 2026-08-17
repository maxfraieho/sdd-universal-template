# Prior Art & Compatible Extensions

`sdd-universal-template` не робить hard-залежностей на жодне зовнішнє
розширення — все нижче або вже вбудоване (GitHub Spec Kit `specify-cli`),
або опційно сумісне.

## Ядро

- **[github/spec-kit](https://github.com/github/spec-kit)** — офіційний
  SDD-тулкіт, 30+ інтеграцій агентів. `specify integration install <key>`
  генерує per-agent adapter — цей шаблон НЕ дублює цю роботу, лише додає
  SDD-контент (конституцію, методологію, скіли, handoff-протокол, арбітра)
  зверху.

## Валідує наш підхід (не залежність)

- **[msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents)**
  (146k+ зірок) — паттерн "один source → генерація адаптерів під
  Claude/Cursor/Copilot/Gemini/Antigravity" на масовому масштабі. Наш
  `.agents/skills/sdd-*` + тонкі `.codex/prompts/`/`.claude/commands/`
  лаунчери — той самий паттерн, вручну, для 3 агентів замість N.

## Дрібні, непровірені (перевір самостійно перед використанням)

- **GenieRobot/spec-kit-maqa-ext (MAQA)** — coordinator → feature-agents →
  QA-agents workflow, ~10 зірок, березень 2026. Цікаво для оркестрації
  кількох паралельних worktree, але замалий community для hard-залежності.
- **xymelon/spec-kit-agent-assign** — розподіл `/speckit.tasks` між
  спеціалізованими Claude-агентами, ~30 зірок.
- **formin/multi-model-review** — spec одним агентом, імплементація іншим,
  рев'ю третім, ~7 зірок.

## Референс для нашого арбітра

- **pelednoam/multi-model-code-review-agent** — deterministic preflight
  audit + 2-4 LLM reviewer'и паралельно + CI convergence gate. Наш
  `scripts/sdd_llm_judge.py` простіший (один reviewer, fail-open), але той
  самий принцип "детермінований gate перед комітом".

## Для brownfield

- **addyosmani/agent-skills/docs/adoption-guide.md** — 4-фазний
  brownfield roadmap, на якому базується наш `brownfield-migration-guide.md`.
