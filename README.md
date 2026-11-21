# MyZong

Customizable Morphe patches for My Zong **5.19.19.112** (`com.zong.customercare`).

Download [MyZong-1.2.22.mpp](https://github.com/FarhanZafarr-9/my-zong-customization/releases/tag/v1.2.22). Import it into Morphe Manager, choose the stock `.112` APK, and select the patches and options you want. The release includes a SHA-256 checksum; GitHub also provides the source archive for its tag.

## Customization

- Charcoal dark mode, optional Android 12+ system Material accents, rounded cards and buttons, styled dialogs, and a quieter startup splash.
- Separate controls for Home promotions, weather, step counter, wallet, regional offers, shortcut sections, SMS card, package line, and loan/recharge controls.
- A Home shortcut allowlist: Rewards and Rs 100 Shop are kept by default. Free MBs is accepted as a Rewards alias. An empty list hides every shortcut.
- Header item selection, optional left-aligned titles, Home title, and Bundles, Free MBs, and loan shortcuts.
- Optional icon-only bottom navigation, individual tab hiding, complete bottom-bar hiding, and starting on Usage.
- Material allowance icons, favorite stars, bundle resource cells, validity chips, and a button beside Search that hides/restores bundle categories, validity chips, and filters. Its state is remembered; scrolling no longer changes it.
- Optional daily reward ad-flow bypass, disabled by default. This is separate from hiding promotional UI.

Options are applied when patching. The Bundles controls button works inside the app without repatching.

## v1.2.22

Replaces automatic bundle-control collapsing with the manual header button, makes the New badge fully rounded, reduces active validity-chip corners, and resolves mapped raw-resource filenames when other patch sources trigger resource decoding.

The bundle built successfully and all 51 selected patches applied to the stock `.112` APK. Binary-XML, first-frame Home layout, and bytecode-hook regression checks passed. The user also confirmed this build works on their phone. The exact combination with Morphe's Disable Play Store patch has not been independently reproduced locally.

Use a consistent signing key for updates. If Morphe and a separately signed APK use different keys, Android requires uninstalling the existing app before switching; uninstalling removes its local data.

## Build

Use Windows PowerShell, JDK 23, Android SDK build-tools 36.0.0, and GitHub CLI. Set the SDK path in `patches/local.properties` and adjust machine paths in `scripts/Build-Bundle.ps1`. The script uses your `gh` login for GitHub Packages and cached Gradle dependencies. For initial dependency downloads, configure `GITHUB_ACTOR` and `GITHUB_TOKEN`, then run the Gradle wrapper without `--offline`.

```powershell
.\scripts\Build-Bundle.ps1
```

Output: `patches/patches/build/libs/patches-1.2.22.mpp`.

Source is in `patches/`; regression fixtures are in `tests/`. Local inputs, signing keys, tools, build artifacts, and analysis work remain outside version control. Older local builds are preserved under `builds/archive/`.

License and upstream attribution: [LICENSE](patches/LICENSE), [NOTICE](patches/NOTICE).
