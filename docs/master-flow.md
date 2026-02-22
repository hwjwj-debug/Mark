flowchart TD

  %% =====================
  %% START + MAIN MENU
  %% =====================
  A[/\/start/] --> MENU{Главное меню}

  MENU --> MARKET[MARKET ACC]
  MENU --> SMM[SM MARKET]
  MENU --> VPN[VPN]
  MENU --> PROXY[PROXY]
  MENU --> WHEEL[Крутилка (Mini App)]
  MENU --> PROFILE[Профиль]

  %% =====================
  %% PROFILE
  %% =====================
  PROFILE --> PINFO[ID + Имя + Баланс USD + Free Spins]
  PINFO --> PACTIONS{Действия}

  PACTIONS --> TOPUP[Пополнить баланс]
  PACTIONS --> TRANSFER[Перевести баланс]
  PACTIONS --> REF[Реферальная система]
  PACTIONS --> PROMO[Промокод]
  PACTIONS --> HIST[История пополнений]
  PACTIONS --> ORDERS[Мои заказы]

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
  MSTOCK -- Да --> MBAL{Хватает баланса USD?}
  MBAL -- Нет --> MERR
  MBAL -- Да --> MCONFIRM{Подтвердить покупку?}

  MCONFIRM -- Отмена --> MARKET
  MCONFIRM -- Да --> MTX[Списать баланс / Выдать товар]

  %% ---- ORDER CREATED ----
  MTX --> MORDER[Создать заказ (order_id)\nСтатус: DELIVERED]
  MORDER --> MWAR[Запустить гарантию 1 час]
  MORDER --> MBON[Начислить бонус 0.12–0.15GB\nСтатус: PENDING\nTTL 30 дней\nCap: 1GB]

  %% ---- FREE SPIN ACCRUAL ----
  MORDER --> MCOUNT[Добавить сумму в turnover_counter]
  MCOUNT --> MSPINCHK{counter >= 10$ ?}
  MSPINCHK -- Нет --> MARKET
  MSPINCHK -- Да --> MGIVE[+1 Free Spin\ncounter -= 10]
  MGIVE --> MSPINCHK

  %% =====================
  %% CLAIMS / WARRANTY
  %% =====================
  ORDERS --> OLIST[Список заказов]
  OLIST --> ODETAIL[Детали заказа]
  ODETAIL --> OPROB[Проблема с товаром]

  OPROB --> OCLM[Создать претензию]
  OCLM --> OWIN{В пределах 1 часа?}

  OWIN -- Да --> OHOLD[Статус: DISPUTED\nБонус -> FROZEN]
  OWIN -- Нет --> OMAN[Ручной разбор]

  OHOLD --> ODEC{Решение}
  OMAN --> ODEC

  ODEC -- Валид --> OCONF[RESOLVED_OK\nБонус -> CONFIRMED]
  ODEC -- Возврат --> OREF[RESOLVED_REFUND\n+USD\nБонус -> REVOKED]
  ODEC -- Замена --> ORPL[RESOLVED_REPLACE\nВыдать замену\nБонус -> REVOKED]

  %% =====================
  %% PROXY MODULE
  %% =====================
  PROXY --> PBALVIEW[Баланс GB\nBonus / Purchased]
  PBALVIEW --> PA{Действия}

  PA --> PBUY[Купить GB]
  PA --> PGEN[Сгенерировать прокси]

  PBUY --> PPACK[1GB / 5GB / 10GB]
  PPACK --> PBCONF{Подтвердить?}
  PBCONF -- Нет --> PROXY
  PBCONF -- Да --> PBUSD{Хватает USD?}
  PBUSD -- Нет --> MERR
  PBUSD -- Да --> PBTX[Списать USD\n+Purchased GB]
  PBTX --> PROXY

  PGEN --> PSET[Тип + Гео + Кол-во]
  PSET --> PCONF{Подтвердить?}
  PCONF -- Нет --> PROXY
  PCONF -- Да --> PGB{Хватает GB?}
  PGB -- Нет --> MERR
  PGB -- Да --> PSPLIT[Списать GB приоритет:\n1) PENDING/FROZEN\n2) CONFIRMED\n3) PURCHASED]
  PSPLIT --> POUT[Выдать прокси]
  POUT --> PROXY

  %% =====================
  %% VPN
  %% =====================
  VPN --> VTARIFF[Тарифы]
  VTARIFF --> VCONF{Подтвердить?}
  VCONF -- Нет --> VPN
  VCONF -- Да --> VBAL{Хватает USD?}
  VBAL -- Нет --> MERR
  VBAL -- Да --> VTX[Выдать доступ]
  VTX --> VPN

  %% =====================
  %% WHEEL
  %% =====================
  WHEEL --> WMODE{Режим}

  WMODE --> WFREE[Free Spin]
  WMODE --> WPAID[Paid Spin 1$]

  WFREE --> WCHKFREE{Есть Free Spins?}
  WCHKFREE -- Нет --> WHEEL
  WCHKFREE -- Да --> WUSE[-1 Spin]
  WUSE --> WFPRIZE[Приз без пусто:\nProxy GB / VPN дни / $]
  WFPRIZE --> WHEEL

  WPAID --> WCHK{Хватает 1$?}
  WCHK -- Нет --> MERR
  WCHK -- Да --> WDEBIT[Списать 1$]
  WDEBIT --> WSPIN[Крутить]
  WSPIN --> WRES{Результат}
  WRES --> WEMPTY[Не повезло]
  WRES --> WPRIZE[Proxy / VPN / $ / Джекпот]
  WEMPTY --> WHEEL
  WPRIZE --> WHEEL

  %% =====================
  %% ERRORS
  %% =====================
  MERR[Сообщение об ошибке]
