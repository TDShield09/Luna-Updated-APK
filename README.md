# Luna Updated APK

Automatic update source for the Luna mobile client.

The app reads `update.json` (packaged in the APK), compares the newest `version_code` with the
installed app, and when a newer release is present it downloads the APK, checks its SHA-256, and hands
it to Android's own installer. Android always asks the user to confirm the install, so the app can
never replace itself silently.

## Release

| Item | Value |
|---|---|
| **Tag** | `apk-latest` |
| **Asset** | `luna-update.apk` |

Download link used by the app:

```
https://github.com/TDShield09/Luna-Updated-APK/releases/download/apk-latest/luna-update.apk
```

## How a release is published

From the project:

```
node Mobile/tools/publish-apk-release.mjs <path-to-apk>
```

The tool hashes the APK, reads its version and size, rewrites `Mobile/assets/update.json` with the
real link, hash and size, uploads the APK as a release asset, and checks that GitHub reports the same
SHA-256.

## Format of `update.json`

```json
{
  "releases": [
    {
      "version_code": 2,
      "version_name": "0.2.0-port-preview",
      "apk_name": "luna-update.apk",
      "apk_url": "https://github.com/TDShield09/Luna-Updated-APK/releases/download/apk-latest/luna-update.apk",
      "apk_sha256": "…",
      "bytes": 0,
      "notes": "what changed"
    }
  ]
}
```

`version_code` must be higher than the installed app's `versionCode` for an update to be offered.
