# Flutter/Dart Style Guide

This document defines consistent coding practices for **Flutter/Dart** frontend development in this project.  
It incorporates secure coding principles aligned with ISMS-P requirements.

---

## 1. General Principles

- **Readability First**: Write code that is easy to read and maintain.
- **Security by Default**: Follow secure coding practices from the start.
- **Consistency**: Apply consistent formatting, naming, and structure across all modules.
- **Peer Review Compliance**: Code should pass security-focused code review before merging.

---

## 2. Code Formatting
- Follow [Effective Dart](https://dart.dev/guides/language/effective-dart/style).
- Use **2 spaces** for indentation.
- Max line length: **100 characters**.
- Organize imports:
  1. Dart core libraries
  2. External packages
  3. Local project files
- Sort each import group alphabetically.

---

## 3. Naming Conventions
- Classes & Widgets: `PascalCase` (e.g., `LoginPage`, `UserCard`).
- Variables & Functions: `camelCase` (e.g., `loadUserData`, `isLoggedIn`).
- Constants: `lowerCamelCase` with `const` (e.g., `maxItems`).
- Private members: Prefix with `_` (e.g., `_buildHeader`).

---

## 4. Widget Structure
- Prefer **StatelessWidget** when state is not needed.
- Use **StatefulWidget** only when internal state changes are required.
- Break down large widgets into smaller, reusable components.

---

## 5. State Management
- Use a consistent state management approach (e.g., Riverpod, Provider, Bloc).
- Keep UI and business logic separated (e.g., use ViewModel/Controller patterns).

---

## 6. Secure Coding (ISMS-P Aligned)
- Validate and sanitize all user inputs (e.g., form fields).
- Avoid storing sensitive data in plain text on device storage.
- Use secure APIs for network communication.
- Obfuscate release builds with `flutter build apk --obfuscate --split-debug-info=...`.

---

## 7. Documentation & Comments
- Use Dart doc comments (`///`) for public APIs.
- Explain the **why**, not just the **what**.
- Keep documentation up to date with code changes.

---

## 8. Testing Requirements
- Use `flutter_test` and mock dependencies.
- Write unit tests for core logic.
- Ensure all tests pass before submitting a PR.

---

## 9. Security Checklist Before Merging
- [ ] No hardcoded secrets or credentials.
- [ ] Inputs are validated and sanitized.
- [ ] Sensitive data is masked or encrypted.
- [ ] Dependencies are updated and free from known vulnerabilities.
- [ ] Debug code is removed.
