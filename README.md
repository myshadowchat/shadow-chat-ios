# Shadow Chat for iOS

The iOS client for **Shadow Chat** — a private, end-to-end encrypted messenger.

This project packages the Shadow Chat app as a native iOS application with
[Capacitor](https://capacitorjs.com/). Builds are produced in CI and shipped
to the App Store.

## Development

```bash
npm install
npx cap add ios
npx cap sync ios
```

iOS build and release are configured in `codemagic.yaml`.
