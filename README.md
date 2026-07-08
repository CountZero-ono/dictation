# Dictation

A local speech-to-text dictation system for the host PC (running Linux/Hyprland) and the Dixie Ball hardware.

## Architecture

This project provides two entry points for speech-to-text dictation into your active window:

1. **PC-level Dictation (F4 key)**:
   - Captures audio from your PC mic/webcam using `pw-record` (PipeWire).
   - Sends the audio to the local `wyoming-faster-whisper` server on port `10300`.
   - Injects the transcribed text as physical keystrokes into the active window using `wtype`.
   - Bound to the `F4` key in Hyprland.

2. **Dixie Ball Keyboard Emulation (Wyoming Server)**:
   - Run `dixie_dictate.py` which hosts a Wyoming server on port `10400`.
   - When the Dixie Ball voice terminal sends dictation audio to port `10400`, `dixie_dictate.py` proxies it to Whisper (port `10300`) and uses `wtype` to type it on the PC.

---

## Files

- [dictate.py](file:///home/fuad/OCProjects/dictation/dictate.py): The desktop keybind recording and transcription script.
- [services/dixie_dictate.py](file:///home/fuad/OCProjects/dictation/services/dixie_dictate.py): The Wyoming server to accept audio from the Dixie Ball voice terminal and type it out.

---

## Setup

### 1. Hyprland Keybind
Add the following line to your `~/.config/hypr/hyprland.conf`:
```ini
bind = , F4, exec, /home/fuad/OCProjects/dictation/dictate.py
```

### 2. Run the Dixie Ball Dictation Server (Optional)
To run the Wyoming proxy server:
```bash
python3 /home/fuad/OCProjects/dictation/services/dixie_dictate.py --port 10400 --whisper-port 10300
```
