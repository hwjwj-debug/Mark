```mermaid
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

MQTY --> MSTOCK{In Stock}
MSTOCK -- No --> ERR[Error]
MSTOCK -- Yes --> MBAL{Enough Balance}
MBAL -- No --> ERR
MBAL -- Yes --> MCONF{Confirm}

MCONF -- No --> MARKET
MCONF -- Yes --> MTX[Debit Balance Deliver]

MTX --> MORDER[Create Order]
MORDER --> MWAR[Start Warranty 1h]
MORDER --> MBON[Add Bonus Proxy Pending]

MORDER --> MCOUNT[Add To Turnover]
MCOUNT --> MSPIN{Turnover >= 10}
MSPIN -- No --> MARKET
MSPIN -- Yes --> MGIVE[Add Free Spin Minus 10]
MGIVE --> MSPIN

ORDERS --> ODETAIL[Order Detail]
ODETAIL --> OCLM[Create Claim]
OCLM --> OTIME{Within 1h}

OTIME -- Yes --> ODIS[Disputed Bonus Frozen]
OTIME -- No --> OMAN[Manual Review]

ODIS --> ODEC{Decision}
OMAN --> ODEC

ODEC -- Valid --> OOK[Resolved OK Bonus Confirmed]
ODEC -- Refund --> OREF[Refund Bonus Revoked]
ODEC -- Replace --> OREP[Replace Bonus Revoked]

PROXY --> PBAL[Proxy Balance]
PBAL --> PBUY[Buy GB]
PBAL --> PGEN[Generate Proxy]

PBUY --> PBCONF{Confirm}
PBCONF -- No --> PROXY
PBCONF -- Yes --> PBTX[Debit USD Add GB]
PBTX --> PROXY

PGEN --> PCONF{Confirm}
PCONF -- No --> PROXY
PCONF -- Yes --> PGB{Enough GB}
PGB -- No --> ERR
PGB -- Yes --> POUT[Deliver Proxy]
POUT --> PROXY

VPN --> VTAR[Tariff]
VTAR --> VCONF{Confirm}
VCONF -- No --> VPN
VCONF -- Yes --> VBAL{Enough Balance}
VBAL -- No --> ERR
VBAL -- Yes --> VTX[Deliver VPN]
VTX --> VPN

WHEEL --> WMODE{Mode}
WMODE --> WFREE[Free Spin]
WMODE --> WPAID[Paid Spin]

WFREE --> WCHK{Have Spins}
WCHK -- No --> WHEEL
WCHK -- Yes --> WUSE[Use Spin]
WUSE --> WPRIZE[Give Prize]
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

ERR[Error Message]
