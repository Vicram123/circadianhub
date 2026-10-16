# CircadianHub Phase 2 — Jet Lag Planner QA

## Changes made

1. Added local wall-time validation using IANA time zones.
2. Departure or return times that do not exist because clocks jump forward are now rejected with a clear message rather than silently shifted.
3. Repeated local times during fall-back transitions are resolved consistently to the earlier occurrence, and the generated plan includes a note asking users to confirm the intended itinerary time.
4. Return departures must occur after the outbound flight's calculated arrival.
5. Existing fallback behavior remains available for conversion code, but form validation prevents a nonexistent wall time from being used to generate a plan.

## Automated checks

The embedded JavaScript passes `node --check`.

The wall-time conversion harness passed all 10 cases:
- Helsinki winter and summer offsets
- New York before and after daylight-saving transition
- India (+05:30) and Nepal (+05:45)
- Nonexistent spring-forward times in New York and Helsinki correctly return zero candidates
- Repeated fall-back times in New York and Helsinki correctly return two candidates and select the earlier instant

## Important limitations

- These are isolated automated checks of time-zone conversion logic, not full end-to-end browser tests.
- Browser interaction tests could not be completed in this environment.
- The live OurAirports CSV and timeapi.io lookups were not verified against production network responses.
- Airport coordinate accuracy, sunrise/sunset recommendations, circadian phase assumptions, and the scientific validity of schedule recommendations still need specialist review.
- Do not treat this as a clinical validation or guarantee that the planner predicts individual adjustment accurately.

## Deployment recommendation

Deploy to staging first. Test airport selection, outbound and return plans, browser console errors, daylight-saving edge cases, mobile layout, and form validation before production release.
