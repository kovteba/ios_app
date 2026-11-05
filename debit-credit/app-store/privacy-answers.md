# App Store privacy and export-compliance answers

## App Privacy (App Store Connect)

**Answer: "Data Not Collected".**

Rationale:
- All data (accounts, transactions, budgets, receipts) is stored locally on the device and, when the user enables it, in the user's own private iCloud (CloudKit private database). The developer cannot access it.
- The only network requests go to the National Bank of Ukraine (NBU) public exchange-rate API. They carry no personal data and no identifiers, only a date and a currency code.
- No analytics, no advertising, no third-party SDKs, no tracking (`NSPrivacyTracking` = false, no tracking domains).
- Receipt scanning runs on device.

Privacy manifests: `App/PrivacyInfo.xcprivacy` and `Packages/BudgetKit/Sources/Persistence/PrivacyInfo.xcprivacy` declare the UserDefaults required-reason API (CA92.1, 1C8F.1). `AppTests/PrivacyManifestTests` audits source for other required-reason APIs.

## Export compliance

The app uses only encryption provided by the Apple operating system (HTTPS via URLSession, CloudKit). It contains no proprietary or non-standard cryptography. CryptoKit's `Insecure.SHA1` is used only as a hash to derive stable name-based (UUIDv5) ids for the default categories (`Persistence/UUID+NameBased.swift`); it encrypts nothing.

**Answer:** `ITSAppUsesNonExemptEncryption = NO` (set in the app Info.plist via `project.yml`), so no export-compliance question is asked on each upload.
