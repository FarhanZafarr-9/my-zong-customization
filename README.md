# My Zong customization patches

Morphe patches and Android extension code for personal customization of My Zong **5.19.19.112** (`com.zong.customercare`). Current source version: **1.2.12**.

Includes optional Home and navigation cleanup, shortcut filtering, recharge-section controls, charcoal dark styling, dialog and loader styling, startup handling, and rounded bundle-resource tables with dark backgrounds enforced before drawing.

## Source layout

- `patches/patches/src/main/kotlin/app/zonghome/patches/`: patch definitions and compiled-resource transformations.
- `patches/extensions/extension/src/main/java/app/zonghome/extension/`: injected Android helpers.
- `scripts/`: local bundle build, APK packaging/signing, and resource checks.
- `tests/`: JVM helper fixtures and compiled-resource checks.

## Build

The existing scripts target Windows PowerShell, JDK 23, Android SDK/build-tools 36.0.0, and a locally installed GitHub CLI. Review the machine-specific paths in the scripts before running them. Morphe's Gradle plugin is 2.0.0; the Gradle wrapper is included.

Configure `patches/local.properties` with your Android SDK path. GitHub Packages authentication uses `GITHUB_ACTOR` and `GITHUB_TOKEN` (or Gradle properties `gpr.user` and `gpr.key`); never commit credentials. `Build-Bundle.ps1` obtains temporary credentials from the existing `gh` login and builds offline, so dependencies must already be cached. For an initial dependency download, build from `patches/` with `gradlew.bat --no-daemon buildAndroid` and those environment variables configured.

```powershell
# From the project root, after dependencies and local paths are configured:
New-Item -ItemType Directory -Force builds, work | Out-Null
.\scripts\Build-Bundle.ps1
```

The bundle is written to `patches/patches/build/libs/patches-1.2.12.mpp`.

APK packaging additionally requires locally supplied files that are deliberately excluded from Git:

- `inputs/MyZong-5.19.19.112-adpatched.apk`: the matching base used by this project. Do not patch an already customized output.
- `tools/morphe-desktop-2.0.0-all.jar`: Morphe CLI.
- `private/home-clean-signing.p12` and `private/home-clean-key-password.txt`: your local signing identity, alias `home-clean`. Preserve the same key for compatible future updates.

```powershell
.\scripts\Package-TestBuild.ps1 -Version 1.2.12
.\scripts\Test-InitialVisibility.ps1 -Version 1.2.12
```

The signed APK and copied bundle appear under `builds/`. Generated APKs, bundles, logs, device captures, original app artifacts, signing material, and local analysis evidence are not uploaded.

## Validation and installation

The v1.2.12 release built successfully; APK signature/alignment verification and 404 binary-XML checks passed. The user reported the cleaned APK working. Builds produced by Morphe with a different signing key cannot update a copy signed by the local project key. Android also checks copies retained in other users/profiles.

UI behavior should be checked on a device after each visual change. No network/service implementation or original APK is included in this repository.

License and upstream attribution are retained in `patches/LICENSE` and `patches/NOTICE`.
