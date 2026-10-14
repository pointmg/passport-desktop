# QSafePass fork of passport-desktop

Upstream: https://github.com/MarkusJx/passport-desktop at tag `v0.1.2` (commit `458184b98bbeacd8dd644b6a3401043d7ab96907`), MIT.

Why this fork exists: QSafePass (a password manager) does not run prebuilt native binaries it cannot trace to source.
This fork pins the reviewed source and is **built from source in QSafePass CI** (`cargo build --release --locked`).

The only change against upstream: `optionalDependencies` removed from `package.json`
(`passport-desktop-win32-x64-msvc` / `-ia32-msvc` are the upstream author's prebuilt npm binaries - they must never
be installed or shipped by QSafePass).

Source review (QSafePass, 2026-10-14): ~770 lines of Rust/TS; no `unsafe`, no network, no process spawning, no file or
environment access; the only OS calls are `KeyCredentialManager` and `UserConsentVerifier` from Microsoft's `windows` crate.
