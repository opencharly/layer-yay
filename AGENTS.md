# AGENTS.md — layer-yay

Standalone candy repo for the `yay` layer — the AUR helper that enables the
`aur:` package section in `charly.yml`. The candy lives in `charly.yml` at the
repo root: the per-distro packages, the download `run:` step, the `check:`
assertions, and the embedded `skill:` entity projected into the marketplace
corpus as `/charly-tools:yay`.

Canonical files:

- `charly.yml` — the `yay:` candy entity and the `yay-skill:` skill entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-tools:yay` — the owning skill. The AUR-helper contract, the `aur:`
  package section, and the builder-image composition. Load before editing or
  troubleshooting the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package/repo
  sections, service declarations). Load before editing any entity field or plan
  step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence — the binary at
  `/usr/local/bin/yay` and `yay --version`.
- The download step resolves the latest yay release asset by a `${BUILD_ARCH}`
  pattern; keep the arch template correct for x86_64 and aarch64.

## Modify this repo

- Edit the `yay:` candy entity AND the `yay-skill:` skill entity in `charly.yml`
  together. The skill is the projected usage source, so a behaviour change not
  mirrored in the skill leaves the corpus stale.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge on
  PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the PR
  body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
