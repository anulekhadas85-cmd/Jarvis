# JARVIS AI — Flutter Android starter

Futuristic Bengali/English voice assistant with speech recognition, spoken replies, AI chat through a small server, quick app commands, and browser-based web search.

## Important
This workspace does not include a compiled APK. Build the APK on a computer with Flutter and Android SDK installed. The Gemini API key belongs on the backend, **never inside the Android app**.

## Included commands
- `open YouTube` / `ইউটিউব খোলো`
- `open WhatsApp` / `হোয়াটসঅ্যাপ খোলো`
- `open Chrome` / `ব্রাউজার খোলো`
- `open Calculator` / `ক্যালকুলেটর খোলো`
- `open Settings` / `সেটিংস খোলো`
- `search weather in Kolkata` / `সার্চ করো ...` opens Google Search in the browser
- `stop speaking` / `চুপ করো`

Voice recognition depends on an Android speech recognition provider being installed and configured. It is not a permanent always-listening wake word service.

## 1. Configure AI backend
Install Node.js 20+ on a computer/server. In `backend/`:

```bash
npm install
cp .env.example .env
```

Edit `.env` and set `GEMINI_API_KEY` using a key from Google AI Studio. Keep `.env` private and do not commit it. Then run:

```bash
npm start
```

For a physical phone on the same Wi-Fi, use your computer's LAN IP, e.g. `http://192.168.1.10:3000`. Emulator default is `http://10.0.2.2:3000`. Enter the right URL from the app's Settings icon. For production, use HTTPS and add authentication; the simple development backend is not intended to be exposed publicly.

## 2. Build APK
Install Flutter stable and Android Studio/Android SDK. From this folder:

```bash
flutter create . --platforms=android
flutter pub get
flutter run
```

Then build a universal APK:

```bash
flutter build apk --release
```

APK output: `build/app/outputs/flutter-apk/app-release.apk`

Optional smaller APKs per CPU architecture:

```bash
flutter build apk --split-per-abi
```

## 3. Live search note
The `search ...` voice command opens Google Search in the phone's browser. The AI backend itself does not perform web-grounded searches yet; add a search API on the backend if you want answers with live sources rather than browser handoff.

## 4. Security / permissions
- Microphone access is requested at runtime.
- App launching is limited to explicit supported apps and uses Android intents.
- The API key stays on the backend.
- The development manifest permits cleartext HTTP so local Wi-Fi development works. Use HTTPS and disable cleartext for release deployment.
