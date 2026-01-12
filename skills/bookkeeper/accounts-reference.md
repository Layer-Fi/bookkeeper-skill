# Common Ledger Accounts Reference

This reference contains account identifier formats and common stable_names used in the Layer API.

## Account Identifiers

Account identifiers are polymorphic - there are two ways to reference a ledger account:

### 1. AccountId (UUID)

A unique ID for a specific ledger account. Unique across ALL businesses and ALL accounts.

```json
{
  "type": "AccountId",
  "id": "f1b3b3b3-1beb-1b3b-1b3b-1b3b3b3b3b3b"
}
```

**When to use:**
- Referencing custom accounts created by users (they don't have stable names)
- When you've already looked up the specific account ID
- When precision is critical and you want to ensure the exact account

### 2. StableName

A stable identifier for templated accounts. Same stable_name works across ALL businesses.

```json
{
  "type": "StableName",
  "stable_name": "ACCOUNTS_RECEIVABLE"
}
```

**When to use:**
- Building workflows that work across multiple businesses
- Referencing standard chart-of-accounts entries (like CASH, REVENUE, etc.)
- Avoiding the need to look up UUIDs for each business

**Limitations:**
- Custom accounts created by users do NOT have stable names - use AccountId instead
- Some stable names are industry-specific (e.g., trucking accounts won't exist for a retail business)
- Using a stable_name for a non-existent account returns an error

### Quick Reference

| Scenario | Use This |
|----------|----------|
| Standard account (Cash, Revenue, etc.) | StableName |
| Custom user-created account | AccountId |
| Cross-business workflow | StableName |
| Account from search/lookup result | AccountId |

### In Journal Entry Lines

When creating journal entries, the `ledger_account_id` field accepts either format:

```json
{
  "lines": [
    {
      "ledger_account_id": {
        "type": "StableName",
        "stable_name": "OFFICE_EXPENSES"
      },
      "amount": 12345,
      "direction": "DEBIT"
    },
    {
      "ledger_account_id": {
        "type": "AccountId",
        "id": "abc-123-def-456"
      },
      "amount": 12345,
      "direction": "CREDIT"
    }
  ]
}
```

---

## Asset Accounts (DEBIT increases)

| Stable Name | Display Name | Description |
|-------------|--------------|-------------|
| `CASH` | Cash | Cash on hand |
| `ACCOUNTS_RECEIVABLE` | Accounts Receivable | Money owed by customers |
| `INVENTORY` | Inventory | Goods held for sale |
| `PREPAID_EXPENSES` | Prepaid Expenses | Expenses paid in advance |
| `FIXED_ASSETS` | Fixed Assets | Long-term assets |
| `ACCUMULATED_DEPRECIATION` | Accumulated Depreciation | Contra-asset for depreciation |

## Liability Accounts (CREDIT increases)

| Stable Name | Display Name | Description |
|-------------|--------------|-------------|
| `ACCOUNTS_PAYABLE` | Accounts Payable | Money owed to vendors |
| `NOTES_PAYABLE` | Notes Payable | Loans and notes |
| `ACCRUED_EXPENSES` | Accrued Expenses | Expenses incurred but not paid |
| `CREDIT_CARD` | Credit Card | Credit card balances |
| `SALES_TAX_PAYABLE` | Sales Tax Payable | Collected sales tax |

## Equity Accounts (CREDIT increases)

| Stable Name | Display Name | Description |
|-------------|--------------|-------------|
| `OWNERS_EQUITY` | Owner's Equity | Owner investment |
| `RETAINED_EARNINGS` | Retained Earnings | Accumulated profits |
| `OWNERS_DRAW` | Owner's Draw | Owner withdrawals (contra) |

## Revenue Accounts (CREDIT increases)

| Stable Name | Display Name | Description |
|-------------|--------------|-------------|
| `REVENUE` | Revenue | Primary sales revenue |
| `SERVICE_REVENUE` | Service Revenue | Revenue from services |
| `OTHER_INCOME` | Other Income | Non-operating income |
| `INTEREST_INCOME` | Interest Income | Interest earned |
| `CUSTOMER_REFUNDS` | Customer Refunds | Contra-revenue for refunds |

## Expense Accounts (DEBIT increases)

| Stable Name | Display Name | Description |
|-------------|--------------|-------------|
| `COST_OF_GOODS_SOLD` | Cost of Goods Sold | Direct costs of sales |
| `OFFICE_EXPENSES` | Office Expenses | General office costs |
| `RENT_EXPENSE` | Rent Expense | Rent payments |
| `UTILITIES` | Utilities | Utility bills |
| `SALARIES_EXPENSE` | Salaries Expense | Employee wages |
| `PAYROLL_TAXES` | Payroll Taxes | Employer tax expenses |
| `INSURANCE_EXPENSE` | Insurance | Insurance premiums |
| `DEPRECIATION_EXPENSE` | Depreciation Expense | Asset depreciation |
| `INTEREST_EXPENSE` | Interest Expense | Interest on loans |
| `PROFESSIONAL_FEES` | Professional Fees | Legal, accounting fees |
| `ADVERTISING` | Advertising | Marketing costs |
| `TRAVEL_EXPENSE` | Travel Expense | Business travel |
| `MEALS_ENTERTAINMENT` | Meals & Entertainment | Business meals |

## Debit vs Credit Rules

| Account Type | Normal Balance | Increase | Decrease |
|--------------|----------------|----------|----------|
| Assets | Debit | Debit | Credit |
| Liabilities | Credit | Credit | Debit |
| Equity | Credit | Credit | Debit |
| Revenue | Credit | Credit | Debit |
| Expenses | Debit | Debit | Credit |

## Journal Entry Examples

### Pay office rent with cash
```
Debit:  RENT_EXPENSE      $1,000
Credit: CASH              $1,000
```

### Purchase inventory on credit
```
Debit:  INVENTORY         $5,000
Credit: ACCOUNTS_PAYABLE  $5,000
```

### Record a sale (cash)
```
Debit:  CASH              $500
Credit: REVENUE           $500
```

### Record a sale (on account)
```
Debit:  ACCOUNTS_RECEIVABLE  $500
Credit: REVENUE              $500
```

### Record cost of goods sold
```
Debit:  COST_OF_GOODS_SOLD  $300
Credit: INVENTORY           $300
```

### Issue customer refund
```
Debit:  CUSTOMER_REFUNDS    $50
Credit: CASH                $50
```

## Important Notes

1. **Always use `get_chart_of_accounts`** to verify actual account names for a business - stable names may vary
2. **Amounts in API are in CENTS** - multiply dollars by 100
3. **direction field** uses `"DEBIT"` or `"CREDIT"` (uppercase strings)
4. **ledger_account_id** can be UUID or stable_name - prefer stable_name for readability
