# Projectionist — Design Language

Rewritten 28 August 2026 from two drawn boards rather than from an argument: `wireframes/b/MarqueeA.html` and `wireframes/b/TheRoomA.html`. Tokens live in `projectionist-wireframes/_kitA.txt`.

## The thesis

**The system is the room, not the film.**

A repertory house in Los Angeles has enormous personality and does not change it when the programme changes. The Vista is the Vista whether it is showing Murnau or a midnight Hangover 2. The room is the constant, the film is the variable, and an audience understands that arrangement without being told.

Everything below follows from that. The chrome never comments on what is being screened. It is the place you came to watch it. **A film's own identity appears in exactly one place, the one-sheet, and nowhere else.** The marquee changes weekly. The building does not.

## Expressionism as a lighting model, not a theme

The reference is German Expressionism and the noir that came out of it, taken as technique rather than costume.

The lasting contribution of Caligari is not crooked sets. It is that **light and shadow do the emotional work, and shadow is an active agent rather than an absence**. Noir points the same technique at moral ambiguity: a hard key, deep falloff, things half seen. Sunset Boulevard is lit the way it is because the film is about what a house conceals.

That is also what this product does. A curator takes an audience past the surface of a film into what is going on underneath it. **The design enacts that rather than illustrating it**, which is why there is no set dressing anywhere in this document.

**Light has a direction and a source.** Every surface is legible because something is lighting it. If a screen could be flipped upside down without looking wrong, it is not lit, it is painted, and it is not finished.

## Two states, not three temperatures

The old system had three temperatures. It now has two lighting states, and the difference between them is time of night rather than theme.

**House up.** Everything before and after the film. Warm ambient falling from above with no visible source. Matte, low contrast, no glow. The lobby before a show.

**House down.** The film itself. Near black with a single cold key from above and behind, the way a projector sits over your shoulder. Everything falls off toward the bottom of the screen.

Squint at any two screens from opposite states. They must read as **the same building at a different time of night**. If either reads as a different place, the model has been broken and no token will fix it.

## Palette

| Token | Value | Job |
|---|---|---|
| `--house-up` | `#141210` | Warm ground, before and after |
| `--house-down` | `#0a0b10` | Cold ground, during the film |
| `--paper` | `oklch(0.93 0.005 75)` | Primary type |
| `--gold` | `#f4e4bc` | Warm light. Never a bulb, never hardware |
| `--silver` | `#f2f7ff` | The live signal, rationed |
| `--time` | `oklch(0.72 0.13 240)` | Sync position |
| `--curtain` | `#7c1f2e` | Light on cloth, T-0 and intermission only |
| `--hair` | `oklch(0.30 0.006 60)` | Borders |
| `--dim` / `--dimmer` | `oklch(0.58 / 0.44)` | Secondary and tertiary type |

**Gold is light, not hardware.** It survives the removal of the marquee bulbs because it was never about bulbs. It is the colour of a warm room with the lamps low.

## The live signal

Electric silver is the only thing in the system that says *this is happening now*, and it is rationed to four places: the ON AIR sign and its dot, the curator's name on a firing note, the primary action at showtime, and telestrator ink. Nothing else, ever.

It always carries its glow:

```
color: #f2f7ff;
text-shadow: 0 0 8px rgba(244,248,255,.85), 0 0 22px rgba(150,190,255,.5);
box-shadow: 0 0 7px rgba(255,255,255,.6), 0 0 20px rgba(160,195,255,.55);
```

The cold of it against a warm house is what makes it read. **A resting surface never gets silver and never glows.** On the Marquee, the single on-air card is the only lit thing in a warm dim room, and that contrast is the system working rather than a decorative choice.

## The curtain is a rhythm of light, not a red shape

You never see a cinema curtain evenly lit. You see it raked, almost always from below, and its whole visual identity is vertical bands of light and shadow. That makes it the most Expressionist object in the building, and it is why it survives here when the rest of the memorabilia did not.

So oxblood is **the colour light picks up off cloth**: deep in the folds, warmer where the wash catches. It is never a fill.

```
repeating-linear-gradient(90deg,
  rgba(124,31,46,.05) 0px, rgba(124,31,46,.62) 7px,
  rgba(160,48,64,.30) 13px, rgba(124,31,46,.07) 19px,
  rgba(92,19,28,.02) 27px),
linear-gradient(to top, rgba(244,228,188,.22), transparent 68%)
```

**It parts as darkness opening, not as panels sliding.** The gap is black, and the inner edges catch a cold rim as they turn into the light. A light event, not a stage effect.

Oxblood appears at T-0 and at intermission. Nowhere else, on any screen, for any reason.

## Grain belongs to projected light only

Film grain, scratches and dust appear where light is being **projected**: the leader, the curtain wash, T-0. They never touch chat, the note editor, the Marquee, or any resting surface.

This is what keeps the aesthetic from becoming a filter. It also keeps type legible and stops a phone rendering noise for two hours.

The leader carries the most, and that is true to life: the academy leader is the most-handled few feet of any print, so it is genuinely the most scratched thing in the building.

## Type

- **Archivo Expanded**, 125% width, for title cards and the marquee.
- **Hanken Grotesk** for UI.
- **Source Serif 4** is **the curator's voice**: Liner Notes, the one-sheet, her answers in the wrap. Never chat. Never an interface label. The rule is about whose voice it is, not about which component it is.
- **JetBrains Mono**, tabular, for timecode, countdowns and anything that ticks.

## The chat rule

Chat is the room's default surface, always labelled, and it never leaves the screen. When a curator element fires it settles to a strip at the bottom, then expands back.

In house down, chat lives in the deepest part of the falloff. That is correct rather than incidental: it is the murmur of the room, and it should sit below the beam.

## Always on screen

Once the film runs, the title and the min:sec position are visible on every surface. Intermission shows `paused` with the timestamp. A viewer glancing at their phone always knows what is playing and where the room is.

## Motion

**The beam is struck, then allowed to decay.** Light arriving is an event; light leaving is not. The rise is roughly a third of the fall: `--beam-rise: 220ms` on `--ease-strike`, `--beam-fall: 640ms` on `--ease-decay`. Symmetrical timing makes a note cross-fade rather than land, and the difference is felt immediately even though it is hard to name.

**One cue, then the next. Never both.** When a note fires, chat settles to its strip first, over about `--settle: 900ms`, and the beam comes up as it lands. Moving them together reads as a glitch rather than a cue.

**A note holds long enough to be read twice**, because the viewer looks up at the television in between. Four seconds plus reading time, floored at five and capped at nine. A fixed hold is too long for a short note and too short for a long one.

**Notes fade up like subtitles**: 4px rise, soft haptic, no badge.

**The curtain travels for ten seconds.** Real curtains take eight to twelve, and a fast curtain reads as cheap in a way that is hard to name and easy to feel.

Everything respects `prefers-reduced-motion`. No bounce, no elastic, nothing that draws attention to itself.

## The pre-show ritual

The house settles first, and the leader only begins once the curtain is fully open, so nobody arrives mid-countdown.

| When | What |
|---|---|
| T&minus;30:00 | Doors. The Lobby opens, chat with the curator begins |
| T&minus;10:00 | The house call |
| T&minus;2:00 | The last call: starting in two minutes, cue the film on your TV |
| T&minus;1:00 | The curtain appears behind the chat |
| T&minus;0:25 | Chat settles to a strip, then the curtain begins to part |
| T&minus;0:15 | Fully open. The leader runs on the revealed surface, with grain |
| T&minus;0:00 | The leader ends, the sign ignites, the Room |

**There is no notification at T-1.** The curtain appearing is the one-minute call, and it is a better one: visible, permissionless, and impossible to miss by someone already looking at the screen.

The surface revealed by the curtain is the app's own live area. The leader plays on it, then it becomes the Room. The curtain is not decoration around a screen; it is revealing the thing you will spend two hours in.

Falling behind later is never a failure. It is a reel change.

## Don'ts

- No silver and no glow on a resting surface, prep and session ready included.
- The serif never appears in chat and never on an interface label.
- Marquee gold never appears mid-film, chat handles included; those take paper on the house-down ground.
- Curtain oxblood appears at T-0 and intermission and nowhere else.
- No grain on a resting surface. It belongs to projected light.
- No badges and no unread counters on Liner Notes.
- Intermission stays matte and empty. No countdown glow, no decoration.
- Never design a surface that works for arthouse but not popcorn, or the reverse.

## What was removed, and why it does not come back

Four things were cut in this rewrite. They were all cinema, and together they were a props cupboard rather than a system.

**Marquee bulbs and the chase animation.** Hardware. The gold survives as light, which is what it was always doing.

**The scalloped curtain, and the curtain as persistent chrome.** Four attempts are preserved at [projectionist-explorations](https://github.com/beingmtm714/projectionist-explorations). The curtain now earns its place as a lighting behaviour rather than a motif.

**French New Wave typographic styling.** A second aesthetic voice competing with the first. The type stack survives; the pastiche does not.

**Cinema Paradiso as a reference for the Lobby.** Nostalgia for a different building.

**The academy leader stays.** It is the most widely recognised artefact in the set and it is now lit by the same model as everything else, which is what stopped it being memorabilia.

## Status

The Marquee and the Room are drawn against this system, on the Direction A page of the canvas. **The other nine artboards are still on the old three-temperature model** and are next, followed by `_kit.txt` and then `projectionist-app/src/tokens.css`. Until that is done, `_kitA.txt` and `_kit.txt` both exist on purpose and neither is wrong.
