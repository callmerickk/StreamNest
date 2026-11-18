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
- Sign out on TV: the "Sign out?" pop-up (PremiumAlert, CloudScreens) gets no remote focus — TV gets its own
  pop-up with Cancel / Sign out focused and reachable (same for other PremiumAlert pop-ups on TV).
- Logs must never be lost: send the log to the cloud right before sign-out and on Exit; while signed out keep the
  lines (and any crash) on the device and send them after the next sign-in; on a crash, try to send it at once.

## Agreed 17 Nov (phone + TV) — waiting for the owner's "final"
- Never show the error screen while untried links remain; keep trying ranked links ("Trying another source…").
- Order: quick-play HLS (Netflix/Prime/Hotstar) → VegaMovies (foreign) / RogMovies (Indian) → 4K HDHUB → rest;
  only seekable streams (HLS, or files that can jump to any minute).
- Upgrades: HLS → VegaMovies/RogMovies when ready; if 4K HDHUB is playing it stays (equal to Vega); if no Vega/Rog
  within ~45 s and the picture is below 1080p → 4K HDHUB. Auto quality never climbs to 4K (4K manual only; an
  "auto 4K" setting maybe later). Slow-connection step-down only after 2+ stalls of 5 s+, same quality from another
  source first.
- Post-credit scenes: TMDB keywords (during/after-credits stinger) say a scene exists. At ~75–80 % watched, look ahead
  at 90–100 % with low-resolution frames (lowest HLS variant / small reads of the file) to find where real picture
  returns after the dark credits; button "Skip to post-credit scene". Found times saved to the cloud so later viewers
  get it instantly (learning).
- Finished titles leave Pick up where you left off: episode done at 90 % or credits/Next-episode pop-up; movie at
  90–95 %. Last existing episode / finished movie → Library › Watched (Rewatch, Details, Remove). A new episode/season
  (TMDB, daily) brings the show back as "New episode · S2E1".
- Labels: S1E1 "Pilot" (never "Up next"); last episode of a season "Season Finale"; of an ended show "Series Finale".
- "Not out online yet" pop-up → "In cinemas only — not online yet" with Remind me · Play cinema copy · Close.
- Cinema copies (cam): judge by name (CAM/HDCAM/TS/HDTS/TC/HDTC/PreDVD = cam; WEB-DL/WEBRip/BluRay/IMAX HD = clean)
  and by service (Netflix/Prime/Hotstar copy of a film TMDB doesn't list on that service in India = cam). Clean copy
  first; cam only if nothing else. While a cam plays, keep looking; a clean copy found later fades in at the same
  frame (phone: two-player fade, no break; TV: kept frame + short sound gap).
- Update 17 Nov (replaces the cinema pop-up idea above): the title page already looks for streams, and 4K HDHUB
  usually answers before VegaMovies — so when Play is pressed and a clean (non-cam) copy is already found, it just
  plays, no pop-up. Only when nothing clean is found: show the "In cinemas only" pop-up (Remind me · Play cinema copy
  · Close). A clean copy found later while the cam plays: fade in at the same frame if the lengths match; if they
  don't, match the frame with cheap low-resolution thumbnails over a wider window, lock there and fade; if no
  confident match, show an "Upgrade to HD" button instead. Never a loading screen; must be quick.

## Agreed 17 Nov — StreamX + Xstream next updates
- First sign-in: remove the "This account has no profiles saved yet" screen. If the account has no profiles, make one
  from the account name and go straight to the profile picker.

## Agreed 18 Nov — StreamX phone + TV, Xstream, Xstream Live
- Seek preview thumbnails per TITLE (not per link): taken cheaply from the quick HLS / MovieBox stream (I-frame track when
  there is one, else lowest variant) at a 10 s spacing, with a crossfade so dragging / ±10 s looks like motion. Kept when
  playback upgrades to VegaMovies / MKV / Live server. Same length (±1 %) → used as is; small difference → scaled to the
  new length + start offset found by matching 1–2 frames; very different (extended cut) → approximate. Saved per title /
  episode on the device (rewatch = no data). Downloads pause while buffering/seeking; capped on mobile data.
- Next episode ready: at ~70 % find the next episode's best link, at ~75 % a paused hidden player loads its first
  8–10 s (from the start or its resume point); Next episode swaps instantly. Dropped if unused; link re-checked on press.
  TV: save the first 10 s to storage instead of a second player.
- Live-server lessons for Quick Play: remember link searches on the device (respect expiry), Home look-ahead (hero,
  Continue, Top 10; 2 at a time), instant green from a remembered link after a 0.1–0.3 s check, 1 s start / 1.5 s after
  seek + keyframe seeks, no hidden swap player, no start-up plugin warm-up.
