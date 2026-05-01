# Noctalia Habitica Release Checklist

Use this checklist before submitting the plugin to the community catalog or opening a publication PR.

## Scope And Safety

- [ ] Confirm the standalone plugin lives at the repository root.
- [ ] Review the diff and keep changes limited to this plugin package unless a broader repo change is strictly required.
- [ ] Confirm the current implementation still preserves the existing refresh throttling and avatar sprite rendering behavior.

## Sensitive Data

- [ ] Verify `.gitignore` still ignores `settings.json` and `cache/`.
- [ ] Verify `settings.json` and `cache/` are ignored by Git:

```bash
git check-ignore -v \
  settings.json \
  cache/habitica.json
```

- [ ] Package from Git-tracked files only. Do not include ignored local state in release archives.
- [ ] Run a local credential scan before publishing:

```bash
rg -n -i --hidden --glob '!README.md' --glob '!.gitignore' \
  '(habitica(Api)?Token|x-api-key|x-api-user|bearer|api[_-]?token|user[_-]?id)' \
  .
```

## Functional Validation

- [ ] Load the plugin locally in Noctalia.
- [ ] Open plugin settings and paste a valid Habitica User ID and API Token.
- [ ] Confirm the bar widget loads and refreshes normally.
- [ ] Confirm the panel opens without QML runtime errors.
- [ ] Confirm manual refresh works.
- [ ] Confirm scoring a daily or todo still refreshes the UI after the API request completes.
- [ ] If habits are enabled, confirm up/down scoring still works.
- [ ] If checklist items are enabled, confirm checklist toggling still works.
- [ ] If tag filtering is enabled, confirm tasks are filtered by the selected tag ID.
- [ ] Confirm the avatar still renders from official Habitica sprites.

## Documentation

- [ ] README includes description, features, install, setup, usage, privacy, troubleshooting, and API references.
- [ ] README links to the Habitica API docs: `https://habitica.com/apidoc/`.
- [ ] README states that avatar rendering uses official Habitica sprite assets.

## Community Submission

- [ ] Verify `manifest.json` metadata is final for the release version:
  - `name`: `Habitica for Noctalia`
  - `version`: intended community release version
  - `minNoctaliaVersion`: `3.7.1` or newer if compatibility changes
  - `description`: still matches the shipped feature set
  - `repository`: `https://github.com/Vasqs/noctalia-habitica` in the standalone repository
  - `repository`: `https://github.com/noctalia-dev/noctalia-plugins` in the community registry PR
- [ ] Capture screenshots or a short demo if the community submission flow benefits from them.
- [ ] Package only the publishable plugin files:
  - `manifest.json`
  - `Main.qml`
  - `BarWidget.qml`
  - `Panel.qml`
  - `Settings.qml`
  - `HabiticaAvatar.qml`
  - `README.md`
  - `LICENSE`
  - `i18n/en.json`
  - `preview.png`
  - `.gitignore`
- [ ] Keep local-only files out of the package:
  - `settings.json`
  - `cache/`
- [ ] Submit through the Noctalia community process or repository requested by maintainers.
- [ ] Wait for review feedback before changing behavior beyond bug fixes or compatibility updates.
