# Dictation

A local, hotkey-driven speech-to-text dictation system for Linux (Hyprland).

## Architecture

This project provides a low-latency, hands-free dictation workflow to type spoken words directly into your active window:

- **Audio Capture**: Uses `pw-record` (PipeWire) to capture audio from your PC microphone/webcam.
- **Transcription**: Streams the audio to a local `wyoming-faster-whisper` server (defaulting to port `10300`) for near-instant transcription using a local Whisper model.
- **Text Injection**: Uses `wtype` to physically inject the transcribed text as keystrokes into the active window on your desktop.
- **Hotkey Integration**: Typically bound to the `F4` key natively in Hyprland.

---

## Files

- [dictate.py](dictate.py): The desktop keybind recording and transcription script.

---

## Setup

### 1. Hyprland Keybind
Add the following line to your `~/.config/hypr/hyprland.conf`:
```ini
bind = , F4, exec, /home/fuad/OCProjects/dictation/dictate.py
```

### 2. Dependencies
Ensure you have the following installed on your host:
* `wtype` (for typing text into Wayland windows)
* `pipewire` / `wireplumber` (for `pw-record`)
* `libnotify` (for `notify-send` visual notifications)
* A running `wyoming-faster-whisper` server on port `10300`.
