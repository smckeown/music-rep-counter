A small, private, browser-based tool that counts how many times you play a phrase while practising, helping you to keep track when your mind starts wandering!

**Live app:** https://smckeown.github.io/music-rep-counter/

## Why

To get a passage properly learned, you need to play it through fluently multiple times. Repetition builds muscle memory. Maybe you want to play it three times, or twenty, or a hundred. The most difficult part of it is keeping track in your head while working through repetitions. This app listens through your device's microphone and keeps the count for you.

## Two ways to count

The app has two modes, switchable with the tabs at the top. Pick whichever suits how you're practising.

**By pauses** — The quick option. It listens for the short silence between repeats and ticks the counter each time one rep ends. No setup beyond a quick tune of the sensitivity. Best when you naturally take a breath between repetitions.

**By reference** — Record your phrase once as a clean reference take, and the app then recognises that phrase whenever it comes round again and counts it. This works even when you run repetitions straight into each other with no gap, because it's matching the music rather than listening for silence. It also shows how closely each rep matched, which is the groundwork for telling clean reps from flubbed ones.

## Using it

Open the app, prop your phone or laptop where it can hear you, and allow microphone access when asked.

**By pauses**
1. Tap **Start listening**.
2. Play your phrase, leaving a brief breath between each repeat.
3. If the count is off, open **Settings**:
   4. **Calibrate from room silence** sets the threshold to your room automatically (stay quiet for two seconds).
   5. **Sensitivity** — drag left if quiet playing isn't counted, right if room noise triggers it.
   6. **Gap between reps** — how long a pause closes a rep (default 0.5s). Keep it shorter than the breath you actually leave.
   7. **Ignore bursts under** — filters out coughs and stray notes.

**By reference**
1. Tap **Record reference**, play your phrase once cleanly, then **Stop**.
2. Listen back, and either **Use this reference** or **Record again** — as many takes as you need.
3. Tap **Start listening** and play. Watch the **match meter**: set **Match strictness** (in Settings) just below where your good reps peak and above the dips between them.

Either way, set your target with the **Goal** stepper, and **Reset count** is on the front page whenever you start a fresh run.

## Privacy

This app has been designed privacy-first. Everything stays in your browser:

- **Nothing leaves your device.** Audio is analysed locally in the browser and is never recorded to a server, uploaded, or transmitted anywhere.
- **No accounts, no tracking, no analytics, no ads.** The page makes no network calls at all — you can confirm that in your browser's developer tools.
- **The only thing stored** is your own settings (chosen tab, goal, and tuning), kept locally on your device so you don't have to set them each time. Reference recordings are held only for the current session.

## Running it yourself

It's a single static HTML file with no build step and no dependencies.

- **Use it online:** just open the live link above.
- **Host your own copy:** drop `index.html` into any static host (GitHub Pages, Netlify, etc.). On GitHub Pages: put the file in the repo, then **Settings → Pages → Deploy from a branch → main / (root)**.
- **A note on the microphone:** browsers only grant mic access over **https** (or `localhost`). Opening the file directly from disk won't work — host it, and you're set.

## How it works

Plain JavaScript and the Web Audio API, no libraries.

- An `AnalyserNode` provides the audio level (for the pause counter and the meters) and the frequency spectrum.
- For reference matching, each slice of sound is reduced to a 12-value **chroma** vector — energy per pitch class — which captures the harmonic content while ignoring timbre and volume.
- Recorded reference and live audio are compared with **Dynamic Time Warping**, which aligns them while tolerating small tempo differences, producing a match score that drives the counting.
- A wake lock keeps the screen awake while listening, so the phone can sit on a music stand.

## Browser support

Any reasonably current browser with microphone support (Chrome, Edge, Firefox, Safari). Served over https. The screen wake lock and a couple of niceties degrade quietly where unsupported.

## Roadmap / ideas

- **Clean vs. flubbed reps**, with a "clean in a row" streak — built on the reference match score, since wrong notes, missing notes, and over-long pauses all lower it.
- **Saved reference snippets**, so a phrase can be reloaded across sessions instead of re-recorded.

## Support

I am not providing support for this app. It comes as is. However, you can contribute by:

- making a suggestion or reporting a bug by opening an issue
- sending a pull request

If it saves you some counting and you'd like to buy me a coffee (add buy me a coffee link eventually if I launch this thing).

## FAQs

### I am using the by pauses tab and the rep counter is not counting. 
You may need to adjust the **ignore burst** setting, especially if you are playing a very short phrase. Adjust this down to 1 second or less, or turn it off altogether.  

## License

This app is licensed under GPLv3. Enjoy!
