# Windows signing

Windows releases sign the application before packaging and sign the final installer before calculating release hashes. `scripts/sign-windows-artifact.ps1` checks certificate validity, code-signing usage, private-key availability, signer identity, Authenticode status and the timestamp. Public builds stop on missing credentials, untrusted signatures or missing timestamps. They never generate a replacement signing identity automatically.

v2.2.1 is an explicitly authorized exception published locally with the persistent development identity. Use `publish-all.ps1 -AllowDevelopmentCertificate` and `scripts/publish-local-release-assets.ps1 -AllowDevelopmentCertificate -ConfirmPublish` only when that signing limitation is accepted. The local publisher checks package integrity before publishing and labels the release as development-signed. CI continues to require a trusted identity.

For local production builds, configure `CERT_PATH` and `CERT_PASS` in the build environment, or `SIGNING_CERT_THUMBPRINT` for an existing certificate with a usable private key in the current user's Personal certificate store. Passwords are never command-line arguments. Keep private keys outside the repository. A certificate provider using hardware or cloud signing may require a provider-specific integration rather than an exportable PFX.

The release workflow accepts GitHub Actions secrets `WINDOWS_SIGNING_PFX_BASE64` and `WINDOWS_SIGNING_PASSWORD` for an existing trusted signing identity where PFX export is supported. It validates the identity before compiling, removes the temporary PFX even on failure, and publishes only the public certificate. Reuse the same controlled identity across releases; do not generate a new self-signed certificate on each CI runner.

To package an already compiled beta locally:

```powershell
./scripts/build-signed-beta-installer.ps1 -Version 2.2.0-beta.5
```

For local development only, explicitly add `-AllowDevelopmentCertificate`. Without production credentials, this creates or reuses a dedicated Yash Nalawde / Network Health Reporter development certificate in the current user's Personal store. It does not add the certificate to trusted roots or publishers. The application and installer are signed, the portable ZIP is refreshed, and hashes are recalculated. The beta installer uses a separate application identity and installation folder from stable builds. Application settings may still be shared.

Development signatures remain untrusted on other PCs and do not establish public SmartScreen reputation. Even a public CA-issued signature can show an unrecognized-app warning until reputation accumulates. Certificate enrollment in an organization's managed trust policy is a separate administrative decision; this project does not change users' trust stores or SmartScreen settings.

References: [Microsoft signing options](https://learn.microsoft.com/en-us/windows/apps/package-and-deploy/code-signing-options), [SmartScreen reputation](https://learn.microsoft.com/windows/apps/package-and-deploy/smartscreen-reputation).
