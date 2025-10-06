# iOS OTA Install – GitHub Pages Starter

This folder lets you publish an **Over‑the‑Air (.ipa) install** via **GitHub Pages**.

## What’s inside
- `index.html` – a simple landing page with an **Install** button
- `manifest.plist` – the OTA manifest (edit values)
- `YourApp.ipa` – placeholder filename (replace with your real .ipa)
- `icon57.png`, `icon512.png` – placeholder icons
- `.nojekyll` – disables Jekyll on GitHub Pages so all files serve as-is

## Quick start (5–8 minutes)

1. **Create a new GitHub repo**, e.g. `ios-builds`.
2. Put these files into the repo root (or a subfolder if you prefer).
3. Replace **placeholders** in `manifest.plist`:
   - `com.example.yourapp` → your Bundle ID
   - `1.0.0` → your app version (must match Info.plist inside .ipa)
   - `https://USERNAME.github.io/REPO/YourApp.ipa` → full HTTPS URL to your actual .ipa
   - Icon URLs similarly (or remove the display/full-size image blocks if you don’t want icons)
4. **Add your real .ipa** next to `manifest.plist` and **commit & push**.
5. Enable **GitHub Pages** (Repo → Settings → Pages → Build from Branch → `main` / `/ (root)`).
6. Find your Pages URL, e.g. `https://USERNAME.github.io/REPO/`.
7. Open **`index.html`** at that URL on your iPhone and tap **Install**.

> The **Install** button dynamically constructs the `itms-services://` link to `manifest.plist` in the same directory, so you don’t need to hardcode it on the page.

## Direct link (if you want to share without the landing page)
When you know your `manifest.plist` absolute URL (e.g. `https://USERNAME.github.io/REPO/manifest.plist`), share this:

```
itms-services://?action=download-manifest&url=https://USERNAME.github.io/REPO/manifest.plist
```

## Tips & gotchas
- **HTTPS is required.** GitHub Pages is HTTPS by default.
- The `.ipa` **must be signed** for Ad Hoc/Enterprise and device UDIDs must be included for Ad Hoc.
- Avoid redirects or auth. Links must be **public and direct**.
- If install doesn’t start:
  - Re-check the manifest URLs (must be absolute `https://`)
  - Confirm the **bundle id** and **bundle version** match the `.ipa`’s `Info.plist`
  - Make sure the device UDID is in the provisioning profile (Ad Hoc)
- MIME type for `.plist` should be `text/xml` (GitHub usually serves fine).

## Verifying .ipa metadata (optional)
On macOS:
```
unzip -p YourApp.ipa Payload/*.app/Info.plist | plutil -p -
```
Copy `CFBundleIdentifier` → `bundle-identifier`
Copy `CFBundleShortVersionString` (or `CFBundleVersion`) → `bundle-version`
