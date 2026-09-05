# Contributing

Two ways in, both reviewed by a person before anything ships.

**Report from the tool.** On https://heho.ai/tools/suno-lyrics-check, every pronunciation or cliché
finding has a "Not right? Report this word" link. That form captures the word and the line it was in;
add what Suno actually sang. This is the fastest route.

**Open an issue or a pull request here.**

- Pronunciation: `{ "word": "...", "reason": "homograph" | "silent_letters" | "loan_word", "respell": ["..."] }`.
  Say in the issue how many generations got it wrong and which respelling fixed it.
- Cliché: the phrase, lower-case, and two prompts it came out of.
- Dead rhyme: the pair, and why the second word is predictable.
- Style conflict: the two descriptors and what Suno did with them together.
- New language: a new file per list with a `language` code; keep English files untouched.

Keep entries lower-case, without punctuation, one per line in the JSON arrays. Do not include
personal data in issues; credit is given by the name or handle on the issue or pull request.
