wser-based tool that counts how many times you play a phrase while practising, helping you to keep track when your mind starts wandering!

**Live app:** [https://smckeown.github.io/music-rep-counter/](https://smckeown.github.io/music-rep-counter/)

## Why

To get a passage properly learned, you need to play it through fluently multiple times. Repetition builds muscle memory. Maybe you want to play it three times, or twenty, or a hundred. The most difficult part of it is keeping track in your head while working through repetitions. This app listens through your device's microphone and keeps the count for you.

## How it counts

It listens for the short silence between repeats and ticks the counter each time one rep ends. The only thing it needs from you is a brief breath between repetitions — if you run them straight into each other with no gap, it can't tell where one ends and the next begins. A quick tune of the sensitivity and you're going.

## Using it

Open the app, prop your phone or laptop where it can hear you, and allow microphone access when asked.

1. Tap **Start listening**.
2. Play your phrase, leaving a brief breath between each repeat.
3. Set your target with the **Goal** field — type a number, or hold +/– to run it up.

If the count is off, open **Settings**:

- **Calibrate from room silence** sets the threshold to your room automatically (stay quiet for two seconds).
- **Sensitivity** — drag left if quiet playing isn't counted, right if room noise triggers it.
- **Gap between reps** — how long a pause closes a rep (default 0.5s). Keep it shorter than the breath you actually leave.
- **Minimum phrase length** — anything shorter than this won't count, which filters out coughs and stray notes.

**Reset count** is on the front page whenever you start a fresh run.

## Privacy

This app has been designed privacy-first. Everything stays in your browser:

- **Nothing leaves your device.** Audio is analysed locally in the browser and is never recorded to a server, uploaded, or transmitted anywhere.
- **No accounts, no tracking, no analytics, no ads.** The page makes no network calls at all — you can confirm that in your browser's developer tools.
- **The only thing stored** is your own settings (goal and tuning), kept locally on your device so you don't have to set them each time.

## Running it yourself

It's a single static HTML file with no build step and no dependencies.

- **Use it online:** just open the live link above.
- **Host your own copy:** drop `index.html` into any static host (GitHub Pages, Netlify, etc.). On GitHub Pages: put the file in the repo, then **Settings → Pages → Deploy from a branch → main / (root)**.
- **A note on the microphone:** browsers only grant mic access over **https** (or `localhost`). Opening the file directly from disk won't work — host it, and you're set.
- **Version:** the number shown at the bottom of the app tells you which build you're running — handy for checking a deploy has gone live (hard-refresh if it still shows the old one).

## How it works

Plain JavaScript and the Web Audio API, no libraries.

- An `AnalyserNode` measures the input loudness.
- When the level rises above a threshold a repetition begins; when it falls quiet for longer than the gap setting, the repetition is counted — as long as it lasted at least the minimum phrase length.
- A wake lock keeps the screen awake while listening, so the phone can sit on a music stand.

## Browser support

Any reasonably current browser with microphone support (Chrome, Edge, Firefox, Safari). Served over https. The screen wake lock and a couple of niceties degrade quietly where unsupported.

## Roadmap / ideas

- **Clean vs. flubbed reps**, with a "clean in a row" streak — telling a good repetition from a sloppy one. This is a meaningfully harder problem than counting, since it means grading a performance against a reference recording (your own, or a teacher's), so it's being scoped as a separate effort rather than bolted on.
- **Saved reference snippets**, if and when reference-based features land.

## Support

I am not providing support for this app. It comes as is. However, you can contribute by:

- making a suggestion or reporting a bug by opening an issue
- sending a pull request

If it saves you some counting and you'd like to buy me a coffee (add buy me a coffee link eventually if I launch this thing).

## FAQs

### I am using the rep counter and it is not counting.

You may need to adjust the **Minimum phrase length** setting, especially if you're playing a very short phrase — try lowering it to 1 second or less. It's also worth checking **Sensitivity**, or running **Calibrate from room silence**, so your playing reads as "playing" and your pauses read as silence.

## License

This app is licensed under GPLv3 — see the [LICENSE](LICENSE) file for the full text. Enjoy!
