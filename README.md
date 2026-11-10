# encore-media

The images the Encore app shows, served from jsDelivr at a tag:
`https://cdn.jsdelivr.net/gh/skymansandy/encore-media@m<N>/<path>`.

**Generated, never edited by hand.** The lossless masters live in the private `encore-exercises` repo (`art/`).
Change art there, then:

```bash
cd ../encore-exercises
uv run encx art export ../encore-media --base-url https://cdn.jsdelivr.net/gh/skymansandy/encore-media@m<N+1>/
cd ../encore-media && git add -A && git commit -m "Media m<N+1>" && git tag m<N+1> && git push --tags origin main
```

Then point the app at the new tag: copy `media.json` into EncoreApp (`scripts/sync-catalog.sh --media ../encore-media`)
and `firebase deploy --only remoteconfig`. A tag is cached forever, so never move one: cut the next.

| Path | What |
|---|---|
| `media.json` | The app's `media` config (Remote Config key + bundled default): every screen's image slot |
| `groups/<group>[-before\|-after].webp` | Group art; a day's hero before and after the workout, by its dominant group |
| `muscles/<art id>.webp` | An exercise's muscle art (`art` in the catalogue) |
| `templates/<name>.webp` | Template cards (`image` in the catalogue's templates) |
| `onboarding/` `planner/` `today/` `summary/` `invite/` | Fixed scenes, one per screen slot |

Served as q90 webp at master resolution (`cwebp -q 90 -m 6`).
