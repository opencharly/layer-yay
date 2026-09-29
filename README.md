# layer-yay

The [yay](https://github.com/Jguer/yay) AUR helper for OpenCharly Arch-based
builds.

The `yay` candy downloads the latest yay release binary to `/usr/local/bin/yay`
and pulls `base-devel` + `git` (on Arch) for building AUR packages. It enables
the `aur:` package format in `charly.yml`: any candy with an `aur:` section
requires a builder that has the `yay` candy (and the `builds: [aur]` capability).

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `yay` |
| Binary | `/usr/local/bin/yay` |
| Packages | `base-devel`, `git` (arch) |
| Enables | the `aur:` package section in `charly.yml` |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a builder box's `candy:` list:

```yaml
my-builder:
  candy:
    base: arch
    candy:
      - '@github.com/opencharly/layer-yay:v2026.240.0121'
```

Then AUR packages build through a candy's `aur:` section. The candy's `plan:`
downloads the latest yay release binary (arch-aware via `${BUILD_ARCH}`) and
asserts the binary at `/usr/local/bin/yay` and `yay --version` reporting a
version.

## Layout

- `charly.yml` — the `yay:` candy entity (the per-distro packages, the download
  `run:` step, the `check:` assertions) and the embedded `yay-skill:` skill
  entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-tools:yay`
- `/charly-distros:arch-builder` — the Arch build infrastructure image
- `/charly-coder:build-toolchain` — C/C++ build tools (also in `arch-builder`)
- `/charly-distros:arch-aur-test` — test candy that validates AUR builds
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
