# Gmail web UI reference (cleanup)

Techniques for bulk cleanup in Gmail through a browser automation tool. Use them when the Gmail API tools are too slow (one call per thread) or can't do the job.

The user signs in to Gmail themselves. Never type credentials.

## General tips

- Screenshots can lag a step behind the page. Prefer element references and DOM checks (`document.body.innerText`, visible `[role=dialog]`) over pixel coordinates.
- Confirmation dialogs: find the visible `[role=dialog]` or `[role=alertdialog]` and click its OK button with JavaScript.
- After a bulk action, reload the page before checking the result.

## Bulk actions

Use for moving thousands of conversations to Trash.

1. Open `https://mail.google.com/mail/u/0/#search/<url-encoded query>`.
2. Click the select-all checkbox in the toolbar.
3. Click **Select all conversations that match this search** in the banner. Without this, only the visible page (about 50) is affected.
4. Click Delete.
5. Confirm the **Confirm bulk action** dialog.
6. Gmail shows "We'll do the same for any remaining conversations in a few minutes" and finishes in the background.

Useful queries:

| Purpose | Query |
|---|---|
| Old promotions | `category:promotions older_than:7d -is:starred` |
| Social | `category:social -is:starred` |
| Old job alerts | `from:(jobalerts-noreply@linkedin.com OR jobs-noreply@linkedin.com OR indeed.com OR glassdoor.com) older_than:14d` |

## Unsubscribe mechanics

- Sandboxed environments often block direct HTTP calls to marketing hosts. Run unsubscribe requests from the browser instead.
- **One-click (RFC 8058):** open any page on the unsubscribe URL's origin, then `fetch(url, {method: 'POST', headers: {'Content-Type': 'application/x-www-form-urlencoded'}, body: 'List-Unsubscribe=One-Click'})`. A 200, 202 or 204 response means accepted.
- **Salesforce Marketing Cloud** (`click.<domain>/subscription_center.aspx?jwt=…`): a GET errors out. Open `/Error.aspx` on the same host, then send the one-click POST to the original URL. "Unsubscribe Request Accepted" (202) means success.
- **If `fetch` fails** (e.g. a content security policy): build a hidden `<form method="POST">` with input `List-Unsubscribe=One-Click` and submit it.
- **Pages with a confirm step:** select the opt-out option, then click Save or Submit. Close any region or cookie popup first.
- **Blank or missing unsubscribe link:** offer to mark the sender as spam or to turn off emails in the sender's app instead.
