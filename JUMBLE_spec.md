# JUMBLE — Game Specification

A daily word-scramble puzzle. Solve 5 six-letter words, then use one circled letter from each to solve a 6th six-letter word.

---

## Core Mechanics

- **Words per puzzle:** 6 total (5 primary + 1 final)
- **Word length:** All 6 letters
- **Final word:** Built from one circled letter per primary word
- **Daily lock:** Only today's puzzle is playable. No archive.
- **Theme:** Every puzzle has a theme, shown at the top
- **Constraint:** Each word has one of each letter (no repeated letters in a single word)

## Layout (top to bottom)

1. Theme + date
2. Five rows for primary words. Each row shows:
   - The scrambled letters (small, above)
   - The answer slots (with the circled letter position marked from the start)
3. The 6th word's answer slots, appearing below as circled letters are revealed
4. Tile bank (where the keyboard would normally sit) — the interactive input

## Pre-Game Screen

- Theme, date, ready button
- For the user's first 3 visits, the "How to play" modal appears here
- Timer does not start until "ready" is pressed
- Timer can be hidden during play if desired

## Input Mechanic

**Scrambled letters** sit above the answer row (small, display-only).

**Tile bank** sits at the bottom (where a keyboard would be). This is the interactive input.

**Cursor:**
- A static (non-blinking) underline marks the active slot
- Tapping any slot moves the cursor there
- Cursor advances right after each tile placement

**Tile bank states (always, regardless of cursor position):**
- Tile placed in the cursor's slot → fully greyed out
- Tile placed elsewhere in the word → grey outline (still tappable, triggers swap)
- Tile not yet placed → fully active
- Spacebar tile → always active, places a blank "?" at cursor

**Placement behavior:**
- Tap active tile → places at cursor, advances cursor right
- Tap grey-outlined tile → swap: source slot becomes blank, cursor slot gets the letter
- Tap filled slot → moves cursor there, no other change
- Backspace → removes letter at cursor, returns to bank
- Clear button → wipes entire guess, all letters return to bank
- Enter button → greyed out unless all 6 slots have real letters (no blanks)

## Submission

- Only real words (in the puzzle's word list) can be submitted; non-word guesses are rejected with a subtle shake
- Correctly placed letters from a wrong guess remain in place (easy mode default)
- The circled letter, if landed correctly during any submitted guess, becomes revealed in word 6

## Hard Mode

- Only one word visible at a time
- Cannot move to the next word until current is solved
- Remaining word rows still show as placeholders (space is preserved)

## Hint Button

- Reveals the first unsolved letter in the current word
- Greyed out at start
- Quietly becomes available after 10 seconds of inactivity on current word
- Never animated, highlighted, or attention-grabbing

## Badges (saved quietly in browser, no email)

Examples (not exhaustive):
- "Solved without mistakes"
- "Solved in under 15 seconds"
- "First try on every word"
- "Hard mode clean"

Badges only display after they're earned. No preview list. No goal-chasing.

## Completion Sequence

1. Confetti
2. Timer result
3. Share card with options to share

## Share Card

Shows:
- Time
- Mode (easy/hard, indicated by icon/emoji)
- Whether hints were used

## Shared Text (via iOS/Android share sheet)

```
[Theme]
[Time]*  ← asterisk if hard mode, no explanation given
Play JUMBLE → [link]
```

## Feedback

- In-game text box
- Sends an email to the creator (you)

## Visual Design

- Clean, minimal
- Lots of white space
- Simple typography
- Black and white feel
- No animation or color that pulls focus away from the puzzle

## Brand

- Name: **JUMBLE** (with the E circled, styled like a solved word)
- One puzzle per day, locked to today's date

## Data Storage

- All progress, badges, settings (easy/hard mode, timer visibility, first-visit count) saved in browser localStorage
- No accounts, no email collection, no server-side database needed

## Word List Format (curated by creator in advance)

```javascript
const puzzles = {
  "2026-06-01": {
    theme: "Ocean Life",
    words: [
      { scrambled: "ALMSON", answer: "SALMON", bonusIndex: 2 },  // bonus letter is "L"
      { scrambled: "RUCNIH", answer: "URCHIN", bonusIndex: 0 },  // bonus letter is "U"
      // ... 3 more
    ],
    finalWord: "LUMBER"  // built from the 5 bonus letters in order
  }
};
```
