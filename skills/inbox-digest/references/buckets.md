# Bucket rules

How to decide which bucket a thread goes in, with Gmail search hints.

## Needs action

### Bills

- Search the Finance, Bills & Utilities and Government labels if they exist, plus `subject:("statement" OR "payment due" OR "payment reminder" OR "billing") newer_than:45d`.
- Include a bill if its due date is in the next 14 days, or it's past due with no later payment confirmation.
- Past-due wording: "past due", "overdue", "no payment was posted", "endorsed to collections".
- Paid wording: "payment received", "payment posted", "thank you for your payment".
- Ignore loan and credit-card marketing.

### Security alerts

- Search: `subject:("security alert" OR "new sign-in" OR "password" OR "verification code" OR "unusual activity") newer_than:7d`
- Include new sign-ins, password changes, account recovery and suspicious-activity notices.
- Leave out one-time verification codes older than a few minutes, unless the user didn't request one, which is worth flagging.

### People waiting for a reply

- Mail from a real person (not `noreply`, `no-reply`, `notifications`, `mailer`), sent to the user directly (not a mailing list), where the user hasn't replied in the thread.
- Search hint: `-from:(noreply OR no-reply OR notifications) -category:(promotions OR social) is:unread`

### Career

- Recruiter or interview emails from a person, not job-board alerts.
- Search hint: `("interview" OR "job opportunity" OR "your application") -from:(linkedin.com OR indeed.com OR glassdoor.com)`

### Government

- Search the Government label if it exists, plus the country's government domain, e.g. `from:gov.ph newer_than:7d` or `from:gov.au newer_than:7d`.
- Needs action when there's a deadline: tax filing or payment, contribution due, a document to submit, an appointment to confirm.
- Otherwise Good to know (announcements, receipts for payments already made).

### Failed subscription payments

- Search: `subject:("payment failed" OR "payment declined" OR "update your payment" OR "card expired") newer_than:7d`, or the Subscriptions label.
- Needs action only if the sender is the real service (check the domain); these are a common phishing pattern.

### Other deadlines

- Documents to sign, forms to submit, renewals with a date, appointments to confirm.

## Good to know

- Orders, shipping and delivery updates.
- Receipts and payment confirmations.
- Subscription renewals and price changes (Subscriptions label if it exists). A price increase is worth one line.
- Appointment and booking confirmations.
- Replies that close a conversation ("thanks, all set").

## Background (count only)

| Type | Search hint |
|---|---|
| Promotions | `category:promotions` |
| Social | `category:social`, or the Social label |
| Newsletters | Newsletters label, a `list:` header, or `unsubscribe` in the body |
| Job alerts | `from:(jobalerts-noreply@linkedin.com OR indeed.com OR glassdoor.com)` |

## Possible phishing

Flag instead of listing normally when:

- The sender domain doesn't match the company named (e.g. a bank name from a free email address).
- It asks for a password, one-time code, card number or urgent payment through a link.
- It threatens account closure or legal action with a short deadline.
