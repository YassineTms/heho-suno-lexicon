# heho-suno-lexicon

Open word lists behind the free [Suno lyrics check](https://heho.ai/tools/suno-lyrics-check): the words
Suno tends to mispronounce, the phrases that show up in a large share of AI-written lyrics, the rhyme
pairs the ear predicts, and the Style-field descriptors that contradict each other.

Everything here is plain JSON so anyone can use it, in any tool. Licence: CC BY 4.0 (see LICENSE).

## Files

| File | What it holds |
|---|---|
| `data/pronunciation.json` | Words with more than one reading, silent letters or borrowed spellings, each with respellings that have only one reading (`live` → `liv` / `lyve`). |
| `data/cliches.json` | Phrases that appear in a large share of generated lyrics ("neon lights", "echoes of", "dancing in the rain"). A hit is a signal, not a verdict. |
| `data/dead-rhymes.json` | End-word pairs the listener hears coming (fire / desire, heart / apart). |
| `data/sung-instructions.json` | Words that mark a parenthesis as a stage direction; Suno sings what is inside parentheses, so `(whispered)` becomes a word. |
| `data/style-conflicts.json` | Groups of Style-field descriptors that pull in opposite directions (lo-fi vs bright, whispered vs anthemic). |
| `data/genre-tempo.json` | Tempo assumed per genre when the Style field gives none, used to estimate sung length. |

English only for now. Other languages are welcome as separate `language` values; French and Spanish
are the next two planned.

## How the lists grow

1. **In the tool.** Every pronunciation or cliché finding on heho.ai has a "Not right? Report this
   word" form. Reports land in a review queue.
2. **Here.** Open an issue with the word, the line it was in and what Suno sang, or send a pull
   request editing the JSON directly.

Nothing is merged without a human reading it. Accepted reports are committed here with credit
(the name or handle you give, never an email).

## What makes a good entry

- Pronunciation: a word Suno got wrong in at least two generations, and a respelling that fixed it.
- Cliché: a phrase you have seen in generated lyrics from more than one prompt, not a phrase you
  merely dislike.
- Style conflict: two descriptors that, together, made Suno ignore one of them.

## Using the lists

```js
import pronunciation from './data/pronunciation.json' with { type: 'json' };
const byWord = new Map(pronunciation.entries.map(e => [e.word, e]));
byWord.get('live'); // { word: 'live', reason: 'homograph', respell: ['liv', 'lyve'] }
```

Maintained by [Heho](https://heho.ai), a lyrics workspace for songwriters and AI-music makers.

## Where the lists are used

The production engine lives in the Heho backend (`api/services/lyrics_check/` in the MusicProd repository) and vendors a copy of `data/`. After a merge here, the copy is refreshed and deployed; the JSON in this repository is the source of truth.
