### APNS retreival minimal reproduction

Since while running in development mode the actual bundle identifier is not used and placeholder (e.g. `com.electron.app`) used I did not find the awy to obtain the APNS token in non-MAS builds due to an error `bundle identifier mismtach`.
So few things should be modified in this project to produce a MAS build which can actually get us the APNS token.

1. Provisioning profile allowing the push notification service for the app should be added and be placed instead of `embedded.provisionProfile_placeholder` with the name `embedded.provisionProfile`.
2. Accoerding certificates should be obtained from the Apple developer portal, which are:
  - `3rd Party Mac Developer Installer` that will allow distribution type (PKG) builds to be signed properly.
  - `Apple Distribution:` certificate for the bundled app signing.
3. placeholders within `entitlements.mas.plist` file should be replaced with the actual TEAM ID and actual åpp bundle identifier.

```sh
  # Should produce the signed distribution ready MAS build
  yarn build:mac-dist
```
