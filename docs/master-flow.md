# Telegram Bot — MASTER FLOW FINAL
flowchart TD

A[Start] --> MENU{Main Menu}

MENU --> MARKET[Market Acc]
MENU --> SMM[SM Market]
MENU --> VPN[VPN]
MENU --> PROXY[Proxy]
MENU --> WHEEL[Wheel]
MENU --> PROFILE[Profile]

PROFILE --> PINFO[User Info]
PINFO --> PACTIONS{Actions}

PACTIONS --> TOPUP[Top Up]
PACTIONS --> TRANSFER[Transfer]
PACTIONS --> REF[Referral]
PACTIONS --> PROMO[Promo]
PACTIONS --> HIST[History]
PACTIONS --> ORDERS[Orders]

MARKET --> MCAT[Categories]
MCAT --> MLIST[Products]
MLIST --> MITEM[Item]
MITEM --> MQTY[Quantity]

MQTY --> MSTOCK{In stock}
MSTOCK -- No --> ERR[Error]
MSTOCK -- Yes --> MBAL{Enough balance}
MBAL -- No --> ERR
MBAL -- Yes --> MCONF{Confirm}

MCONF -- No --> MARKET
MCONF -- Yes --> MTX[Debit balance and deliver]

MTX --> MORDER[Create order]
MORDER --> MWAR[Start warranty 1h]
MORDER --> MBON[Add bonus proxy GB pending]

MORDER --> MCOUNT[Add to turnover counter]
MCOUNT --> MSPIN{Counter >= 10}
MSPIN -- No --> MARKET
MSPIN -- Yes --> MGIVE[Add free spin and minus 10]
MGIVE --> MSPIN

ORDERS --> ODETAIL[Order detail]
ODETAIL --> OCLM[Create claim]
OCLM --> OTIME{Within 1h}

OTIME -- Yes --> ODIS[Status disputed bonus frozen]
OTIME -- No --> OMAN[Manual review]

ODIS --> ODEC{Decision}
OMAN --> ODEC

ODEC -- Valid --> OOK[Resolved ok bonus confirmed]
ODEC -- Refund --> OREF[Refund and bonus revoked]
ODEC -- Replace --> OREP[Replace and bonus revoked]

PROXY --> PBAL[Proxy balance]
PBAL --> PBUY[Buy GB]
PBAL --> PGEN[Generate proxy]

PBUY --> PBCONF{Confirm}
PBCONF -- No --> PROXY
PBCONF -- Yes --> PBTX[Debit USD add GB]
PBTX --> PROXY

PGEN --> PCONF{Confirm}
PCONF -- No --> PROXY
PCONF -- Yes --> PGB{Enough GB}
PGB -- No --> ERR
PGB -- Yes --> POUT[Deliver proxy]
POUT --> PROXY

VPN --> VTAR[Tариф]
VTAR --> VCONF{Confirm}
VCONF -- No --> VPN
VCONF -- Yes --> VBAL{Enough balance}
VBAL -- No --> ERR
VBAL -- Yes --> VTX[Deliver VPN]
VTX --> VPN

WHEEL --> WMODE{Mode}
WMODE --> WFREE[Free Spin]
WMODE --> WPAID[Paid Spin]

WFREE --> WCHK{Have spins}
WCHK -- No --> WHEEL
WCHK -- Yes --> WUSE[Use spin]
WUSE --> WPRIZE[Prize]
WPRIZE --> WHEEL

WPAID --> WCHK2{Enough 1 USD}
WCHK2 -- No --> ERR
WCHK2 -- Yes --> WDEBIT[Debit 1 USD]
WDEBIT --> WSPIN[Spin]
WSPIN --> WRES{Result}
WRES --> WEMPTY[Empty]
WRES --> WPR[Prize]
WEMPTY --> WHEEL
WPR --> WHEEL

ERR[Error message]
