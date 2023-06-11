# hledger for North Macedonia

[hledger](https://hledger.org) is a Plain Text Accounting tool. This project
provides you with defaults such as a Chart of Accounts valid for use in North
Macedonia.

You have to know Macedonian to understand the chart. It is
[described](http://www.ujp.gov.mk/mk/regulativa/opis/72) by the Internal
Revenue Service.

All accounts have the form:

```
mk:<class>:<subaccount>:<your custom account>
```

For example, to declare a cash account, use:

```
include mk.journal

; Declare and alias the bank account number account for Macedonian denars
account mk:10:0:<bank account number>
alias cash_mkd_<bank>=mk:10:0:<bank account number>

; Declare the banking expenses account for the bank
account mk:44:6:<bank>
alias bank_expenses_<bank>=mk:44:6:<bank>

; Banking liabilities fall under general service liabilities in North Macedonia
account general_liabilities_mk=mk:22:0
```

To record the liability and expense entries for paying the bank account
commisions, you can do something like:

```
; Liability to pay comission starts each month the bank account is active
2023-01-01 Bank account comission
  bank_expenses_<bank>  MKD <sum>
  general_liabilities_mk

; Liability is closed once the month ends
2023-02-01 Paid bank account comission
  general_liabilities_mk  MKD <sum>
  cash_mkd_<bank>
```

## License

Public domain. Go wild.

