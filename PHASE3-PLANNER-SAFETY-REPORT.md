# CircadianHub Phase 3 — Planner Safety and Recommendation Review

## Scope
This revision builds on the Phase 2 package and makes targeted wording changes in `jetlag.html`. It does not claim that the planner's circadian recommendations have been clinically validated.

## Changes made
- Added a visible general-guidance note to generated plans. It explains that the schedule is not individualized medical advice, sunrise/sunset cues are approximate, users should not restrict needed sleep or drive while drowsy, and melatonin should be discussed with a qualified clinician in relevant circumstances.
- Replaced three categorical “Do not sleep now” instructions with “Avoid a long nap if safe” wording and explicit permission to take a short nap when very sleepy.
- Added a warning not to drive or do hazardous tasks while drowsy in those nap-related instructions.
- Softened the flight daytime recommendation: it no longer tells users to stay awake as a default; it advises flexibility and says not to force wakefulness when very sleepy.

## Checks performed
- Confirmed the three former “Do not sleep now” labels are no longer present in the planner source.
- Confirmed all three updated nap labels, the general guidance note, and the softened flight-sleep wording are present.
- Extracted the embedded JavaScript and ran Node.js syntax validation.
- Verified the resulting ZIP archive can be opened and tested with `ZipFile.testzip()`.

## Important limitations / next work
- This is a static source-level revision. No full browser-based end-to-end test, real airport-data audit, or live-site test was performed in this step.
- Sunrise/sunset-based light cues are simplified and may be inappropriate in some situations. Light timing can advance or delay the circadian clock depending on biological timing; the planner does not measure an individual's current circadian phase.
- The “hours per day” adjustment estimate is a heuristic, not a prediction of individual recovery. It should be clearly framed as approximate and ideally supported by an evidence review.
- Age, chronotype, and medication flags are not enough to individualize a sleep plan. Do not present the output as treatment for a sleep disorder or as a substitute for clinical advice.
- Before production release, test edge cases in a browser, review all recommendation text with qualified sleep/circadian expertise, and validate local times and airport identifiers against authoritative sources.

## Suggested acceptance criteria
1. No instruction implies that a person should push through dangerous sleepiness.
2. All light cues are labeled general and approximate, with individual-phase limitations explained.
3. Melatonin is not prescribed by the planner; users are directed to a qualified clinician for individualized guidance.
4. UI tests cover long-haul flights, short trips, return trips, daylight-saving transitions, and missing/unusual airport data.
5. The generated plan, print view, and exports include the same relevant caveats.
