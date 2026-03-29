```bash
claude \
  --dangerously-skip-permissions \
  --output-format=stream-json \
  --verbose \
  -p "Please implement a voice input method: hold the Fn key to record audio, release to inject the transcribed text into the input field. Streaming transcription is preferred."
```
