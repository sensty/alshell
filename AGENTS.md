# AGENTS.md

## Project mission
Build a lightweight Android app that silently schedules blacklist add/remove operations for a configured phone number using Android system scheduling primitives.

## Core constraints
- Keep the app lightweight.
- Do not add heavy automation frameworks.
- Prefer AlarmManager over JobScheduler for fixed daily times.
- Preserve buildability at every step.
- GitHub Actions must build a debug APK.
- Shizuku integration should be cleanly abstracted and compile-safe even if CI cannot exercise it.

## Architecture rules
- Kotlin only.
- Keep packages organized:
  - ui
  - scheduler
  - receiver
  - executor
  - storage
- Avoid overengineering.
- Every new dependency must be justified by direct product value.

## Behavior rules
- Daily schedule:
  - unblock at work-start time
  - block at off-work time
- Restore alarms after boot.
- Avoid duplicate alarms.
- Make blacklist operations idempotent.

## CI rules
- Maintain `.github/workflows/android-build.yml`
- Ensure `assembleDebug` works.
- Upload APK artifact.
- Prefer stable GitHub Actions versions.

## Honesty rules
- Never claim Shizuku/device behavior was tested in CI if it was not.
- Clearly separate compile-time completion from device-only validation.

## Documentation rules
- README must explain:
  - purpose
  - architecture
  - scheduling design
  - Shizuku integration
  - build steps
  - limitations
