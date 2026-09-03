# Ample private investment brief

GENERATED. Do not edit the deck, index.html, methodology.html or ASSUMPTIONS.md by hand; they are overwritten on every build.

Source of truth:

- `deck-build/model.js` for every dollar, square foot, count, month, stake and valuation
- `deck-build/build-investor.js` for the slide and page structure and the investor narrative
- `deck-build/copy.js`, `landlord.js`, `market.js` and `assumptions.js` for shared copy, team, market figures and build-ups
- `deck-build/theme-gold.js` and `design cue/design-system.md` for the design system
- `private investments/renders/`, `logo.png` and `floorplanv2/` for imagery

Rebuild, then check:

```bash
node deck-build/model.js && node deck-build/build-assumptions.js && node deck-build/build-investor.js && node deck-build/check-investor.js && node deck-build/check-slides.js
```

METHODOLOGY.md in the parent folder is hand-written and explains the priced round.

L-K-Wellness-Ample-4.75M-Private.pdf is a manual PowerPoint export, not a build output.
It does NOT refresh when the deck is rebuilt: re-export it, or it goes stale against the .pptx.
