flowchart TD

  A[/start] --> MENU{Главное меню}

  MENU --> MARKET[MARKET ACC]
  MENU --> SMM[SM MARKET]
  MENU --> VPN[VPN]
  MENU --> PROXY[PROXY]
  MENU --> WHEEL[Крутилка]
  MENU --> PROFILE[Профиль]

  PROFILE --> PINFO[ID Имя Баланс USD Free Spins]
  PINFO --> PACTIONS{Действия}

  PACTIONS --> TOPUP[Пополнить баланс]
  PACTIONS --> TRANSFER[Перевести баланс]
  PACTIONS --> REF[Реферальная система]
  PACTIONS --> PROMO[Промокод]
  PACTIONS --> HIST[История]
  PACTIONS --> ORDERS[Мои заказы]

  MARKET --> MCAT[Категории]
  MCAT --> DRAW[DRAW]
  MCAT --> FORPOST[FORPOST]

  DRAW --> MLIST[Список товаров]
  FORPOST --> MLIST

  MLIST --> MITEM[Карточка товара]
  MITEM --> MQTY[Количество]

  MQTY --> MSTOCK{Есть в наличии?}
  MSTOCK -- Нет --> MERR[Ошибка]
  MSTOCK -- Да --> MBAL{Хватает USD?}
  MBAL -- Нет --> MERR
  MBAL -- Да --> MCONFIRM{Подтвердить покупку?}

  MCONFIRM -- Нет --> MARKET
  MCONFIRM -- Да --> MTX[Списать баланс и выдать товар]

  MTX --> MORDER[Создать заказ статус DELIVERED]
  MORDER --> MWAR[Запустить гарантию 1 час]
  MORDER --> MBON[Начислить бонус 0.12-0.15GB статус PENDING TTL 30 дней]

  MORDER --> MCOUNT[Добавить сумму в turnover_counter]
  MCOUNT --> MSPINCHK{counter >= 10?}
  MSPINCHK -- Нет --> MARKET
  MSPINCHK -- Да --> MGIVE[+1 Free Spin и counter -10]
  MGIVE --> MSPINCHK

  ORDERS --> OLIST[Список заказов]
  OLIST --> ODETAIL[Детали заказа]
  ODETAIL --> OPROB[Проблема с товаром]

  OPROB --> OCLM[Создать претензию]
  OCLM --> OWIN{В пределах 1 часа?}

  OWIN -- Да --> OHOLD[Статус DISPUTED бонус FROZEN]
  OWIN -- Нет --> OMAN[Ручной разбор]

  OHOLD --> ODEC{Решение}
  OMAN --> ODEC

  ODEC -- Валид --> OCONF[RESOLVED_OK бонус CONFIRMED]
  ODEC -- Возврат --> OREF[RESOLVED_REFUND начислить USD бонус REVOKED]
  ODEC -- Замена --> ORPL[RESOLVED_REPLACE выдать замену бонус REVOKED]

  PROXY --> PBALVIEW[Баланс GB bonus purchased]
  PBALVIEW --> PA{Действия}

  PA --> PBUY[Купить GB]
  PA --> PGEN[Сгенерировать прокси]

  PBUY --> PPACK[1GB 5GB 10GB]
  PPACK --> PBCONF{Подтвердить?}
  PBCONF -- Нет --> PROXY
  PBCONF -- Да --> PBUSD{Хватает USD?}
  PBUSD -- Нет --> MERR
  PBUSD -- Да --> PBTX[Списать USD и начислить GB]
  PBTX --> PROXY

  PGEN --> PSET[Тип Гео Количество]
  PSET --> PCONF{Подтвердить?}
  PCONF -- Нет --> PROXY
  PCONF -- Да --> PGB{Хватает GB?}
  PGB -- Нет --> MERR
  PGB -- Да --> PSPLIT[Списать GB приоритет bonus затем purchased]
  PSPLIT --> POUT[Выдать прокси]
  POUT --> PROXY

  VPN --> VTARIFF[Тарифы]
  VTARIFF --> VCONF{Подтвердить?}
  VCONF -- Нет --> VPN
  VCONF -- Да --> VBAL{Хватает USD?}
  VBAL -- Нет --> MERR
  VBAL -- Да --> VTX[Выдать доступ]
  VTX --> VPN

  WHEEL --> WMODE{Режим}
  WMODE --> WFREE[Free Spin]
  WMODE --> WPAID[Paid Spin 1 USD]

  WFREE --> WCHKFREE{Есть Free Spins?}
  WCHKFREE -- Нет --> WHEEL
  WCHKFREE -- Да --> WUSE[-1 Spin]
  WUSE --> WFPRIZE[Приз proxy vpn или USD]
  WFPRIZE --> WHEEL

  WPAID --> WCHK{Хватает 1 USD?}
  WCHK -- Нет --> MERR
  WCHK -- Да --> WDEBIT[Списать 1 USD]
  WDEBIT --> WSPIN[Крутить]
  WSPIN --> WRES{Результат}
  WRES --> WEMPTY[Не повезло]
  WRES --> WPRIZE[Proxy VPN USD или Джекпот]
  WEMPTY --> WHEEL
  WPRIZE --> WHEEL

  MERR[Сообщение об ошибке]
