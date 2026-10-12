# LiquidHunt Android

A free, mobile-first crypto dashboard with estimated liquidity zones, price alerts, and a local paper-trading simulator. This project does **not** place real orders.

## Features
- BTC, ETH, BNB, SOL, XRP, DOGE, ADA and LINK markets
- Public Binance Futures 24-hour ticker with Binance Spot fallback
- Estimated buy-side/sell-side liquidity zones based on the 24-hour high/low range
- Price-above, price-below, upper-zone and lower-zone alerts
- Virtual $10,000 paper account; long/short, leverage, TP/SL, manual close, realized/unrealized PnL
- Local persistence in the device's WebView storage
- GitHub Actions workflow to build a debug APK for free on GitHub-hosted runners

## Important limitations
- Liquidity zones are heuristics, not actual liquidation clusters, order-book liquidity or a validated prediction.
- Market endpoints may be unavailable in some regions or networks; app falls back from futures ticker to spot ticker. Spot fallback is clearly labeled.
- Alerts are evaluated while the app is open/active; this initial version does not guarantee background notifications when Android suspends the app.
- Paper simulation omits fees, funding, slippage and liquidation; it is not an exchange execution engine.
- This project has not been device-tested. An APK must be built and installed/tested before release.

## Build APK for free with GitHub Actions
1. Create a free GitHub account if you do not already have one.
2. Create a new **public or private** repository and upload all files from this folder (do not upload `node_modules`).
3. Open **Actions** and enable workflows if GitHub asks.
4. Run **Build LiquidHunt Android APK** from the Actions tab (or push to the main branch).
5. When the workflow completes, open its run and download the `LiquidHunt-debug-apk` artifact.
6. Extract the artifact and install `app-debug.apk` on your Android phone. Android may ask you to allow installs from your browser/file manager. Only install APKs you built or trust.

## Build locally (requires Android Studio / Android SDK)
Requirements: Node.js 20+, Java 21, Android SDK/platform tools and Gradle-compatible Android build environment.

```bash
npm install
npx cap add android
npx cap sync android
cd android
./gradlew assembleDebug
```
APK output: `android/app/build/outputs/apk/debug/app-debug.apk`.

## Project layout
- `www/` — app UI and logic
- `capacitor.config.json` — Capacitor Android app identity/config
- `.github/workflows/android-apk.yml` — hosted APK build workflow

## Privacy
The app stores the paper account and alerts in local device storage. It calls public Binance market-data endpoints. No API keys, exchange credentials or backend server are required.
