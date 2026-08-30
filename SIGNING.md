# APK signing

The private Android signing key is intentionally **not stored in this public repository**.

Official releases, including 0.3.2, are signed with the same certificate used for the previous ClaimBoard Scanner builds.

Certificate SHA-256:

`42:8B:8E:0A:6D:FB:9E:5E:93:C6:7B:57:CC:74:0E:5D:6E:DE:7B:A8:1B:9B:88:0A:7F:DA:63:47:83:2F:9A:A2`

The GitHub Actions workflow builds an aligned unsigned APK. Release APKs are signed separately with the private keystore and only the signed APK is published.
