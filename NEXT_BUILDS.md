# Planned for the next builds (agreed with the owner, not built yet)

## Next StreamX phone build
- Activity log browser (developer view), arranged as:
  1. App: StreamX Mobile · StreamX TV · Xstream Mobile (later: Xstream TV, Windows — added when built)
  2. Versions of that app (newest first), each listed once
  3. Devices on that version: model + account email (one entry per device and account — no duplicates)
  4. The log itself, with Share and Copy
- Merge entries that are the same model + account + version (a "Clear data" used to create a second device id).
- Stable device id: Settings.Secure.ANDROID_ID (survives Clear data) instead of a random id kept in prefs
  (ActLog.devId) — on phone and TV. Old random ids are mapped to the new one on first start so history stays together.
- Carried over from before: Next Episode double poster (hide NextEpisodePill when wnLoad != null); resume after an
  update uses the source, not the dead 127.0.0.1 link; Now playing + fast sync; completion rules (movie 90–95 %,
  episode when Next episode shows); own LGPL FFmpeg (replace NextLib); no "in theatres" reminder for titles opened
  from search.

## Next StreamX TV build
- Stable device id (ANDROID_ID) as above.
- CNC search with the English / original title (Netflix failed on "कृष ३").
- Saved-link resume that hangs with no picture and no error (Young Sheldon S1E1, 0.8.8 log 12:56) → time out after
  8 s and find another link.
