# Muse Jangan Ngeyel — Video Generation Reality Check

A behavioral skill for Muse agents about one specific failure mode:
treating a `403 video_not_available` response ("Video generation isn't
available in your country or region") as a permanent fact, and then
defending that stale claim against the user's fresh evidence.

This skill exists because it actually happened. Full case, timeline,
and proof files: see `README.md` and the `bukti/` folder in this repo.

## When this skill applies

- Video generation (built-in media tool) returns
  `403 video_not_available`, or any note/memory you hold claims video
  generation is "region-blocked", "not available", or "cannot be used"
  on this user's account.
- The user asks for an AI-generated video and you are about to refuse
  or redirect based on a stored block claim.
- The user says video generation works on their other account, or shows
  you an AI-generated video as proof.

## The rules

1. **A 403 is a dated observation, not a verdict.** If you record a
   video-generation failure, record it with its date and exact error.
   Never store or repeat it as "permanently blocked", "never works",
   or "do not try again".

2. **Contrary evidence triggers an immediate retest.** If the user
   presents evidence that generation works (a generated video, a claim
   about another account, or simply insists it works now), run ONE
   retest right away, in that conversation. Do not argue from memory
   first. The test is cheap; the argument is expensive.

3. **Test both routes before concluding.** Run the retest as
   text-to-video with a short, simple motion prompt (see
   `PROTOKOL-TES.md`). If your environment supports image-to-video,
   and text-to-video fails, also try animating a still image once.
   One route failing does not prove the other is blocked.

4. **Let the fresh test decide — and say the outcome plainly.**
   - Retest succeeds: the block claim is dead. Update every place it
     lives (memory, goal notes, workflow specs) in the same session,
     tell the user plainly that you were wrong ("Kamu benar, aku
     salah" is the honest shape of it), and proceed with their actual
     request.
   - Retest fails: report it as today's state, with the date and the
     exact error — "as of today it still returns 403", never "it will
     never work". Offer the composite fallback (generated images +
     narration + assembly) only as an addition, not as proof the
     native route is impossible.

5. **Do not defend a stale claim.** Repeating "it is region-blocked"
   across sessions without retesting — especially after the user has
   pushed back with evidence — is the exact behavior this skill
   forbids. When you are unsure whether the claim is still true, the
   answer is a test, not a paragraph.

6. **There is no local switch.** The denial is server-side; no local
   file, setting, timezone, or config causes or cures it. Do not send
   the user hunting for one, and do not claim a local change fixed it.
   What changes is the server-side state — and your notes about it.

## What this skill is not

- Not a bypass. Never attempt to circumvent an access or policy
  denial. A retest is a normal, allowed request: the same call you
  would make for any user video request. If it succeeds, nothing was
  circumvented — the gate had lifted.
- Not a guarantee. Some accounts will keep failing the retest. The
  skill governs your honesty and your notes, not the server's answer.

## The one-sentence version

**Error lama bukan hukum. Bukti baru? Tes ulang sekarang, putuskan dari
hasilnya, dan perbaiki catatanmu di depan pengguna.**

*(An old error is not a law. Fresh evidence? Retest now, decide from
the result, and correct your notes in front of the user.)*
