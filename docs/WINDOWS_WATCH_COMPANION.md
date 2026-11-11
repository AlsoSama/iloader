# Experimental Windows Apple Watch companion support

**Unofficial community build — not an official iLoader release.** This work is experimental. Use at your own risk, and review the source before entering any Apple Account credentials.

## Download the verified build

- **[Successful GitHub Actions build (11 November 2026)](https://github.com/AlsoSama/iloader/actions/runs/43020614046)**
- **[Windows installer artifact: `windows-exe`](https://github.com/AlsoSama/iloader/actions/runs/43020614046/artifacts/13855143172)** — download the ZIP from Actions, extract it and run the Windows installer. A GitHub sign-in may be required.
- GitHub reported the Actions artifact ZIP SHA-256 as `152b78b5dd6085c2f80081b85bd9d54c889226caf07d5666c2d96b6c051b8089`. **This is the ZIP artifact digest, not a hash of the inner EXE.**
- The Actions artifact currently has a GitHub expiration date of **9 February 2027**. This is **not** a permanent GitHub Release attachment.

The build passed the GitHub Actions Windows job. It was tested on one paired iPhone/Apple Watch setup; compatibility across other accounts, devices and software versions has **not** been established.

## Exact tested source

| Component | Repository and reference |
| --- | --- |
| iLoader desktop UI | [`AlsoSama/iloader` at `bef7e279`](https://github.com/AlsoSama/iloader/tree/bef7e279769022ded6618520c1fbaf1f6388c084) |
| isideload backend | [`AlsoSama/isideload` at `323e5341`](https://github.com/AlsoSama/isideload/tree/323e5341b6f02a182e2c913a09ca43f553322758) |
| Active iLoader branch | [`fix/watch-companion-appgroup-27.3b1`](https://github.com/AlsoSama/iloader/tree/fix/watch-companion-appgroup-27.3b1) |
| Active backend branch | [`fix/watch-companion-appgroup-27.3b1`](https://github.com/AlsoSama/isideload/tree/fix/watch-companion-appgroup-27.3b1) |

**Important:** The `main` branch is an upstream fork baseline, **not** the exact source for the Windows download above. The pinned commits are authoritative for reproducing that build.

## What was fixed

1. **Apple Watch companion app installation.** Rewrites companion bundle identifiers consistently with signing and supports installing the paired watchOS app from Windows.
2. **Apple authentication interoperability.** Adjustments to the GrandSlam/Anisette client-information and HTTP client handling for failures encountered as HTTP 503 and HTTP 429.
3. **Apple Watch App Groups.** Registers and associates App Groups for watchOS App IDs, and verifies the generated watchOS provisioning profile contains the expected App Group entitlement. This was necessary for apps requiring a shared group container, such as HermesEnabler.

These changes **do not** bypass Apple's account, device, developer-team, entitlement or service eligibility restrictions.

## How to use

1. Download the Windows `windows-exe` artifact above, extract the ZIP and install the EXE.
2. Use a compatible iPhone paired with an Apple Watch; install Apple's Windows device drivers if needed.
3. Launch iLoader and authenticate using **your own** Apple Account. Two-factor authentication may be required. Use a trusted Anisette service; third-party Anisette providers have their own privacy implications.
4. Import the IPA of an app that actually includes a watchOS companion, then select the paired iPhone for installation. For HermesEnabler, obtain the IPA from the [original project](https://github.com/pookjw/HermesEnabler); it is **not bundled** here.
5. Confirm the watchOS app installed correctly. For tools that modify MobileGestalt, follow the original project's backup and restore directions **before making changes**.

For HermesEnabler specifically, keep the app and its initial MobileGestalt backup until you have safely restored original settings. Deleting the app or erasing its data may delete the only copy of that backup.

## Privacy and security

- **This repository does not publish any personal Apple Account credentials, two-factor codes, local login/session files, signing profiles, private keys, or personal device logs in this guide.** No end-user credentials were supplied to GitHub Actions to build the installer.
- iLoader's source uses Apple authentication and, when credential saving is selected, stores passwords through the operating system's credential store. **That does not prove a third-party binary or Anisette provider is perfectly safe.** Review the source and trust model before use.
- **Do not upload or share** personal login caches, developer certificates/private keys, provisioning profiles, personal device identifiers, modified signed IPAs containing your provisioning data, or unredacted diagnostic logs.
- Binary provenance: download from this exact repository's GitHub Actions run; do not trust repackaged installers from unrelated websites.

## Limits

- Experimental code, tested in only a narrow configuration. A successful build is not a security audit or broad compatibility certification.
- The Windows installer may continue to show the upstream app version in its title; use the **commit hashes and Actions run ID** to identify this build.
- Apple may change private signing/developer endpoints, account throttling, required entitlements, or pairing behavior without notice.
- The Windows artifact expires; a durable GitHub Release download has **not** been created.
- This fork is not affiliated with Apple, iLoader, Sideloadly or HermesEnabler.

## Credits and licensing

Based on [iLoader](https://github.com/nab138/iloader) and [isideload](https://github.com/nab138/isideload), with watch companion support work derived from the [Rzbck forks](https://github.com/Rzbck/iloader) and [isideload companion fork](https://github.com/Rzbck/isideload). The source code licenses are MIT; preserve upstream copyright and license notices. Upstream branding, logos and the iLoader name have **separate restrictions**; see [LICENSE-BRANDING](https://github.com/nab138/iloader/blob/main/LICENSE-BRANDING). Do not imply official endorsement.

---

## 中文快速说明

这是一份**非官方实验版**，用于在 Windows 上侧载包含 Apple Watch 配套应用的 IPA，并修复了 Apple Watch App Group 授权问题。

- 下载：[成功构建记录](https://github.com/AlsoSama/iloader/actions/runs/43020614046)，选择 **`windows-exe`**。
- 对应源码：[iLoader](https://github.com/AlsoSama/iloader/tree/bef7e279769022ded6618520c1fbaf1f6388c084) / [isideload](https://github.com/AlsoSama/isideload/tree/323e5341b6f02a182e2c913a09ca43f553322758)。
- 安装包**不附带 HermesEnabler IPA**；请从原项目取得。务必使用自己的 Apple ID，不要上传账号密码、签名文件、设备 UDID、调试日志等个人数据。
- 本项目**不是稳定正式版**，没有在所有设备和系统版本上验证。若修改过 MobileGestalt，请先备份；未恢复前不要随意卸载相关手表应用。
