# Add to the <head> of audio_feedback_recorder.html

```html
<link rel="manifest" href="./manifest.webmanifest" />
<meta name="theme-color" content="#1a73e8" />
<link rel="icon" href="./icons/icon-192.png" />
<link rel="apple-touch-icon" href="./icons/icon-192.png" />
<meta name="apple-mobile-web-app-capable" content="yes" />
<meta name="apple-mobile-web-app-status-bar-style" content="default" />
<meta name="apple-mobile-web-app-title" content="Feedback Recorder" />
```

# Add before </body>

```html
<script>
  if ("serviceWorker" in navigator) {
    window.addEventListener("load", async () => {
      try {
        await navigator.serviceWorker.register("./sw.js");
        console.log("Service worker registered");
      } catch (error) {
        console.error("Service worker registration failed", error);
      }
    });
  }
</script>
```
