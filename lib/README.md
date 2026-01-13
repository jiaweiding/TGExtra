# Dylib Library Directory

This directory contains the dylib files (or .deb packages) that will be injected into the Telegram IPA variants.

## Required Files

Place your dylib files **or** .deb packages in this directory:

- **TGExtra.dylib** or **TGExtra-*.deb** - Main tweak (required)
- **SideloadFix.dylib** - Sideload fix for non-jailbroken devices (optional, will download from GitHub if not present)
- **NSEFix.dylib** - Notification Service Extension fix (optional, will download from GitHub if not present)
- **SwiftgramPro.dylib** or **SwiftgramPro-*.deb** - Swiftgram Pro features unlock (optional, only injected for Swiftgram variant)

> **Note**: The workflow will automatically extract .dylib files from .deb packages if needed.

## Usage

1. Add your dylib files to this directory
2. Commit and push to GitHub
3. Run the "Build and Release IPA" workflow from GitHub Actions
4. Select the Telegram variant you want to build

## Notes

- If SideloadFix.dylib or NSEFix.dylib are not present in this directory, the workflow will automatically download them from their respective GitHub repositories
- SwiftgramPro.dylib is only injected when building the Swiftgram variant
- All dylibs will be signed with ldid during the injection process
