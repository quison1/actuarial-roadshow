# Can You Price the Future?

An interactive workshop deck for high school students on risk, data and the actuarial profession (ANU Actuarial Roadshow). The deck is built with [Quarto](https://quarto.org) as a reveal.js presentation.

- **Live deck:** https://quison1.github.io/actuarial-roadshow/
- **On-screen dice for the game:** https://quison1.github.io/actuarial-roadshow/dice.html

## Rendering the deck

Defaults (what the public site shows):

```bash
quarto render can-you-price-the-future.qmd
```

One preset:

```bash
quarto render can-you-price-the-future.qmd --profile with-photo
```

Several presets, separated by commas with no spaces:

```bash
quarto render can-you-price-the-future.qmd --profile with-photo,no-phones
```

The output is a single self-contained file, `can-you-price-the-future.html`, which opens offline in any browser. Press **S** while presenting to open the speaker notes, which include timings.

## Settings

Optional slides and slide parts are switched on and off under `show:` in `_quarto.yml`. These are the defaults:

| Setting | Default | What it controls |
|---|---|---|
| `scoreboard` | off | Live team scoreboard during the game |
| `winner` | off | Winner announcement (needs `scoreboard` on) |
| `dice-qr` | on | QR code to the dice page, on the rules slide |
| `more-customers-editable` | off | On "What happens with more customers?", the first row's number of customers is a box you can type into (e.g. the class size) instead of a fixed 20 |
| `testimonial` | on | "In a student's words" slide |
| `testimonial-photo` | off | Student photo on that slide; without it the quotes sit in three columns |
| `vietnam` | off | "Actuaries in Vietnam" slide for Vietnamese students, after the testimonial |
| `sg-my` | off | "Qualifying as an actuary in Singapore and Malaysia" slide, after the testimonial (and Vietnam slide, if on) |
| `backup` | on | "Backup slides" divider and the maths requirement slide |
| `backup-sea` | on | Southeast Asia employers backup slide |
| `backup-extra` | off | Older backup slides: where actuaries work, ANU (5 slides), careers |

## Presets

Each preset is a file named `_quarto-<name>.yml` that changes a few settings. Use it with `--profile <name>`.

| Preset | Changes from the defaults | Slides |
|---|---|---|
| *(none)* | Defaults above | 18 |
| `with-photo` | Photo on | 18 |
| `no-phones` | Dice QR code off | 18 |
| `class-size` | Editable first row on "What happens with more customers?" | 18 |
| `vietnam` | "Actuaries in Vietnam" slide on | 19 |
| `sg-my` | Singapore and Malaysia qualifying slide on | 19 |
| `full` | Scoreboard, winner and older backup slides on | 27 |
| `short` | Testimonial and all backup slides off | 14 |

Useful combinations:

| Session | Profile |
|---|---|
| In-person school visit | `with-photo` |
| School where phones are put away | `with-photo,no-phones` |
| Long workshop | `full,with-photo` |
| Short slot | `short` |
| Short slot, no phones | `short,no-phones` |
| School in Vietnam | `with-photo,vietnam` |
| School in Singapore or Malaysia | `with-photo,sg-my` |

If two presets change the same setting, the one listed last wins.

## Rendering on GitHub

Every push to `main` publishes the default deck to GitHub Pages. To build another version, go to **Actions**, then **Publish deck**, then **Run workflow**:

- **Profile:** any value from the tables above, or blank for the defaults.
- **Publish ticked:** replaces the public deck.
- **Publish unticked:** builds the deck and attaches it to the run under **Artifacts** for 30 days, without changing the public deck. Use this for any version with the student photo.

## Changing the options

- **Change a default:** edit its value in `_quarto.yml`.
- **Add a preset:** create `_quarto-<name>.yml` listing only the settings it changes, for example:

  ```yaml
  # Online session: no QR code, no Southeast Asia slide
  show:
    dice-qr: false
    backup-sea: false
  ```

- **Make a slide switchable:** wrap its include in `can-you-price-the-future.qmd` in a block, then add the setting to `_quarto.yml`:

  ```markdown
  ::: {.content-visible when-meta="show.my-setting"}
  {{< include slides/my-slide.qmd >}}
  :::
  ```

Keep these settings out of the deck's own front matter. Values there override every preset.

## Files

| Path | Contents |
|---|---|
| `can-you-price-the-future.qmd` | The deck: front matter, run sheet and the order of slides |
| `slides/` | One file per slide or group of slides, included by the deck |
| `custom.scss` | ANU colours, fonts and slide styles |
| `images/` | Photos and QR codes |
| `dice.html` | Standalone on-screen die, published next to the deck |
| `_quarto.yml`, `_quarto-*.yml` | Settings and presets |
| `.github/workflows/publish.yml` | Builds and publishes the deck to GitHub Pages |
| `archive/` | Retired slides, not part of the deck |
| `reference/` | Source material (original PowerPoint, brief, proposal) |
