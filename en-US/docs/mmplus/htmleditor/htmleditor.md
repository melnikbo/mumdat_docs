---
title: Anwenderhandbuch m+m HTML Editor
---

# m+m HTML Editor User Guide

## Introduction

The **m+m HTML Editor** provides a convenient rich-text editor in Microsoft Dynamics 365 Business
Central that lets users capture and maintain long text fields (BLOB/long-text fields) with
formatting. Instead of entering plain running text, you edit the content in a toolbar with
formatting functions such as font size, bold, bulleted lists, tables, and images; the editor saves
the result as HTML back into the underlying long text field.

**Target audience:** This guide is aimed primarily at **operational users** who maintain long texts
as part of their daily work — for example descriptions, notes, or document texts on pages where the
editor control is embedded. It also addresses, secondarily, **administrators and key users** who
install the app, ensure the license is in place, and assign permissions.

**Brief process overview:** The user opens a page on which a long text field is provided through the
HTML editor → they edit and format the text in the toolbar → the entries are transferred into the
field automatically or when the page is saved. The editor appears either as a **large editing area**
or as a compact **FactBox editor** at the side of the page.

This module is a technical extension: it supplies the editor control that other Business Central
pages use for their long text fields. It does not bring its own lists, documents, master data, or
setup pages; the specific page on which you encounter the editor is determined by the calling
function.

## Quick Start for Users

The fastest way from opening the page to saved, formatted text:

1. **Open a page with a long text field.** Call up the page whose long text field is provided
   through the HTML editor (for example a comment or description field). The editor is displayed as
   an editing area with a toolbar.
2. **Enter or paste text.** Click into the editing area and type or paste your text.
3. **Format.** Use the toolbar — for example **Bold**, **Font Size**, **Bulleted List**, or
   **Insert table** — to style the text.
4. **Save.** The editor applies changes automatically (autosave); in addition, the content is saved
   when the calling page requests the save. Leave or close the page as usual to commit the record.

If the field is displayed as **read-only**, the editor hides the toolbar and allows reading only —
this is not an error; it reflects the editing status of the record.

## Setup

The m+m HTML Editor comes with **no setup page of its own, no number series, and no report or mail
parameters**. Setup is limited to the technical provisioning of the app, a valid license, and the
assignment of permissions. The administrator performs these steps once before first use; after that,
the editor control is available everywhere a calling page embeds it.

### Setting up installation and dependency

**Process:** The administrator installs the app in the Business Central environment. The m+m HTML
Editor requires the base app **m+m Cloud Base** (dependency in `app.json`); without this base, the
module cannot be installed.

Proceed in dependency order:

1. **First**, make sure that **m+m Cloud Base** is installed in the target environment.
2. **Then** install the **m+m HTML Editor** (app version 27.0.0.0, compatible with platform and
   application 27.0.0.0).
3. **Finally**, the users sign in; from this point on, the editor control is available to calling
   pages.

After installation, no further field-level configuration is needed — the editor configures its
toolbar and its behavior itself.

### Understanding the license check

**Process:** On every user sign-in, the module automatically checks the license. This check is not
configurable in a visible way; it runs in the background and binds the HTML editor to a valid
license of the m+m product line.

| Process | Explanation |
|---------|-------------|
| License check at sign-in | When a user signs in, the module determines its own app registration and calls the base's license check; this ensures that the HTML editor is active only in licensed environments. Without a valid license, the module's functions are not available — the administrator must have the license of the m+m product line checked. |

The check is performed against the current module registration (installed app) and the signed-in
user in the current tenant. There is nothing for the operational user to configure here; the only
relevant point is that, if the license is missing, the editor does not work as expected and the
administrator must be informed.

### Assigning permissions

**Process:** So that users can use the module's functions, the administrator assigns the included
permission set. The module supplies an assignable permission set with the name **All permissions**.

| Setup | Explanation |
|-------------|-------------|
| Permission set **All permissions** | When this permission set is assigned to a user or a user group, the user gains access to the HTML editor's functional building blocks; without this assignment, the module cannot run its objects for the user. The set therefore determines which users are allowed to use the editor. |

Assign the permission set to the users who are to maintain long texts through the editor. Field-level
control is not provided; access is governed at the module level.

## The HTML Editor in Daily Use

As soon as a calling page provides a long text field through the HTML editor, you work directly in
the editing area. The editor loads the existing field content on opening and automatically applies
your changes back into the field.

### Editing, loading, and saving

**Sequence for opening and editing:**

1. **First**, the page opens the editor and loads the existing content of the long text field into
   the editing area.
2. **Then** you edit the text. The editor buffers your entries on its own with **autosave** shortly
   after the last change.
3. **Finally**, the editor applies the content when the calling page requests a save or you close
   the page; the formatted HTML content is written into the field.

| Function | Explanation |
|----------|-------------|
| Autosave | When you change the text, the editor reports the change back on its own after a short wait; this means your interim state is not lost, even if you do not save manually. |
| Loading the field content | On opening, the current field content is loaded into the editor so that you always continue working from the most recently saved state. |
| Request save | When the calling page triggers the save, the editor hands the current HTML content over to the field; this ensures that your formatting is committed together with the record. |

### Toolbar and formatting functions

The toolbar of the large editor provides the following functions. The button captions appear in
English in Business Central.

| Function | Explanation |
|----------|-------------|
| **Heading** | When you mark a paragraph as a heading, the text is displayed as a structured heading; this makes longer content more readable. |
| **Font Size** | When you choose a font size (available: 9, 11, 13, Default, 17, 19, 21), the selected text is displayed at that size; without a selection, the default size is retained. |
| **Font Family** | When you select a font, the selected text is set in that font. |
| **Font Color** | When you choose a foreground color from the color palette, the selected text is colored in that color. Available colors include **Black**, **Dim grey**, **Grey**, **Light grey**, **White**, **Red**, **Orange**, **Yellow**, **Light green**, **Green**, **Aquamarine**, **Turquoise**, **Light blue**, **Blue**, **Purple**. |
| **Font Background Color** | When you choose a background color, the selected text is given a colored background (for example to highlight it); the same color palette as for the font color is available. |
| **Bold** | When you apply this function, the selected text is displayed in bold. |
| **Italic** | When you apply this function, the selected text is displayed in italics. |
| **Underline** | When you apply this function, the selected text is underlined. |
| **Remove Format** | When you apply this function, all character formatting of the selected text is removed and the text is reset to its basic appearance. |
| **Link** | When you insert a link, the selected text is linked to a target address; the reader can follow the reference later. |
| **Bulleted List** | When you apply this function, the selected lines are formatted as an unnumbered bulleted list. |
| **Numbered List** | When you apply this function, the selected lines are formatted as a numbered list; the numbering is continued automatically. |
| **Alignment** | When you choose an alignment, the paragraph is aligned accordingly (left, center, right, justified). |
| **Increase Indent** | When you apply this function, the paragraph is indented one level further; this is useful for nesting within lists. |
| **Decrease Indent** | When you apply this function, the indentation of the paragraph is reduced by one level. |
| **Insert image** | When you insert an image, a graphic is placed into the text; image tools then become available (see below). |
| **Block quote** | When you apply this function, the selected paragraph is displayed as a set-off quotation and visually highlighted from the rest of the text. |
| **Insert table** | When you insert a table, a row/column grid is placed into the text; table tools are then available for editing (see below). |
| **Undo** | When you apply this function, the last editing step is undone. |
| **Redo** | When you apply this function, a previously undone step is restored. |

**Image tools (after inserting an image):** After **Insert image**, you can store alternative text
via **Image text alternative** and show or hide a caption via **Toggle caption**. In addition, the
placement variants **In line**, **Wrap text**, and **Break text** are available, with which the
image is positioned within the text or next to the text.

**Table tools (after inserting a table):** Use **Column** to edit columns, **Row** to edit rows, and
**Merge cells** to merge selected cells into one.

### Viewing and editing the HTML source

The large editor additionally offers a button at the end of the toolbar with which you switch
between the rendered view and the **HTML source**. This lets you correct unwanted formatting (for
example from pasted content) directly in the source.

| State | Explanation |
|---------|-------------|
| Rendered view (default) | The editor displays the formatted text. When you press the **Show HTML (edit raw)** button, the editor switches to the source view. |
| Source view | Once you have switched, you see and edit the raw HTML in a text area; this is suitable for targeted corrections to the markup. Via **Show rendered** you return to the rendered view, whereby your source changes are carried over into the formatted display. |

### Read-only and enlarged display

| Behavior | Explanation |
|-----------|-------------|
| Read-only mode | When the calling page sets the field to read-only, the editor hides the toolbar and allows reading only; this way you immediately recognize that the record must not be edited in its current status. |
| Hide toolbar | When the calling page hides the toolbar, the content is shown without formatting tools; the text remains readable but cannot be formatted via the bar. |
| Enlarged view | When the enlarged display is active, the editor fills the available area completely; this provides more space when editing long texts. |

## FactBox Editor

Alongside the large editor, the module provides a compact variant for the **FactBox** at the side of
the page. It is suitable for displaying and maintaining long texts alongside a document or record
without leaving the main view.

The FactBox editor behaves largely like the large editor — it loads the field content, offers the
same formatting toolbar (**Bold**, **Font Size**, **Insert table**, etc.), supports autosave, and
can be set to read-only. Two differences should be noted:

- The FactBox editor is displayed at a **lower height**, matching the narrower FactBox column.
- Switching to the **HTML source** (the **Show HTML (edit raw)** button) is **not** available in the
  FactBox variant; for source corrections, use the large editor.

## Typical Use Cases

### Capturing long text with formatting

**Trigger:** A clerk is tasked with storing a meaningful, structured long text for a record — for
example as an internal note or as a document text that is later printed or sent.

**Entry point in BC:** The user opens the relevant page with the long text field; there the HTML
editor appears with its toolbar.

**Core sequence:**

1. Click into the editing area and enter the text.
2. Highlight important passages with **Bold**, structure enumerations via **Bulleted List**, and, if
   needed, insert an overview via **Insert table**.
3. Set color highlights via **Font Color** or **Font Background Color**.
4. The editor saves the changes automatically; when the page is closed, the content is transferred
   into the field.

**Conclusion:** The formatted HTML content is saved in the field and is available to the downstream
function (for example display, printing) on the calling page.

### Cleaning up pasted content via the source

**Trigger:** A user copies text from another application into the long text field and finds that
unwanted formatting was carried over in the process.

**Entry point in BC:** The user works in the large HTML editor of the relevant page.

**Core sequence:**

1. First remove the character formatting of the selected area via **Remove Format**.
2. If the remaining markup (for example paragraphs, tables) is still not sufficient, switch to the
   source view via the **Show HTML (edit raw)** button.
3. In the source, remove or correct the offending HTML elements.
4. Switch back to the rendered view via **Show rendered**; the corrections are carried over.

**Conclusion:** The cleaned-up text is saved automatically and committed to the field when the page
is closed. In the FactBox variant, the source view is not available; this case is therefore handled
in the large editor.

## FAQ and Troubleshooting

### Why do I see no toolbar, only the text?

The field is displayed as read-only. In this case the editor hides the toolbar and allows reading
only. Whether a field is editable depends on the status of the record on the calling page — not on
the editor itself.

### Do I have to save my changes manually?

No. The editor applies your entries with autosave shortly after the last change. In addition, the
content is committed when the calling page requests a save or you close the page.

### Why are the editor functions not available to me at all?

The license or the permission may be missing. The module checks the license of the m+m product line
on every sign-in; if no valid license is present, the editor does not work as expected. In addition,
you need the permission set **All permissions**. In this case, contact your administrator.

### Which base app is required?

The m+m HTML Editor requires the app **m+m Cloud Base**. Without this base, the module cannot be
installed; the base is therefore provisioned first.

### How do I insert an image into the text?

Use **Insert image** in the toolbar. Afterwards you can add alternative text via **Image text
alternative** and a caption via **Toggle caption**, and position the image within or next to the
text.

### How do I create a table and edit it?

Insert a table via **Insert table**. Afterwards you edit the columns via **Column**, the rows via
**Row**, and merge cells via **Merge cells**.

### How do I remove accidental formatting?

Select the affected text and choose **Remove Format**. This removes the character formatting and
resets the text to its basic appearance. For corrections to the underlying HTML, additionally use
the source view.

### How can I see and correct the raw HTML?

In the large editor, press **Show HTML (edit raw)** at the end of the toolbar to switch to the source
view. After the correction, return to the formatted view via **Show rendered**. In the FactBox
variant, this switch is not available.

### Why is the HTML source toggle missing in the FactBox?

The FactBox variant of the editor deliberately does not offer switching to the HTML source; it is
designed for the compact display. For source work, use the large editor on the main page.

### Why does the editor use a lower height in the FactBox?

The FactBox variant is designed for the narrower FactBox column at the side of the page and is
therefore displayed at a lower height. For longer texts with plenty of editing space, use the large
editor or the enlarged view.
