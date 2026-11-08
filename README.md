# iPhone Duo App Store Screenshots

An agent skill for turning **real app captures** into App Store screenshot sets for iPhone Duo’s folded outer and unfolded inner displays.

Plan the set, choose matching device frames, compose readable artwork, and check the exported files before handoff. Works with captures from any app framework; capture and design tools depend on your agent environment.

[Install](#install) · [Use the skill](#use-the-skill) · [Deliverables](#deliverables) · [Sources and attribution](#sources-and-attribution)

## What it helps with

| Task | Guidance |
| --- | --- |
| Plan a screenshot set | Choose the build, locales, display targets, orientations, and screenshot order. |
| Capture the app | Use hardware, a simulator, or supplied captures; preserve originals and remove personal data. |
| Compose artwork | Match the device pose, preserve UI proportions, and keep headlines legible at thumbnail size. |
| Export and preflight | Check actual format, dimensions, and alpha; record locale, display, orientation, and order. |

This repository contains instructions and visual references. Your agent needs access to the app or captures and suitable image or design tools to produce artwork. It does not bundle a screenshot generator, simulator, or App Store uploader.

## Install

With Node.js and npm available, install through the [Skills CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add nxdinh94/iphone-duo-screenshot-skill --skill iphone-duo-app-store-screenshots
```

Install for your user rather than the current project:

```bash
npx skills add nxdinh94/iphone-duo-screenshot-skill --skill iphone-duo-app-store-screenshots --global
```

Inspect the available skill without installing:

```bash
npx skills add nxdinh94/iphone-duo-screenshot-skill --list
```

### Manual installation

Clone the repository and copy the **entire skill folder**, including its references, into your agent’s skills directory. Run one of the installation options below. Check for an existing installation before copying so you do not overwrite local changes.

```bash
git clone https://github.com/nxdinh94/iphone-duo-screenshot-skill.git
cd iphone-duo-screenshot-skill

# Codex: user-level installation
mkdir -p ~/.codex/skills
cp -R skills/iphone-duo-app-store-screenshots ~/.codex/skills/

# Claude Code: project-level installation, from your app repository
# Use the absolute path to the clone you just created.
# mkdir -p .claude/skills
# cp -R /path/to/iphone-duo-screenshot-skill/skills/iphone-duo-app-store-screenshots .claude/skills/
```

Start a new agent session after installation. The entrypoint uses `SKILL.md` with YAML frontmatter; `agents/openai.yaml` supplies Codex display metadata and a suggested prompt.

## Use the skill

Provide the app build or capture directory, desired locales, display targets, orientations, brand assets, and output location. If you only need validation, provide the existing export directory.

**Create a set from supplied captures**

```text
Use $iphone-duo-app-store-screenshots to prepare an English App Store
screenshot set from the real captures in ./marketing/captures.
Cover outer portrait and inner portrait. Show the same content before
and after unfolding where the captures allow it. Use our brand assets
in ./marketing/brand and write final files to ./marketing/exports.
Include an export list and flag any missing captures.
```

**Check existing exports**

```text
Use $iphone-duo-app-store-screenshots to preflight ./marketing/exports.
Check format, pixel dimensions, alpha, display, orientation, locale,
and ordering. Review full-size and thumbnail readability and report
which files need changes. Keep the original exports intact.
```

**Prepare localized artwork**

```text
Use $iphone-duo-app-store-screenshots to prepare English and Vietnamese
outer and inner portrait sets from ./marketing/captures.
Use natural benefit headlines for each locale, preserve the actual app
UI, and report missing localized views before finalizing the set.
```

Without usable captures or a runnable build, the agent should identify the missing views and label layout studies as drafts. Final screenshots must show the actual app. Uploading or submitting assets requires a separate user request.

## Workflow

1. **Choose targets.** Confirm the app build, locales, display, orientation, and intended story.
2. **Capture real behavior.** Use demo accounts, check for personal data, and preserve source captures.
3. **Compose each display.** Show a quick outer-display task and an inner-display task that benefits from the available space when supported by the app.
4. **Export and inspect.** Match Apple’s current upload specifications, check the files themselves, and review the sequence at full size and thumbnail size.

The detailed instructions live in [SKILL.md](skills/iphone-duo-app-store-screenshots/SKILL.md). The [source guide](skills/iphone-duo-app-store-screenshots/references/sources.md) includes upload dimensions, optional Figma canvas math, and composition references. Recheck [Apple’s screenshot specifications](https://developer.apple.com/help/app-store-connect/reference/app-information/screenshot-specifications) before preparing final deliverables; the source guide is a maintained reference, not a live specification feed.

## Deliverables

A completed screenshot task should leave:

- Original captures, kept separately from editable artwork and exports.
- Opaque PNG or JPEG exports at the verified target dimensions.
- An export list identifying each file’s locale, display, orientation, and sequence number.
- A preflight report covering file properties, visual review, and any missing views or unresolved issues.

Use filenames such as `en-outer-portrait-01.png` and `vi-inner-portrait-01.png`. Keep standard iPhone exports separate from native Duo exports. These are naming examples, not bundled sample screenshots.

On macOS, inspect an individual export with:

```bash
sips -g format -g pixelWidth -g pixelHeight -g hasAlpha "en-inner-portrait-01.png"
```

Compare width and height with the current specification and confirm `hasAlpha: no`. File checks complement visual review; they cannot establish whether the app is accurately represented or the text is readable.

## Repository structure

```text
iphone-duo-screenshot-skill/
├── README.md
└── skills/
    └── iphone-duo-app-store-screenshots/
        ├── SKILL.md
        ├── agents/
        │   └── openai.yaml
        └── references/
            ├── sources.md
            ├── duo-device-frame-reference.png
            └── duo-composition-example.png
```

The skill is self-contained. Agents load the entrypoint first and consult supporting references as needed. No other skill repository is required.

## Maintenance

Keep the skill name, folder name, installation command, and agent metadata aligned. When changing export guidance, verify the primary Apple source and update the source guide. Keep third-party layout advice distinct from submission requirements.

After editing, check discovery from the repository root:

```bash
npx skills add . --list
```

Confirm that `iphone-duo-app-store-screenshots` appears, every relative reference resolves, and both bundled images open. This checks packaging and discovery; validate generated screenshots separately with real captures and file inspection.

Report corrections or missing workflows through [GitHub Issues](https://github.com/nxdinh94/iphone-duo-screenshot-skill/issues), including the source URL and the affected instruction. Do not attach credentials, private app data, or unredacted personal information.

## Sources and attribution

- [Apple screenshot specifications](https://developer.apple.com/help/app-store-connect/reference/app-information/screenshot-specifications) and [preparation guidance](https://developer.apple.com/iphone-duo/prepare/) are the primary submission references.
- [mirzaaghazadeh/iphone-duo-skills](https://github.com/mirzaaghazadeh/iphone-duo-skills) informed the repository’s skill-distribution structure. This is a separate screenshot-focused skill, not a copy of that collection.
- The supplied skill bundle includes a device frame sheet and a composition example as visual references. Their inclusion does not establish a reusable asset license; retain original attribution and confirm usage rights before adapting or redistributing artwork.
- The source guide links Noah Elhadedy’s Figma kit and its stated CC BY 4.0 license. Credit the creator when adapting that kit’s assets. The Figma kit itself is not bundled here.

No repository-wide license has been declared. Linked documentation, third-party artwork, and trademarks remain subject to their respective owners’ terms. This project is not affiliated with or endorsed by Apple.
