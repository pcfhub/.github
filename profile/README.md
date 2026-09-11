<h1 align="center">PCFHub</h1>

<p align="center">
  <strong>Storybook for the Power Platform.</strong><br>
  Browse, try, configure and install PCF controls without ever opening Visual Studio.
</p>

<p align="center">
  <a href="https://pcfhub.dev"><strong>pcfhub.dev →</strong></a>
</p>

---

## Why this exists

Evaluating a Power Apps Component Framework control usually means cloning a repo,
building it, packing a solution, importing it into a Dataverse environment and wiring
it to a form — twenty minutes of work to answer one question: *does this do what I
need, and what does it look like?*

PCFHub collapses that loop to seconds. Every published control runs **live in your
browser** against a mock `ComponentFramework` context, with an editable property
panel beside it, next to documentation that is versioned alongside the control's
source.

|  | Link directories | PCFHub |
|---|---|---|
| Live interactive demo | ✗ | **✓ hosted, in-page** |
| Change properties at runtime | ✗ | **✓** |
| Canvas + model-driven setup guides | ✗ | **✓ per control** |
| Versioned docs and release notes | ✗ | **✓ with a version switcher** |
| Solution downloads | link out | **✓ hosted, checksummed** |

## What's in this organisation

The controls themselves. Each one is a **public repository of its own**, owned by its
author, and the repository is the source of truth — PCFHub ingests it rather than
building it.

The **Demo** column is the control's own `demo.fidelity`: how much of it the
browser sandbox can run. *Full* means the real control, end to end. *Limited*
means it renders and most of it works, but something the sandbox cannot provide
— a camera, a live Dataverse, navigation — is stubbed and the page says so.
*Mocked* means the writes go to a stand-in Web API. *None* means the page has
docs and downloads but no live demo, usually because the host it needs (the
Power Apps grid) has no browser equivalent.

### Field controls

Bound to one column on a form. Most are plain TypeScript; the ones marked React
build on the platform's own React and Fluent, so neither is bundled.

| Control | What it does | Demo |
|---|---|---|
| [`pcf-barcode-scanner`](https://github.com/pcfhub/pcf-barcode-scanner) | A text field with a device barcode/QR scan button. | limited |
| [`pcf-choices-picker`](https://github.com/pcfhub/pcf-choices-picker) | A Choice or Multi-Select Choice column as a keyboard-accessible picker. React. | full |
| [`pcf-copy-field`](https://github.com/pcfhub/pcf-copy-field) | A text column with a copy-to-clipboard button and a confirmation. | full |
| [`pcf-date-range-picker`](https://github.com/pcfhub/pcf-date-range-picker) | Pick a start and end date as one range, on a two-month calendar. React. | full |
| [`pcf-file-drop`](https://github.com/pcfhub/pcf-file-drop) | Drop a file onto a form and keep it in the column. | limited |
| [`pcf-geo-stamp`](https://github.com/pcfhub/pcf-geo-stamp) | Stamp the device's location, and optionally a photo, onto a record. | limited |
| [`pcf-lookup-search`](https://github.com/pcfhub/pcf-lookup-search) | A lookup column as a type-ahead search over the target table. React. | limited |
| [`pcf-process-flow`](https://github.com/pcfhub/pcf-process-flow) | A choice column as a Business Process Flow stage bar. | full |
| [`pcf-sla-timer`](https://github.com/pcfhub/pcf-sla-timer) | A live countdown to a deadline column, with warning and overdue states. | full |
| [`pcf-star-rating`](https://github.com/pcfhub/pcf-star-rating) | A numeric column as an accessible star rating. | full |
| [`pcf-toolkit`](https://github.com/pcfhub/pcf-toolkit) | Link Toolkit: render a URL column as a real link, on a form and in a view. | limited |

### Buttons

A form has no native button. These two raise an event the app can handle — one
per host, because the two hosts handle events differently.

| Control | What it does | Demo |
|---|---|---|
| [`pcf-action-button`](https://github.com/pcfhub/pcf-action-button) | A button for canvas apps that raises `OnSelect`, with an optional two-step confirm. | limited |
| [`pcf-form-action-button`](https://github.com/pcfhub/pcf-form-action-button) | A model-driven form button that raises an event a form script can handle, confirm and answer. | limited |

### Dataset controls

Bound to a view — a subgrid, a canvas gallery's data source, or a related-records
list — rather than a column.

| Control | What it does | Demo |
|---|---|---|
| [`pcf-attachment-list`](https://github.com/pcfhub/pcf-attachment-list) | The notes and attachments on a record, with download. | limited |
| [`pcf-compact-list`](https://github.com/pcfhub/pcf-compact-list) | A Dataverse view as a stacked list of records, for narrow spaces. | limited |
| [`pcf-data-table`](https://github.com/pcfhub/pcf-data-table) | A sortable, filterable table over any Dataverse view, with inline editing and pinned columns. React. | limited |
| [`pcf-kanban-board`](https://github.com/pcfhub/pcf-kanban-board) | A Dataverse view as a drag-and-drop board, grouped by a choice column. React. | limited |
| [`pcf-row-commands`](https://github.com/pcfhub/pcf-row-commands) | Open a record, launch a URL, or delete it with a confirm, from the row itself. | limited |
| [`pcf-sparkline`](https://github.com/pcfhub/pcf-sparkline) | A compact trend chart over any Dataverse view. | limited |
| [`pcf-tag-list`](https://github.com/pcfhub/pcf-tag-list) | A many-to-many tag picker rendered as removable chips, bound to a dataset. React. | mocked |
| [`pcf-view-filter`](https://github.com/pcfhub/pcf-view-filter) | A search box that filters the view server-side. | limited |

### Grid customizers

Not controls a maker places, but renderers the Power Apps grid loads for a column
type. They only exist inside that grid, so the hub either stands in a mock grid
host or shows docs and downloads without a demo.

| Control | What it does | Demo |
|---|---|---|
| [`pcf-grid-cell-styler`](https://github.com/pcfhub/pcf-grid-cell-styler) | Fluent cell renderers and editors for the Power Apps grid, driven by column type. | mocked |
| [`pcf-grid-data-bars`](https://github.com/pcfhub/pcf-grid-data-bars) | In-cell proportional bars for bounded numeric columns on the Power Apps grid. | none |

### Everything else

[`_template`](https://github.com/pcfhub/_template) is the starting point for a new
control — the layout below, already wired up, in four variants: a plain field
control, a dataset control, a React (virtual) control, and a grid customizer. It
also owns the **shared CI**: every control repository's `build.yml` and
`release.yml` are thin callers of the reusable workflows in the template, pinned
to `@v1`, so a fix to the pipeline reaches every control instead of the one that
happened to be edited.

The portal that hosts all of this is a private repository; the controls are not.

A control does not have to live in this organisation to be on the hub —
[Code Editor](https://pcfhub.dev/components/pcf-code-editor), a Monaco editor for
JSON, XML and other code in a multiline column, sits in its author's own account.
The catalog is invite-only, and which controls get added is decided case by case.

## Anatomy of a control repository

```
pcf-<control>/              # from https://github.com/pcfhub/_template
├─ <Control>/
│  ├─ ControlManifest.Input.xml
│  ├─ index.ts
│  ├─ strings/              # .resx in en, es, fr, de, ja
│  └─ components/  css/
├─ Solution/                # cdsproj → managed + unmanaged zips
├─ docs/                    # overview · installation · canvas · model-driven ·
│                           # api · examples · limitations · faq · migration
├─ media/                   # logo, screenshots, poster — mirrored by the hub
├─ dev/                     # a stand-in host: npm run smoke / harness / preview
├─ scripts/                 # template setup, and the CI guard that keeps it adopted
├─ SPEC.md                  # what building it corrected: verified vs. read
├─ pcfhub.json              # the hub manifest: identity, category, links, demo presets, fidelity
└─ .github/workflows/       # build.yml + release.yml → pcfhub/_template reusable workflows @v1
```

Every control ships its maker-facing strings in English, Spanish, French, German
and Japanese, and styles itself after Fluent whether or not it uses React.

A tagged release builds the control, packs the solution and publishes the demo bundle.
PCFHub picks up the release — from a webhook within seconds, or from the hourly sweep
otherwise — mirrors the artifacts, compiles `docs/*.md` into a version-pinned
documentation set, and imports it as a draft. A person publishes it; from then on
the new version appears on the site with docs, demo and downloads together.

## Running a control in the browser

The demo harness loads each control on a **separate origin**, inside an iframe without
`allow-same-origin`, and talks to it only over `postMessage`. Third-party control code
never shares an origin with your session. Behind that boundary sits a mock
`ComponentFramework` context — parameters, datasets, formatting, resources and Web API
stubs — so the property panel drives the real control, not a screenshot of one.

Some things a sandbox genuinely cannot do (camera, device APIs, a live Dataverse, the
Power Apps grid). Where that is true, the control's page says so on the demo itself
rather than quietly failing, and the repository's `demo.fidelity` says so up front.

## Getting a control onto the hub

The hub is invite-only: controls are added by arrangement, not by submission. If
you have one you would like considered, open an issue here with a link to it. What
a repository needs to be ingestible:

1. The layout [`_template`](https://github.com/pcfhub/_template) sets up, with
   `docs/` and `pcfhub.json` kept in the repo.
2. A tagged release carrying the managed and unmanaged solutions and the demo bundle.

Controls stay under their author's ownership and licence. PCFHub links back to the
repository from every page and counts downloads on the author's behalf.

## Contact

Questions and bug reports: open an issue on the relevant control repository, or on
this one for anything about the site itself.
