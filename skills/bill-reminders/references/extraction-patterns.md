# Extraction patterns

How to find due dates and statuses in bill emails.

## Due date phrases

Look for a date right after one of these phrases, in the subject or body:

- "due date", "payment due date", "due on", "due by"
- "please pay by", "pay on or before", "payment deadline"
- "minimum amount due … on"
- "was due on" (usually means overdue)
- Tables with a "Due Date" or "Payment Due" column

## Date formats

| Format | Example |
|---|---|
| Month name | October 21, 2026 · 21 October 2026 · Oct 21 |
| Numeric, day first | 21/10/2026 · 21-10-2026 |
| Numeric, month first | 10/21/2026 |
| ISO | 2026-10-21 |

- Numeric dates are ambiguous. Use the biller's country convention, and confirm with the user if day and month could both be ≤ 12.
- If the year is missing, use the next future occurrence relative to the email date.
- Convert to the user's time zone. Treat all-day due dates as the local calendar date.

## Status phrases

| Status | Phrases |
|---|---|
| Statement | "your statement is ready", "statement of account", "billing statement" |
| Reminder | "payment reminder", "friendly reminder", "upcoming due date" |
| Past due | "past due", "overdue", "no payment was posted", "months past due", "endorsed to collections" |
| Paid | "payment received", "payment posted", "thank you for your payment", "payment confirmation" |

## Amount phrases

"total amount due", "minimum amount due", "amount due", "outstanding balance", "statement balance".

Record the currency as shown. Only include amounts in calendar events if the user agreed.

## Things to ignore

- Marketing about loans, cards, cash advances or "pre-approved" offers.
- Rewards and points balances.
- Promotional "due" wording, e.g. "free October dues" from a gym promotion.
