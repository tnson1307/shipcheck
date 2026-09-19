# ShipCheck

A native macOS app that audits your Xcode project against App Store
Connect before you submit — catching IAP mismatches, Privacy Manifest
gaps, and missing App Information/Review fields that cause rejections.

Download the latest build from [Releases](../../releases/latest).

## Command line / CI mode

The same app also runs headless, so drift gets caught the moment it's
introduced instead of only right before you submit:

```sh
/Applications/ShipCheck.app/Contents/MacOS/ShipCheck --ci /path/to/your/project
```

`<path>` must be the folder that directly contains the `.xcodeproj` or
`.xcworkspace` — for a React Native app, that's the `ios` folder, not the
repo root.

This runs the checks that need no App Store Connect account — IAP ID
consistency, Privacy Manifest / Required Reason APIs, and the Additional
Declarations (Export Compliance, permission strings, ATT, Sign in with
Apple, Background Modes) — and exits non-zero if any blocking finding is
found, so it can gate a CI job or an Xcode Run Script build phase.

For a shorter command, symlink it onto your `PATH` once:

```sh
ln -s /Applications/ShipCheck.app/Contents/MacOS/ShipCheck /opt/homebrew/bin/shipcheck
```

Then: `shipcheck --ci .`
