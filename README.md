# TGExtra

A Telegram iOS Tweak with support for multiple Telegram variants (Swiftgram, Turrit, and official Telegram).

## Features

- **Ghost Mode** - Browse without leaving traces
- **No Read Receipt** - For messages and Stories
- **Disable Ads** - Clean interface
- **Allow Saving Protected Content** - Save media from protected channels
- **Multi-Variant Support** - Works with Swiftgram, Turrit, and official Telegram

To open the Tweak menu: Long press the screen with 3 fingers (or 4 fingers if Flex is injected).

## Building IPAs

This repository includes GitHub Actions workflows to automatically build and inject TGExtra into Telegram variants.

### Prerequisites

1. Add your `TGExtra.dylib` file to the `/lib` directory
2. (Optional) Add `SideloadFix.dylib` and `NSEFix.dylib` to `/lib` (will auto-download if not present)
3. (Optional for Swiftgram) Add `SwiftgramPro.dylib` to `/lib` to unlock Pro features

### Running the Workflow

1. Go to **Actions** tab in GitHub
2. Select **"Build and Release IPA"** workflow
3. Click **"Run workflow"**
4. Choose options:
   - **Telegram variant**: Select `swiftgram`, `turrit`, or `telegram`
   - **Decrypted IPA URL**: (Optional) Provide a direct URL to a decrypted IPA, or leave empty to auto-fetch
   - **Inject SideloadFix**: Enable/disable SideloadFix.dylib injection
   - **Inject NSEFix**: Enable/disable NSEFix.dylib injection
5. Wait for the workflow to complete
6. Download the patched IPA from the **Releases** page

### Supported Variants

| Variant | Bundle ID | Notes |
|---------|-----------|-------|
| **Swiftgram** | `app.swiftgram.ios` | Supports SwiftgramPro.dylib injection |
| **Turrit** | `com.seastar.turrit` | Standard injection |
| **Telegram** | `ph.telegra.Telegraph` | Official client |

### File Structure

```
TGExtra/
├── lib/
│   ├── TGExtra.dylib          # Required: Main tweak
│   ├── SideloadFix.dylib      # Optional: Auto-downloads if missing
│   ├── NSEFix.dylib           # Optional: Auto-downloads if missing
│   └── SwiftgramPro.dylib     # Optional: For Swiftgram variant only
├── TGExtra.bundle/            # Resources bundle
└── .github/workflows/
    ├── ipa.yml                # IPA build workflow
    └── build.yml              # Tweak build workflow (legacy)
```

## Screenshots

![Screenshot 1](Screenshots/1.png)
![Screenshot 2](Screenshots/2.png)

## Disclaimer

This project is an **independent modification (tweak)** for the Telegram app. I am **not affiliated, associated, authorized, endorsed by, or in any way officially connected with Telegram Messenger LLP**, or any of its subsidiaries or affiliates.

This tweak is created solely for **personal and educational purposes**. Use it at your own risk.

**I do not take any responsibility for any issues, damages, or consequences** resulting from the use or misuse of this tweak. If something breaks, it's not my problem.
