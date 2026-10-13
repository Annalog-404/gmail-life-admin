# Gmail web UI reference (labeling)

Techniques for setting up labels and filters in Gmail through a browser automation tool.

The user signs in to Gmail themselves. Never type credentials.

## General tips

- Screenshots can lag a step behind the page. Prefer element references and DOM checks (`document.body.innerText`, visible `[role=dialog]`) over pixel coordinates.
- Confirmation dialogs: find the visible `[role=dialog]` or `[role=alertdialog]` and click its OK button with JavaScript.
- After changing settings, reload the page before checking the result.

## Removing filters and labels

- **Filters:** open `#settings/filters`, tick the filters to remove (or **Select: All**), click **Delete**, then confirm "Really delete selected filters?".
- **Labels:** open `#settings/labels` and click **remove** next to each label, then confirm the dialog. Each dialog says how many conversations lose the label. No emails are deleted.

## Importing filters

Creates labels and filters in one step and can apply them to existing mail.

1. Open `#settings/filters` and click **Import filters**.
2. Attach an Atom XML file (see [the template](../assets/filters-template.xml)) to `input[type=file][name=upload]`. Without a file picker, build the file in JavaScript and assign it with `DataTransfer`, then dispatch a `change` event.
3. Click **Open file**. Gmail lists the filters it found.
4. Tick **Apply new filters to existing email**, then click **Create filters**.
5. Reload and check the filter list.

Notes:

- Each entry uses `apps:property` names such as `from`, `hasTheWord`, `label`, and `shouldArchive` (`true` means skip the inbox).
- Escape `&` as `&amp;` and quotes as `&quot;` inside values.
- Labels in the file are created automatically. Nested labels use `/`, e.g. `Finance/Example Bank`.
- If one entry shows "Could not create", import it again on its own.
- To change an existing filter's actions (e.g. add Skip Inbox), delete it and import the updated version.

## Bulk actions

Use to mark everything in the inbox as read or to archive in bulk.

1. Open `https://mail.google.com/mail/u/0/#search/<url-encoded query>`, e.g. `in:inbox is:unread`.
2. Click the select-all checkbox in the toolbar.
3. Click **Select all conversations that match this search** in the banner.
4. Click **Mark as read** (or Archive).
5. Confirm the **Confirm bulk action** dialog. Gmail finishes in the background.

## Label colors

There's no API for this in the browser flow.

1. Each sidebar label has a menu button: `div.pM[data-label-name="<label name>"]`. Fire `mouseover`, `mousedown`, `mouseup` and `click` on it. If the menu was already open, this closes it, so check for a visible `[role=menu]` and retry once.
2. In the menu, hover **Label color** (fire `mouseover`, `mouseenter`, `mousemove`).
3. In the submenu, click the swatch whose `title` matches the color, e.g. `RGB (22, 167, 101)`.

| Color | Swatch title |
|---|---|
| Red | `RGB (217, 48, 37)` |
| Green | `RGB (22, 167, 101)` |
| Blue | `RGB (30, 83, 184)` |
| Pink | `RGB (194, 24, 91)` |
| Purple | `RGB (120, 88, 195)` |
| Orange | `RGB (255, 117, 55)` |
| Teal | `RGB (0, 114, 134)` |
