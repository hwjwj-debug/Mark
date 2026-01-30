# Master Flow — Telegram Bot (overview)

```mermaid
flowchart TD
  A[/\/start/] --> B{Главное меню}

  B --> MARKET[MARKET ACC]
  B --> SMM[SM MAKRET]
  B --> VPN[VPN]
  B --> PROXY[PROXY]
  B --> PROF[Профиль]

  %% Профиль (крупно)
  PROF --> PROF_INFO[Профиль: ID + Имя + Баланс]
  PROF_INFO --> PROF_ACT{Действия}
  PROF_ACT --> TOPUP[Пополнить баланс]
  PROF_ACT --> TRANSFER[Перевести баланс]
  PROF_ACT --> REF[Реферальная система]
  PROF_ACT --> PROMO[Активировать промокод]
  PROF_ACT --> HIST[История пополнений]

  %% Пополнение (крупно)
  TOPUP --> T_SUM[Ввести сумму]
  T_SUM --> T_METHOD{Способ}
  T_METHOD --> T_CB[CryptoBot API]
  T_METHOD --> T_CR[Криптовалюта API]
  T_CB --> T_DONE[Начислить баланс после подтверждения]
  T_CR --> T_DONE

  %% Перевод (крупно)
  TRANSFER --> TR_USER[Ввести @username]
  TR_USER --> TR_FIND{Пользователь найден?}
  TR_FIND -- Нет --> TR_ERR[Ошибка: не найден]
  TR_FIND -- Да --> TR_AMT[Ввести сумму]
  TR_AMT --> TR_CONF{Подтвердить?}
  TR_CONF -- Отмена --> TR_CAN[Перевод отменен]
  TR_CONF -- Да --> TR_BAL{Хватает баланса?}
  TR_BAL -- Нет --> TR_NOM[Недостаточно средств]
  TR_BAL -- Да --> TR_TX[Транзакция: списать/зачислить]
  TR_TX --> TR_OK[Перевод выполнен]

  %% MARKET ACC (крупно)
  MARKET --> CAT[Выбрать категорию]
  CAT --> DRAW[DRAW]
  CAT --> FORPOST[FORPOST]

  DRAW --> LIST[Категория + описание + список товаров]
  FORPOST --> LIST

  LIST --> ITEM[Выбор товара]
  ITEM --> CARD[Карточка товара: цена + описание]
  CARD --> QTY[Ввести количество]
  QTY --> STOCK{Есть в наличии?}
  STOCK -- Нет --> OOS[Нет в наличии]
  STOCK -- Да --> MONEY{Хватает баланса?}
  MONEY -- Нет --> NOMONEY[Недостаточно средств]
  MONEY -- Да --> BUYCONF{Подтвердить покупку?}
  BUYCONF -- Отмена --> BCAN[Покупка отменена]
  BUYCONF -- Да --> BUYTX[Выдать товар + списать баланс]
  BUYTX --> BUYOK[Покупка успешна]

  %% Заглушки
  SMM --> TODO1[TODO: логика не описана]
  VPN --> TODO2[TODO: логика не описана]
  PROXY --> TODO3[TODO: логика не описана]
