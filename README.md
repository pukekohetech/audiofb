# Audio Feedback Recorder

A lightweight single-file HTML app for recording spoken feedback in short clips, trimming the start and end of each clip, reordering clips, exporting the final combined audio, and fetching a transcript with AssemblyAI.

## What it does

This tool is designed for quick voice feedback workflows.

You hold the **spacebar** to record, release it to pause, and press it again to create the next clip. Each recording burst becomes its own segment, which means you can:

* listen back to each clip individually
* trim the **start** and **end** of each clip
* reorder clips into the final sequence
* delete clips you do not want
* build and preview the final combined recording
* download the final audio file
* send the final audio to **AssemblyAI** and display the returned transcript

## Why this exists

This project was built to make spoken feedback faster and easier to manage.

Instead of recording one long take and having to start over when you make a mistake, this app lets you build the final message piece by piece. You can tidy each clip, rearrange the order, and only then export or transcribe the finished result.

## Main features

* **Press-and-hold recording** using the spacebar
* **Pause on release** and continue with a new clip on the next press
* **Clip-based editing** rather than one long recording
* **Trim handles** for adjusting the start and end of each clip
* **Reordering controls** for changing the final clip order
* **Delete controls** for removing unwanted clips
* **Final combined preview** before download
* **Final audio download** as a `.webm` file
* **AssemblyAI transcript fetch** using the final combined audio
* **Saved API settings** in the browser using local storage

## How it works

### Recording

The browser asks for microphone access. Once enabled:

* pressing the **spacebar** starts recording
* releasing the **spacebar** stops that clip
* pressing again creates a new clip

Each clip is stored separately so it can be edited before export.

### Trimming

Every clip has:

* a **blue handle** for the start point
* a **green handle** for the end point

Dragging these handles changes which portion of the clip is kept in the final export.

### Final audio build

When you click **Build Full Recording**, the app:

1. decodes each kept clip in the browser
2. trims them to the selected ranges
3. combines them in the visible order
4. creates one final audio file
5. loads that file into the preview player

### Transcript flow

When you click **Fetch Transcript**, the app:

1. builds the final combined audio
2. uploads that audio to AssemblyAI
3. creates a transcript job using the returned `upload_url`
4. polls AssemblyAI until the transcript is complete
5. displays the transcript text in the transcript box

## AssemblyAI setup

To use transcript fetching, you need an AssemblyAI API key.

In the app:

1. paste your API key into the **AssemblyAI API key** field
2. leave **Language detection** on unless you have a reason to disable it
3. leave the default **Speech models** unless you want to experiment
4. click **Fetch Transcript** after building or recording your audio

The page stores your AssemblyAI settings in **local storage** so you do not need to re-enter them every time on the same browser.

## Files

This project is intentionally simple.

* `audio_feedback_recorder.html` — the full application in one file
* `README.md` — this documentation

There are no build tools, no framework dependencies, and no install step for the app itself.

## How to use

1. Open the HTML file in a modern browser
2. Click **Enable Microphone**
3. Hold **Space** to record your first clip
4. Release **Space** to stop
5. Repeat for additional clips
6. Trim clip boundaries with the drag handles
7. Move clips up or down to set the final order
8. Click **Build Full Recording** to preview the combined result
9. Click **Download Final Audio** to save the audio file
10. Click **Fetch Transcript** to send the final audio to AssemblyAI

## Browser notes

This app works best in modern Chromium-based browsers such as:

* Google Chrome
* Microsoft Edge

Because it relies on browser audio APIs, support can vary across browsers.

## Known limitations

* Audio export is currently downloaded as **WebM** rather than MP3
* Trimming supports **start and end only**, not cuts from the middle of a clip
* Transcript fetching depends on:

  * a valid AssemblyAI API key
  * network access
  * browser permission to make the request
* Storing the API key in browser local storage is convenient, but not ideal on a shared machine
* Direct browser-side API usage exposes the API key to the client environment

## Privacy and security note

The current version sends the final audio **directly from the browser** to AssemblyAI.

That is fine for personal use and prototyping, but for production use it is better to place a small backend in front of AssemblyAI so your API key is not exposed in client-side code.

## Technical notes

This project uses browser-native features only:

* `MediaRecorder` for capturing microphone audio
* `getUserMedia` for microphone access
* `AudioContext` / `OfflineAudioContext` for trimming and merging clips
* `fetch` for AssemblyAI API requests
* `localStorage` for saving settings in the browser

## Future improvements

Possible next steps for this project:

* MP3 export
* waveform display for more precise trimming
* keyboard shortcuts for reordering clips
* transcript download button
* backend proxy for safer API key handling
* speaker labels or timestamps in transcript output
* better mobile/touch optimisation

## Example use cases

* spoken feedback for student work
* teacher voice notes
* internal review comments
* quick content review recordings
* reflective notes and verbal drafts

## Contributing

This project is currently designed as a simple single-file tool, but improvements are welcome.

Good contribution areas include:

* browser compatibility improvements
* transcript workflow improvements
* UI simplification
* export format support
* accessibility improvements

