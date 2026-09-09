# Pull Request: Add tests, CI, KaTeX, Room persistence, and ingest improvements

This branch adds the following features and improvements:

- Render math using Markwon + KaTeX (no WebView).
- Add Room persistence for notes with a polymorphic Gson TypeAdapter for Block (Text/Math/Bash).
- Add a Room migration (1 → 2) that normalizes existing rows to typed/versioned JSON.
- Improve IngestUtils to extract multi-line fenced code (```lang ... ```), detect bash/sh, and extract <annotation> LaTeX.
- Add unit tests for ingest edge cases and the BlockTypeAdapter (round-trip and backward compatibility).
- Add an instrumented UI test verifying clipboard ingestion via MainActivity.
- Add a GitHub Actions CI workflow with two jobs: build (assemble + unit tests) and instrumentation (start emulator and run connectedAndroidTest).

How to run locally

- Unit tests: ./gradlew test
- Instrumented tests (requires emulator/device): ./gradlew connectedAndroidTest
- Build debug: ./gradlew assembleDebug

Notes

- The Gson TypeAdapter writes a "version" and a "type" discriminator to support future migrations. It also falls back to detect older JSON that lacks "type".
- The Room migration attempts to rewrite existing rows using the adapter; it skips rows that fail parsing to avoid data loss.

If you'd like changes before merging (e.g., make the PR a draft, tweak CI, or reduce emulator API level), tell me and I will update the PR.
