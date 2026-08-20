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

| Control | What it does |
|---|---|
| [`pcf-tag-list`](https://github.com/pcfhub/pcf-tag-list) | A many-to-many tag picker rendered as removable chips, bound to a dataset. |
| [`pcf-barcode-scanner`](https://github.com/pcfhub/pcf-barcode-scanner) | A text field with a device barcode/QR scan button. |
| [`pcf-choices-picker`](https://github.com/pcfhub/pcf-choices-picker) | A Choice or Multi-Select Choice column as a keyboard-accessible picker. |

[`_template`](https://github.com/pcfhub/_template) is the starting point for a new
control — the layout below, already wired up. The portal that hosts all of this is a
private repository; the controls are not.

A control does not have to live in this organisation to be on the hub —
[Code Editor](https://pcfhub.dev/components/pcf-code-editor), for one, sits in its
author's own account. The catalog is curated rather than open at the moment, so
which controls get added is decided case by case while the hub is young.

## Anatomy of a control repository

```
pcf-<control>/          # from https://github.com/pcfhub/_template
├─ <Control>/
│  ├─ ControlManifest.Input.xml
│  ├─ index.ts
│  └─ components/  css/
├─ docs/            # overview · installation · canvas · model-driven · api · examples · faq
├─ media/           # screenshots, logo, poster
├─ solution/        # cdsproj → managed + unmanaged zips
├─ pcfhub.json      # the hub manifest: categories, tags, demo presets, fidelity
└─ .github/workflows/release.yml
```

A tagged release builds the control, packs the solution and publishes the demo bundle.
PCFHub picks up the release, mirrors the artifacts, compiles `docs/*.md` into a
version-pinned documentation set, and the new version appears on the site — docs,
demo and downloads together.

## Running a control in the browser

The demo harness loads each control on a **separate origin**, inside an iframe without
`allow-same-origin`, and talks to it only over `postMessage`. Third-party control code
never shares an origin with your session. Behind that boundary sits a mock
`ComponentFramework` context — parameters, datasets, formatting, resources and Web API
stubs — so the property panel drives the real control, not a screenshot of one.

Some things a sandbox genuinely cannot do (camera, device APIs, a live Dataverse).
Where that is true, the control's page says so on the demo itself rather than quietly
failing.

## Getting a control onto the hub

Submissions are not open yet — controls are added by arrangement for now. If you
have one you would like considered, open an issue here with a link to it and we can
talk about it. What a repository needs to be ingestible, when that time comes:

1. The layout [`_template`](https://github.com/pcfhub/_template) sets up, with
   `docs/` and `pcfhub.json` kept in the repo.
2. A tagged release carrying the managed and unmanaged solutions and the demo bundle.

Controls stay under their author's ownership and licence. PCFHub links back to the
repository from every page and counts downloads on the author's behalf.

## Contact

Questions and bug reports: open an issue on the relevant control repository, or on
this one for anything about the site itself.
