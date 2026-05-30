# Index

${toc}

# Investments

++Capital gains retrieval/reimbursement++:
```math
//Capital gains retrieval/reimbursement
amount = 100 # Initial amount
interest = .05 # Anual rate
// Reimbursement moment(1=anual, 2=semestral, 3=quadrianual, 4=trimestral)
period = 1
interest = interest/period
tax = .28 # Tax or commission
// Capital gains
capital_gains = amount*interest
// Accumulated amount
accumulated = amount+capital_gains
// Amount to be redeemed
redeem = capital_gains/(1+tax)
// Total debited from the accumulated amount.
debited = redeem*(1+tax)
```