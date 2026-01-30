# Telegram Bot — MASTER FLOW (единая диаграмма)

```mermaid
flowchart TD

  %% =====================
  %% START + MAIN MENU
  %% =====================
  A[/\/start/] --> MENU{Главное меню}

  MENU --> MARKET[MARKET ACC]
  MENU --> SMM[SM MAKRET]
  MENU --> VPN[VPN]
  MENU --> PROXY[PROXY]
  MENU --> PROFILE[Профиль]

  %% =====================
  %% PROFILE
  %% =====================
  PROFILE --> PINFO[ID + Имя + Баланс]
  PINFO --> PACTIONS{Действия}

  PACTIONS --> TOPUP[Пополнить баланс]
  PACTIONS --> TRANSFER[Перевести баланс]
  PACTIONS --> REF[Реферальная система]
  PACTIONS --> PROMO[Промокод]
  PACTIONS --> HIST[История пополнений]

  %% ---- TOP UP ----
  TOPUP --> TSUM[Ввести сумму]
  TSUM --> TMETHOD{Способ оплаты}
  TMETHOD --> TCB[CryptoBot API]
  TMETHOD --> TCR[Криптовалюта API]
  TCB --> TPAY[Создать платёж]
  TCR --> TPAY
  TPAY --> TWAIT{Оплата подтверждена?}
  TWAIT -- Нет --> TWAIT
  TWAIT -- Да --> TADD[+ Баланс]
  TADD --> PROFILE

  %% ---- TRANSFER ----
  TRANSFER --> TUSER[Ввести @username]
  TUSER --> TFOUND{Пользователь найден?}
  TFOUND -- Нет --> TERR[Ошибка]
  TFOUND -- Да --> TAMOUNT[Ввести сумму]
  TAMOUNT --> TCONFIRM{Подтвердить?}
  TCONFIRM -- Отмена --> PROFILE
  TCONFIRM -- Да --> TBAL{Хватает баланса?}
  TBAL -- Нет --> TERR
  TBAL -- Да --> TTX[Списать / Зачислить]
  TTX --> PROFILE

  %% ---- REFERRAL ----
  REF --> RINFO[Реф. ссылка + статистика]
  RINFO --> RCOND[Условия]
  RINFO --> RSTAT[Приглашённые]
  RINFO --> RBONUS[Бонусы → баланс]
  RBONUS --> PROFILE

  %% ---- PROMO ----
  PROMO --> PCODE[Ввести промокод]
  PCODE --> PVALID{Промокод валиден?}
  PVALID -- Нет --> PROFILE
  PVALID -- Да --> PREWARD[Начислить бонус / скидку]
  PREWARD --> PROFILE

  %% ---- HISTORY ----
  HIST --> HLIST[Список пополнений]
  HLIST --> HDETAIL[Детали операции]
  HDETAIL --> PROFILE

  %% =====================
  %% MARKET ACC
  %% =====================
  MARKET --> MCAT[Категории]
  MCAT --> DRAW[DRAW]
  MCAT --> FORPOST[FORPOST]

  DRAW --> MLIST[Список товаров]
  FORPOST --> MLIST

  MLIST --> MITEM[Карточка товара]
  MITEM --> MQTY[Ввести количество]

  MQTY --> MSTOCK{Есть в наличии?}
  MSTOCK -- Нет --> MERR[Ошибка]
  MSTOCK -- Да --> MBAL{Хватает баланса?}
  MBAL -- Нет --> MERR
  MBAL -- Да --> MCONFIRM{Подтвердить покупку?}

  MCONFIRM -- Отмена --> MARKET
  MCONFIRM -- Да --> MTX[Списать баланс / Выдать товар]
  MTX --> MARKET

  %% =====================
  %% SM MAKRET
  %% =====================
  SMM --> SMCAT[Категории]
  SMCAT --> SMLIST[Товары]
  SMLIST --> SMITEM[Карточка]
  SMITEM --> SMQTY[Кол-во / пакет]
  SMQTY --> SMBAL{Хватает баланса?}
  SMBAL -- Нет --> MERR
  SMBAL -- Да --> SMTX[Списать / Выдать]
  SMTX --> SMM

  %% =====================
  %% VPN
  %% =====================
  VPN --> VTARIFF[Тарифы]
  VTARIFF --> VCONF{Подтвердить?}
  VCONF -- Нет --> VPN
  VCONF -- Да --> VBAL{Хватает баланса?}
  VBAL -- Нет --> MERR
  VBAL -- Да --> VTX[Создать доступ / выдать конфиг]
  VTX --> VPN

  %% =====================
  %% PROXY
  %% =====================
  PROXY --> PTYPE[Тип прокси]
  PTYPE --> PGEO[Гео]
  PGEO --> PTERM[Срок / кол-во]
  PTERM --> PCONF{Подтвердить?}
  PCONF -- Нет --> PROXY
  PCONF -- Да --> PBAL{Хватает баланса?}
  PBAL -- Нет --> MERR
  PBAL -- Да --> PTX[Резерв / выдать прокси]
  PTX --> PROXY

  %% =====================
  %% ERRORS
  %% =====================
  MERR[Сообщение об ошибке]
