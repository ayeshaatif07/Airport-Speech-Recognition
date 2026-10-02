# Airport Speech Recognition

An offline, multi-language speech recognition system for an airport virtual assistant, built in a Jupyter notebook with [Vosk](https://alphacephei.com/vosk/). It recognises English, Spanish and Italian, cleans up noisy recordings before transcribing them, and measures accuracy with Word Error Rate (WER).

## Features

- **Offline recognition** in three languages (English, Spanish, Italian) using Vosk models.
- **Noise-aware preprocessing** before recognition:
  - mono conversion and DC offset removal
  - peak normalisation and RMS-based gain adjustment
  - low-pass filter (3200 Hz in aggressive mode, 3800 Hz otherwise)
  - noise gate that turns down quiet background sound
  - final normalisation and clipping, saved as a 16-bit WAV
- **WER evaluation** with `jiwer` for each test file and the average per language.
- **Microphone recording** of your own sentences with `sounddevice`, transcribed and scored the same way.

## Results

From the saved run in the notebook:

| Language | Average WER | Threshold | Result |
|----------|-------------|-----------|--------|
| English | 18.57% | < 25% | Pass |
| Spanish | 19.52% | < 35% | Pass |
| Italian | 15.72% | < 35% | Pass |

The test set has five airport phrases per language (check-in desk, lost parents, lost suitcase, plane time, restaurants and shops). Two custom English sentences were also recorded and scored.

## Project Structure

| File / folder | Purpose |
|---------------|---------|
| `ex4.1.ipynb` | The notebook: the `AirportASR` class, evaluation and the recording session |
| `Ex4_audio_files/EN`, `ES`, `IT` | Test recordings for each language, with their `_preprocessed` versions |
| `your_sentence1.wav`, `your_sentence2.wav` | Custom recordings, with their preprocessed versions |
| `models/` | Vosk models (**not included**, see below) |

## Download the Models

The Vosk models are about 2.7 GB, which is too large for GitHub, so they are not in this repository. Download these three from the [Vosk model list](https://alphacephei.com/vosk/models), unzip them and put the folders in a `models/` folder next to the notebook:

| Language | Model folder name |
|----------|-------------------|
| English | `vosk-model-en-us-0.22` |
| Spanish | `vosk-model-small-es-0.42` |
| Italian | `vosk-model-small-it-0.22` |

The folder should look like this:

```
models/
├── vosk-model-en-us-0.22/
├── vosk-model-small-es-0.42/
└── vosk-model-small-it-0.22/
```

## Run Locally

You need Python 3 and Jupyter. A microphone is only needed for the custom recording part.

```bash
git clone https://github.com/ayeshaatif07/Airport-Speech-Recognition.git
cd Airport-Speech-Recognition
pip install vosk soundfile jiwer numpy sounddevice jupyter
jupyter notebook ex4.1.ipynb
```

Then:

1. Add the `models/` folder as described above.
2. Run the cells from top to bottom. Start Jupyter from the project folder, because the notebook uses the relative paths `models/` and `Ex4_audio_files/`.
3. The last cell evaluates all three languages and then asks you to record two sentences. Press ENTER when prompted and speak for 5 seconds each time.

## Author and Credits

- **Author:** Ayesha Atif
- **Coursework:** Intelligent Signal Processing (CM3065) – Midterm (Exercise 4)
- Speech recognition by [Vosk](https://alphacephei.com/vosk/); WER computed with [jiwer](https://github.com/jitsi/jiwer).
