# Wilderguard Android beta distribution

This repository serves the signed APKs and signed F-Droid feed for [Wilderguard](https://github.com/Sivivatu/wilderguard), Eric's tower-defense game.

- [Install page](https://sivivatu.github.io/wilderguard-beta/)
- [F-Droid feed](https://sivivatu.github.io/wilderguard-beta/fdroid/repo)
- [Public game source](https://github.com/Sivivatu/wilderguard)
- [Report a problem](https://github.com/Sivivatu/wilderguard/issues)
- [APK releases and checksums](https://github.com/Sivivatu/wilderguard/releases)
- [Release workflow and recovery runbook](https://github.com/Sivivatu/wilderguard/blob/main/docs/publication.md)

## Tag-based publishing

The source repository's [release workflow](https://github.com/Sivivatu/wilderguard/blob/main/.github/workflows/beta-release.yml) is being added for review in [source PR #1](https://github.com/Sivivatu/wilderguard/pull/1). After it is reviewed and merged, a new `vX.Y.Z-beta.N` source tag on reviewed `main` starts the tests and unsigned Android build. Android and F-Droid version metadata must match the tag. An owner approves the protected signing environment before the permanent app and feed keys are used.

CI publishes only the verified public distribution payload here, atomically with a matching distribution tag. It verifies Pages, then attaches the identical signed APK, checksum and source-bound receipt to a prerelease in the source repository. Signing keys and CI credentials stay in encrypted secrets; a dedicated deploy key grants write access only to this distribution repository.

The source tag identifies game source. The same-named tag here identifies the distribution payload; their Git commit hashes are intentionally different. Existing APKs, certificate pins, signed feed history, install URL and feed URL are retained. New publications must increase the version code; beta 9 is already published, so the next new code is at least 10. Never overwrite a version, tag or release asset. CI receipts allow a failed run to resume without regenerating a published feed.

Setting up this workflow does not create another APK release. Beta 9 does not include Sentry reporting. CI keeps reporting disabled until the native crash, offline and device checks documented in the source repository are completed and a configuration change is reviewed. Source maps and debugging archives are not published by CI.

This is a developer-operated custom feed, separate from F-Droid's official catalog. Physical Samsung Tab S4 and actual F-Droid-client update validation remain separate from build/signature checks. Public source visibility does not grant a license; a license has not yet been selected.
