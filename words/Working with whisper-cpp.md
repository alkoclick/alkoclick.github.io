

```
# Install whisper.cpp
brew install whisper-cpp

# Fetch a GGML formatted model (using large here)
# Comparisons: https://github.com/ggerganov/whisper.cpp/blob/master/models/README.md
curl -L -o ggml-large-v2-q8_0.bin "https://huggingface.co/ggerganov/whisper.cpp/resolve/main/ggml-large-v2-q8_0.bin"

# Ensure your brew path is reloaded
source ~/.zshrc

# You may need to convert your file because the CLI only works with 16 kHz WAVs
ffmpeg -i input.mp3 -ar 16000 -ac 1 -c:a pcm_s16le output.wav

whisper-cli -t 8 -m ~/models/ggml-large-v2-q8_0.bin input.wav -otxt output.txt
```
