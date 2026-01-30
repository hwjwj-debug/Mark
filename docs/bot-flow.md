# Telegram Bot — ТЗ + Диаграммы (Mermaid)

> Этот документ рендерится GitHub-ом в виде диаграмм.
> Файл: `docs/bot-flow.md`

---

## 1) Главное меню (/start)

```mermaid
flowchart TD
  A[/\/start/] --> B{Главное меню}

  B --> M1[MARKET ACC]
  B --> M2[SM MAKRET]
  B --> M3[VPN]
  B --> M4[PROXY]
  B --> P0[Профиль]

