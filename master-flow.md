flowchart TD

%% =====================
%% START + MAIN MENU
%% =====================
A[/start/] --> MENU{Main Menu}

MENU --> MARKET[MARKET ACC]
MENU --> SMM[SM MARKET]
MENU --> VPN[VPN]
MENU --> PROXY[PROXY]
MENU --> PROFILE[Profile]

%% =====================
%% PROFILE (User)
%% =====================
PROFILE --> PINFO[Show: ID + Username + Balance]
PINFO --> PA{Profile Actions}

PA --> TOPUP[Top Up Balance]
PA --> TRANSFER[Transfer Balance]
PA --> REF[Referral System]
PA --> PROMO[Activate Promo]
PA --> TOPUPH[Top Up History]
PA --> TXH[Transaction History]
PA --> ORDERS[My Orders]
PA --> ADMIN{Admin Panel (only admin)}

%% ---- Transaction History (User) ----
TXH --> TXHLIST[List last N transactions]
TXHLIST --> TXHDETAIL[Transaction details]
TXHDETAIL --> PROFILE

%% ---- My Orders (User) ----
ORDERS --> OLIST[List last N orders]
OLIST --> ODETAIL[Order details + status]
ODETAIL --> REISSUE[Re-issue product data]
REISSUE --> ODETAIL

%% =====================
%% TOP UP FLOW
%% =====================
TOPUP --> TSUM[Enter Amount]
TSUM --> TM{Select Payment Method}
TM --> TCB[CryptoBot API]
TM --> TCR[Crypto API]
TCB --> TPAY[Create invoice/payment]
TCR --> TPAY
TPAY --> TWAIT{Payment confirmed?}
TWAIT -- No --> TWAIT
TWAIT -- Yes --> TADD[Update Balance + create transaction record]
TADD --> PROFILE

%% =====================
%% TRANSFER FLOW
%% =====================
TRANSFER --> TRU[Enter @username]
TRU --> TRF{User exists in DB?}
TRF -- No --> TRERR[Error]
TRF -- Yes --> TRA[Enter amount]
TRA --> TRC{Confirm transfer?}
TRC -- Cancel --> PROFILE
TRC -- Yes --> TRB{Enough balance?}
TRB -- No --> TRERR
TRB -- Yes --> TRTX[Atomic transaction: -sender +receiver + tx log]
TRTX --> PROFILE

%% =====================
%% MARKET ACC (Purchase + Reserve)
%% =====================
MARKET --> MCAT[Select Category]
MCAT --> MLIST[List Products in category]
MLIST --> MCARD[Product card: price + description]
MCARD --> MQTY[Enter quantity]

%% Reserve before confirm
MQTY --> MRES[Reserve stock (temporary)]
MRES --> MSTOCK{Reserve success?}
MSTOCK -- No --> MERR[Out of stock / reserve failed]
MSTOCK -- Yes --> MBAL{Enough balance?}
MBAL -- No --> MUNRES[Release reserve]
MBAL -- No --> MERR
MBAL -- Yes --> MCONF{Confirm purchase?}

MCONF -- Cancel --> MUNRES[Release reserve]
MUNRES --> MARKET

MCONF -- Yes --> MPAY[Atomic: deduct balance + finalize reserve->sold + create order + tx log]
MPAY --> MDEL[Deliver product data]
MDEL --> MCODE{Requires login code flow?}
MCODE -- No --> MOK[Order Delivered/Completed]
MCODE -- Yes --> MLV[Order status: LoginVerification (code mode)]
MLV --> MOK

%% =====================
%% SM MARKET (same purchase pattern)
%% =====================
SMM --> SCAT[Select Category]
SCAT --> SLIST[List Packages/Products]
SLIST --> SCARD[Product card]
SCARD --> SQTY[Enter qty/package]
SQTY --> SRES[Reserve stock]
SRES --> SBAL{Enough balance?}
SBAL -- No --> SUNRES[Release reserve]
SUNRES --> SMM
SBAL -- Yes --> SCONF{Confirm?}
SCONF -- Cancel --> SUNRES
SCONF -- Yes --> SPAY[Atomic: deduct + finalize reserve + create order + tx log]
SPAY --> SDEL[Deliver service/product]
SDEL --> SMM

%% =====================
%% VPN (Buy + Subscription record)
%% =====================
VPN --> VPLAN[Select Plan 7/30/90]
VPLAN --> VBAL{Enough balance?}
VBAL -- No --> MERR
VBAL -- Yes --> VPAY[Atomic: deduct + create subscription + tx log]
VPAY --> VDATA[Show VPN data]
VDATA --> PROFILE

%% =====================
%% PROXY (Buy + Reserve pool)
%% =====================
PROXY --> PTYPE[Select Type]
PTYPE --> PGEO[Select GEO]
PGEO --> PTERM[Select Duration/Qty]
PTERM --> PBAL{Enough balance?}
PBAL -- No --> MERR
PBAL -- Yes --> PPAY[Atomic: deduct + reserve pool + create order + tx log]
PPAY --> PDATA[Deliver proxy list]
PDATA --> PROFILE

%% =====================
%% ADMIN PANEL (Single-admin, you upload goods)
%% =====================
ADMIN --> A0[Admin Menu]

A0 --> A1[Add Product]
A0 --> A2[Edit Product (price/desc/status)]
A0 --> A3[Restock Product (increase qty)]
A0 --> A4[Manage Categories (add/rename/remove)]
A0 --> A5[Search Product by ID/name]
A0 --> A6[Sales Stats (day/week)]

A1 --> A1F[Save to DB]
A2 --> A2F[Update DB]
A3 --> A3F[Update stock DB]
A4 --> A4F[Update categories DB]
A5 --> A5R[Show results]
A6 --> A6R[Show metrics]

A1F --> A0
A2F --> A0
A3F --> A0
A4F --> A0
A5R --> A0
A6R --> A0
