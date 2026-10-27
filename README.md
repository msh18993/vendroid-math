# VendroidEnhanced math build

Custom Vencord web build for VendroidEnhanced, reusing a patched BetterMarkdown renderer.

## Install

In VendroidEnhanced:

1. User Settings → VendroidEnhanced Settings.
2. Set Client mod to Vencord.
3. Other → Open developer settings → Vencord location.
4. Enter `https://msh18993.github.io/vendroid-math/browser.js`.
5. Force-stop the app in Android app settings, then reopen it.
6. Vencord → Plugins → enable BetterMarkdown; enable Math in its settings.

The build is downloaded on a cold app start. No PC or Tailscale connection is required, but internet access to GitHub Pages and the pinned KaTeX CDN is required. Do not install unknown replacement bundles: client modifications execute inside Discord.

## Scope and evidence

- Reuses the patched desktop BetterMarkdown source, including Markdown preservation and multipart display-math handling.
- Includes VendroidEnhanced plugins and the official mobile plugin blacklist.
- Embeds matching core/plugin CSS in `browser.js`; suppresses only the APK's conflicting stock core CSS link.
- Retains the APK-provided Android bridge and unrelated styles.
- Uses the current Vencord Modal API and the real managed mobile-style import.
- Carries the clean-heading style; no desktop hover/sidebar settings are included.
- Host parser, TypeScript, packaging and Chrome CSS/KaTeX smoke tests passed.
- **Actual Android installation, message rendering, copying and cold-start behavior remain unverified until device testing.**

Ordinary Discord is the recovery fallback. If the build fails, disable BetterMarkdown or restore the stock client bundle through VendroidEnhanced recovery. Preserve the previous custom URL before editing it. A stock reset removes the custom renderer.

## Source and licenses

`docs/source.zip` is the corresponding build source, including build scripts, the patched plugin and mobile additions. It excludes Git metadata, node_modules, local settings, logs, conversations and private test fixtures. **Read the archive's `REBUILD.md` first:** it describes the local Git-initialization prerequisite and version-display environment variables needed when rebuilding outside the original checkout. Then install the package-manager version pinned in `package.json`, run `pnpm install --frozen-lockfile`, `pnpm buildWeb --skip-extension`, and `node scripts/packageVendroid.mjs --out ../site`.

- Vencord and this integration: GPL-3.0-or-later, see LICENSE.
- VendroidEnhanced plugins: upstream GPLv3; source provenance is included.
- BetterMarkdown: MIT, as declared in its upstream README; original notices preserved.
- KaTeX 0.16.21: MIT, loaded from jsDelivr; not included in the bundle.
- Additional bundled dependency notices: `docs/browser.js.LEGAL.txt`.

This is an unofficial client modification, not an official Discord, Vencord or VendroidEnhanced release. Discord's client-modification policy applies; account safety cannot be guaranteed.
