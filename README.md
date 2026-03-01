# Interview Practice

A lightweight, static interview practice tool designed to be hosted on GitHub Pages.

## How It Works

1. Click **Start Interview Practice** — questions are randomized each session.
2. An audio question plays automatically.
3. Click **Start Answering** — a timer begins alongside the expected answer time.
4. Answer out loud, then choose:
   - **Hear Response** — plays the suggested response audio
   - **Next Question** — moves to the next question
   - **Finish** — ends the session and shows your summary

The summary shows how many questions you answered, your total time versus expected time, and a per-question breakdown with color-coded pacing.

## Setup

### 1. Add your audio files

Create an `audio/` folder next to `index.html` and add your MP3 files:

```
interview-practice/
├── index.html
├── README.md
└── audio/
    ├── q01-question.mp3
    ├── q01-response.mp3
    ├── q02-question.mp3
    ├── q02-response.mp3
    ├── q03-question.mp3
    ├── q03-response.mp3
    └── ...
```

### 2. Configure questions

Open `index.html` and find the `QUESTIONS` array near the top of the `<script>` section. Edit it to match your audio files:

```javascript
const QUESTIONS = [
  {
    questionAudio: "audio/q01-question.mp3",   // path to question audio
    responseAudio: "audio/q01-response.mp3",   // path to response audio
    expectedTime: 120,                          // expected answer time in seconds
    label: "Tell me about yourself"             // short label for the summary
  },
  {
    questionAudio: "audio/q02-question.mp3",
    responseAudio: "audio/q01-response.mp3",   // can reuse the same response audio
    expectedTime: 90,
    label: "Why this role?"
  },
  // Add as many as you need...
];
```

**Note:** Multiple questions can point to the same `responseAudio` file — just use the same path.

### 3. Deploy to GitHub Pages

1. Create a new repository on GitHub (e.g., `interview-practice`).
2. Push all files (including the `audio/` folder) to the `main` branch.
3. Go to **Settings → Pages → Source** and select `main` branch, root (`/`).
4. Your site will be live at `https://yourusername.github.io/interview-practice/`.

### File size note

GitHub Pages repos have a soft limit of ~1 GB. If your audio files are large, consider compressing them to 128kbps mono MP3s — they'll still sound clear for spoken content and will be roughly 1 MB per minute.

## Timer Color Coding

| Color  | Meaning                        |
|--------|--------------------------------|
| Black  | Under 85% of expected time     |
| Amber  | Between 85%–100% of expected   |
| Red    | Over expected time             |

## Customization

- **Styling**: All CSS is in the `<style>` block — uses CSS variables for easy theming.
- **Order mode**: To switch to sequential order, replace `shuffled = shuffle(QUESTIONS)` with `shuffled = [...QUESTIONS]` in the `startPractice()` function.
