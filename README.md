# Darak (Attic) — SOHO/Personal NAS Platform

Darak (Korean: 다락, meaning “attic”) is a modern SOHO/personal NAS platform that combines a Kotlin/Spring Boot API server with a cross‑platform Flutter client. It focuses on secure file management, NAS administration, and optional local AI capabilities for private, on‑prem workflows.

This repository contains the Flutter client (Frontend) for Darak.

- API Server (Spring Boot/Kotlin): [Link to API server repository] (TBD)
- Flutter Client (this repo): cross‑platform app for Android, iOS, Web, macOS, Windows, and Linux

## Key Features

- User Management
  - Local user accounts
  - Active Directory (AD) integration and SSO
- Security
  - Security architecture aligned with ISMS‑P principles
  - One‑Time Password (OTP) using Google Authenticator compatible TOTP
  - WebAuthn Passkey support for passwordless MFA (platform authenticators where supported)
- File Management
  - Upload and download
  - Internal sharing (between users)
  - External sharing
    - Link‑based sharing with optional password protection
    - Direct file serving mode (configurable via server policy)
- NAS Management
  - Docker Hub capability
    - List, run, restart, stop, and remove containers on local or configured hosts
  - Web terminal access (secured)
  - System monitoring
    - Process and memory utilization
  - Storage management
    - Check storage capacity/usage
    - Per‑user storage quotas
    - External storage connectors
      - USB media
      - Google Drive
      - Microsoft OneDrive
      - WebDAV servers
      - AWS S3 API compatible object storage
- Chatbot (Private AI)
  - Select and run a small LLM (sLLM) locally when system memory ≥ 4 GB
  - RAG: vectorize uploaded files and query via retrieval‑augmented generation

## Architecture Overview

Darak follows a client–server model:
- Backend: Kotlin/Spring Boot API server exposing authentication, storage, NAS orchestration, and AI endpoints.
- Frontend: Flutter application (this repo) that provides a unified UI to manage files, devices, and AI features across platforms.

Communication is secured via HTTPS and token‑based authentication (with OTP and WebAuthn options). External storage and Docker hosts are configured server‑side and surfaced in the client.

## Repository Scope (This Repo)

This repository includes the Flutter app code, build configuration, and platform shells for:
- Android, iOS, Web, macOS, Windows, and Linux

If you are looking for server APIs or backend configuration, see the API server repository (link TBD).

## Getting Started (Frontend)

### Prerequisites
- Flutter SDK (stable channel)
- Dart SDK (bundled with Flutter)
- Platform toolchains as needed:
  - Android: Android Studio, SDK/NDK, device/emulator
  - iOS/macOS: Xcode, Cocoapods
  - Web: Chrome or supported browsers
  - Windows/Linux: native toolchains supported by Flutter

Check your setup:

```
flutter doctor
```

### Install Dependencies

From this directory:

```
flutter pub get
```

### Configure API Endpoint

The frontend communicates with the Darak API server. Set the base URL via one of the following patterns (choose what your project standards allow):
- Build‑time environment (e.g., --dart-define):
  - `flutter run --dart-define=API_BASE_URL=https://your-darak-api.example.com`
- Config file (if implemented in your fork):
  - e.g., `lib/config/app_config.dart` or `.env` consumed at runtime

Note: Ensure the server has CORS configured for web builds.

### Run

- Android/iOS (device or emulator):
```
flutter run
```

- Web:
```
flutter run -d chrome
```

- Desktop (platform dependent):
```
flutter run -d macos   # or windows / linux
```

### Build

- Android (APK/AAB):
```
flutter build apk
flutter build appbundle
```

- iOS:
```
flutter build ios
```

- Web:
```
flutter build web
```

- Desktop:
```
flutter build macos   # or windows / linux
```

## Security Notes

- OTP (TOTP): The frontend supports enrolling and verifying TOTP codes compatible with Google Authenticator. Enrollment QR and recovery flows are provided by the server.
- WebAuthn Passkeys: Where supported, the client triggers platform/WebAuthn flows for registration and authentication. Availability depends on device/OS/browser support and server policy.
- ISMS‑P alignment: Backend policies (logging, data retention, encryption at rest, least privilege) are enforced server‑side and surfaced via UI where applicable (e.g., password policies, sharing protections).

## File Sharing Details

- Internal sharing: Invite other Darak users/groups with configurable permissions.
- External sharing:
  - Link mode: Create a sharable URL with optional password and expiration.
  - File‑serving mode: Direct serve with access controls per server configuration.

## NAS Management Details

- Docker host configuration is managed on the server. The client provides UIs to view containers, pull images, and perform lifecycle actions (run/restart/stop/remove).
- Web terminal sessions are proxied via the server with audit/logging.
- Monitoring panels display process/memory stats provided by the backend.
- Storage:
  - View total and used capacity.
  - Per‑user quotas are enforced by the server; the client surfaces warnings and usage meters.
  - External storage connectors (USB, Google Drive, OneDrive, WebDAV, S3‑compatible) are configured via the server and accessible in the client’s file views.

## Chatbot and RAG

- Local sLLM execution is available when the host meets minimum specs (≥ 4 GB RAM). Model selection and runtime are managed by the server; the client provides controls and chat UI.
- RAG functionality indexes uploaded files (vectorization done server‑side) and enables semantically‑enhanced answers in chat.

## Roadmap (High‑Level)

- Enhanced admin dashboards and alerts
- Additional external storage providers
- Offline‑first sync improvements
- Expanded WebAuthn device support matrix

## Contributing

Contributions are welcome! See:
- [CONTRIBUTING.md](CONTRIBUTING.md)
- [CONVENTION.md](CONVENTION.md)

Please open issues for bugs and feature requests. For substantial changes, discuss via an issue first to align on design.

## License

TBD (See LICENSE when available). If you are packaging this for distribution, ensure compliance with third‑party licenses and your organization’s security policies.

## Related Repositories

- API Server (Spring Boot/Kotlin): Link TBD
- Flutter Client (this repository)

## Acknowledgements

- Flutter, Dart
- Spring Boot, Kotlin
- WebAuthn standards and the broader open source community
