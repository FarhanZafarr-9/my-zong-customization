# MyZong

Morphe patch bundle for My Zong **5.19.19.112** (`com.zong.customercare`).

Download `MyZong-1.2.13.mpp` from [v1.2.13](https://github.com/FarhanZafarr-9/my-zong-customization/releases/tag/v1.2.13). In Morphe Manager, import the bundle and select a stock 5.19.19.112 APK. The new daily reward option is off by default. It was validated on the stock APK and still needs a phone test.

The signed APK from the previous build is available in [v1.2.12](https://github.com/FarhanZafarr-9/my-zong-customization/releases/tag/v1.2.12).

## Build the bundle

Use Windows PowerShell, JDK 23, Android SDK build-tools 36.0.0, and GitHub CLI. Set the SDK path in `patches/local.properties` and adjust the local paths in `scripts/Build-Bundle.ps1` as needed. The script uses your `gh` login for GitHub Packages and expects Gradle dependencies to be cached. For the initial dependency download, run the Gradle wrapper from `patches/` with `GITHUB_ACTOR` and `GITHUB_TOKEN` configured and omit the offline flag.

```powershell
.\scripts\Build-Bundle.ps1
```

The bundle is written to `patches/patches/build/libs/patches-1.2.13.mpp`. Source lives under `patches/` and validation fixtures under `tests/`. License and upstream attribution are in `patches/LICENSE` and `patches/NOTICE`.
