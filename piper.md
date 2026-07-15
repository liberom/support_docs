# Piper Text-to-Speech Engine

Piper is a fast, local neural text-to-speech system that converts written text into natural-sounding speech using ONNX voice models. Built on a VITS (Variational Inference with adversarial learning for end-to-end Text-to-Speech) architecture, Piper embeds espeak-ng for phonemization and runs entirely offline without cloud dependencies. The engine supports multiple languages, multi-speaker voices, and various quality levels, making it suitable for accessibility tools, voice assistants, and embedded systems.

The system operates by converting input text to phonemes using espeak-ng, mapping phonemes to numeric IDs, and feeding these through trained ONNX neural network models to generate 16-bit PCM audio at configurable sample rates (typically 22050 Hz). Piper provides three interfaces: a command-line tool for quick synthesis, an HTTP server for repeated use, and Python/C/C++ APIs for programmatic integration. Voice models are distributed separately from HuggingFace and can be downloaded on-demand, with each voice consisting of an `.onnx` model file and a `.onnx.json` configuration file containing phoneme mappings and inference parameters.

## Python API - Loading and Using Voices

```python
import wave
from piper import PiperVoice

# Load voice model (config auto-detected as model_path + ".json")
voice = PiperVoice.load("/path/to/en_US-lessac-medium.onnx")

# Synthesize text to WAV file
with wave.open("output.wav", "wb") as wav_file:
    voice.synthesize_wav("Welcome to the world of speech synthesis!", wav_file)
```

## Python API - Streaming Audio Output

```python
from piper import PiperVoice

voice = PiperVoice.load("/path/to/en_US-lessac-medium.onnx")

# Stream audio chunks (useful for real-time playback)
for chunk in voice.synthesize("This text will be synthesized in chunks."):
    # Each chunk contains:
    # - chunk.sample_rate: int (e.g., 22050)
    # - chunk.sample_width: int (2 for 16-bit)
    # - chunk.sample_channels: int (1 for mono)
    # - chunk.audio_int16_bytes: bytes (raw PCM data)
    # - chunk.phonemes: list[str]
    # - chunk.phoneme_ids: list[int]

    # Set up audio stream with format from first chunk
    audio_stream.write(chunk.audio_int16_bytes)
```

## Python API - Synthesis Configuration

```python
from piper import PiperVoice, SynthesisConfig

voice = PiperVoice.load("/path/to/en_US-lessac-medium.onnx")

# Customize synthesis parameters
syn_config = SynthesisConfig(
    speaker_id=0,           # Speaker index for multi-speaker models
    length_scale=2.0,       # 2.0 = half speed, 0.5 = double speed
    noise_scale=0.667,      # Audio variation (higher = more variability)
    noise_w_scale=0.8,      # Phoneme duration variation
    volume=0.5,             # Volume multiplier (0.5 = half volume)
    normalize_audio=True    # Scale to full dynamic range
)

with wave.open("custom.wav", "wb") as wav_file:
    voice.synthesize_wav("This will sound different.", wav_file, syn_config=syn_config)
```

## Python API - GPU Acceleration

```python
from piper import PiperVoice

# Enable CUDA for GPU inference (requires onnxruntime-gpu)
voice = PiperVoice.load("/path/to/en_US-lessac-medium.onnx", use_cuda=True)

# Synthesis works the same as CPU mode
with wave.open("gpu_output.wav", "wb") as wav_file:
    voice.synthesize_wav("GPU accelerated synthesis.", wav_file)
```

## Python API - Phoneme Extraction and Alignment

```python
import wave
from piper import PiperVoice

voice = PiperVoice.load("/path/to/en_US-lessac-medium.onnx")

# Get phoneme alignments with audio samples
with wave.open("aligned.wav", "wb") as wav_file:
    alignments = voice.synthesize_wav(
        "Phoneme alignment example.",
        wav_file,
        include_alignments=True
    )

# alignments is list of PhonemeAlignment objects:
# - phoneme: str (e.g., "h", "ə", "l", "oʊ")
# - phoneme_ids: Sequence[int]
# - num_samples: int (audio samples for this phoneme)

for align in alignments:
    duration_ms = (align.num_samples / voice.config.sample_rate) * 1000
    print(f"Phoneme '{align.phoneme}': {duration_ms:.1f}ms")
```

## Python API - Raw Phoneme Injection

```python
from piper import PiperVoice

voice = PiperVoice.load("/path/to/en_US-lessac-medium.onnx")

# Inject custom espeak-ng phonemes with [[ ... ]] blocks
# Get phonemes with: espeak-ng -v en-us --ipa=3 -q batman
text_with_phonemes = "I am the [[ bˈætmæn ]] not [[ bɹˈuːs wˈeɪn ]]"

with wave.open("phonemes.wav", "wb") as wav_file:
    voice.synthesize_wav(text_with_phonemes, wav_file)
```

## Python API - Phonemization Only

```python
from piper import PiperVoice

voice = PiperVoice.load("/path/to/en_US-lessac-medium.onnx")

# Convert text to phonemes (grouped by sentence)
phonemes = voice.phonemize("Hello world. This is a test.")
# Returns: [['h', 'ə', 'l', 'oʊ', ' ', 'w', 'ɜː', 'l', 'd'], ['ð', 'ɪ', 's', ...]]

# Convert phonemes to numeric IDs
phoneme_ids = voice.phonemes_to_ids(phonemes[0])
# Returns: [1, 42, 15, 8, ...]  (1=BOS, includes padding and EOS)
```

## Command-Line Interface - Downloading Voices

```bash
# List all available voices
python3 -m piper.download_voices

# Download a specific voice (format: <language>-<name>-<quality>)
python3 -m piper.download_voices en_US-lessac-medium

# Download to specific directory
python3 -m piper.download_voices en_US-lessac-medium --data-dir /path/to/voices/

# Download multiple voices
python3 -m piper.download_voices en_US-lessac-medium es_ES-carlfm-x_low
```

## Command-Line Interface - Basic Synthesis

```bash
# Synthesize text to WAV file
python3 -m piper -m en_US-lessac-medium -f output.wav -- 'This is a test.'

# Synthesize from stdin
echo "Hello world" | python3 -m piper -m en_US-lessac-medium -f output.wav

# Read from text file(s)
python3 -m piper -m en_US-lessac-medium -f output.wav --input-file text1.txt --input-file text2.txt

# Play audio immediately with ffplay (requires ffplay)
python3 -m piper -m en_US-lessac-medium -- 'This will play on your speakers.'

# Stream raw PCM to stdout
python3 -m piper -m en_US-lessac-medium --output-raw -- 'Raw audio' | aplay -r 22050 -f S16_LE
```

## Command-Line Interface - Voice Configuration

```bash
# Use voice from different directory
python3 -m piper -m en_US-lessac-medium --data-dir /path/to/voices/ -f out.wav -- 'Hello'

# Multi-speaker voice (select speaker by ID)
python3 -m piper -m en_US-libritts_r-medium -s 23 -f out.wav -- 'Speaker 23'

# Adjust synthesis parameters
python3 -m piper -m en_US-lessac-medium \
  --length-scale 0.5 \
  --noise-scale 0.667 \
  --noise-w-scale 0.8 \
  --volume 1.5 \
  --no-normalize \
  -f fast_loud.wav -- 'Fast and loud'

# Add silence between sentences
python3 -m piper -m en_US-lessac-medium \
  --sentence-silence 0.5 \
  -f paused.wav -- 'First sentence. Second sentence.'

# Enable GPU acceleration
python3 -m piper -m en_US-lessac-medium --cuda -f out.wav -- 'GPU synthesis'
```

## HTTP Server - Starting and Basic Usage

```bash
# Install HTTP dependencies
python3 -m pip install piper-tts[http]

# Start server on default port 5000
python3 -m piper.http_server -m en_US-lessac-medium

# Custom host and port
python3 -m piper.http_server -m en_US-lessac-medium --host 0.0.0.0 --port 8080

# Load voices from specific directory
python3 -m piper.http_server -m en_US-lessac-medium --data-dir /path/to/voices/
```

## HTTP Server - Synthesizing Speech

```bash
# Basic synthesis (returns WAV file)
curl -X POST \
  -H 'Content-Type: application/json' \
  -d '{"text": "This is a test."}' \
  -o output.wav \
  http://localhost:5000

# With synthesis parameters
curl -X POST \
  -H 'Content-Type: application/json' \
  -d '{
    "text": "Customized synthesis.",
    "length_scale": 0.5,
    "noise_scale": 0.667,
    "noise_w_scale": 0.8
  }' \
  -o custom.wav \
  http://localhost:5000

# Multi-speaker voice (by speaker name)
curl -X POST \
  -H 'Content-Type: application/json' \
  -d '{
    "text": "Hello from speaker.",
    "speaker": "speaker_name"
  }' \
  -o speaker.wav \
  http://localhost:5000

# Multi-speaker voice (by speaker ID)
curl -X POST \
  -H 'Content-Type: application/json' \
  -d '{
    "text": "Hello from speaker 5.",
    "speaker_id": 5
  }' \
  -o speaker5.wav \
  http://localhost:5000
```

## HTTP Server - Voice Management

```bash
# List available voices
curl http://localhost:5000/voices

# Response example:
# {
#   "en_US-lessac-medium": {
#     "sample_rate": 22050,
#     "num_speakers": 1,
#     "speakers": {}
#   },
#   "en_US-libritts_r-medium": {
#     "sample_rate": 22050,
#     "num_speakers": 904,
#     "speakers": {"speaker_1": 0, "speaker_2": 1, ...}
#   }
# }

# Specify different voice in request
curl -X POST \
  -H 'Content-Type: application/json' \
  -d '{
    "text": "Using alternate voice.",
    "voice": "en_GB-alan-medium"
  }' \
  -o british.wav \
  http://localhost:5000
```

## C/C++ API - Creating Synthesizer

```c
#include "piper.h"
#include <stdio.h>

int main() {
    // Create synthesizer from ONNX model
    // Config path is optional (defaults to model_path + ".json")
    piper_synthesizer *synth = piper_create(
        "/path/to/en_US-lessac-medium.onnx",
        NULL,  // Auto-detect config
        NULL   // Use default espeak-ng data path
    );

    if (!synth) {
        fprintf(stderr, "Failed to create synthesizer\n");
        return 1;
    }

    // Clean up when done
    piper_free(synth);
    return 0;
}
```

## C/C++ API - Synthesizing Speech

```c
#include "piper.h"
#include <stdio.h>
#include <string.h>

int main() {
    piper_synthesizer *synth = piper_create(
        "/path/to/en_US-lessac-medium.onnx", NULL, NULL
    );

    if (!synth) return 1;

    // Get default synthesis options from voice config
    piper_synthesize_options options = piper_default_synthesize_options(synth);

    // Customize options
    options.speaker_id = 0;
    options.length_scale = 1.0;    // Normal speed
    options.noise_scale = 0.667;   // Default audio variation
    options.noise_w_scale = 0.8;   // Default phoneme variation

    // Start synthesis
    const char *text = "Hello, world!";
    if (piper_synthesize_start(synth, text, &options) != PIPER_OK) {
        fprintf(stderr, "Failed to start synthesis\n");
        piper_free(synth);
        return 1;
    }

    // Get audio chunks
    piper_audio_chunk chunk;
    FILE *wav_file = fopen("output.raw", "wb");

    while (piper_synthesize_next(synth, &chunk) != PIPER_DONE) {
        // Write raw float samples
        fwrite(chunk.samples, sizeof(float), chunk.num_samples, wav_file);

        // chunk.sample_rate: int (e.g., 22050)
        // chunk.is_last: bool (true for final chunk)
        // chunk.phonemes: char32_t* (phoneme codepoints)
        // chunk.num_phonemes: size_t
        // chunk.phoneme_ids: int* (phoneme IDs)
        // chunk.num_phoneme_ids: size_t
        // chunk.alignments: int* (sample count per phoneme ID)
        // chunk.num_alignments: size_t

        if (chunk.is_last) break;
    }

    fclose(wav_file);
    piper_free(synth);
    return 0;
}
```

## C/C++ API - Phoneme Alignment Processing

```c
#include "piper.h"
#include <stdio.h>

void process_alignments(piper_audio_chunk *chunk) {
    // Phoneme alignment format:
    // phonemes: [p1, p1, 0, p2, p2, p2, 0, ...]
    // phoneme_ids: [1, 0, id1, 0, id2, id2, 0, ..., 2]
    // alignments: [count_for_id1, count_for_id2, ...]
    //
    // Where: 0 = pad, 1 = BOS, 2 = EOS

    size_t phoneme_idx = 0;
    size_t id_idx = 0;
    size_t align_idx = 0;

    while (phoneme_idx < chunk->num_phonemes) {
        // Read repeated phoneme codepoints until 0
        char32_t phoneme = chunk->phonemes[phoneme_idx];
        int repeat_count = 0;

        while (phoneme_idx < chunk->num_phonemes &&
               chunk->phonemes[phoneme_idx] != 0) {
            phoneme_idx++;
            repeat_count++;
        }
        phoneme_idx++; // Skip the 0 separator

        // Sum alignment counts for this phoneme's IDs
        int total_samples = 0;
        for (int i = 0; i < repeat_count && align_idx < chunk->num_alignments; i++) {
            total_samples += chunk->alignments[align_idx];
            align_idx++;
        }

        // Calculate duration
        float duration_ms = (total_samples / (float)chunk->sample_rate) * 1000.0f;
        printf("Phoneme U+%04X: %.1f ms\n", phoneme, duration_ms);
    }
}
```

## Voice Training - Dataset Preparation

```bash
# Install training dependencies
git clone https://github.com/OHF-voice/piper1-gpl.git
cd piper1-gpl
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install -e .[train]

# Build monotonic alignment extension
./build_monotonic_align.sh

# For development builds from repo
python3 setup.py build_ext --inplace
```

## Voice Training - Creating Training Dataset

```csv
audio001.wav|This is the first utterance.
audio002.wav|This is the second utterance.
audio003.wav|Text with punctuation, numbers, and symbols!
```

## Voice Training - Training a Voice Model

```bash
# Train new voice (recommended: use existing checkpoint for faster training)
python3 -m piper.train fit \
  --data.voice_name "my_custom_voice" \
  --data.csv_path /path/to/metadata.csv \
  --data.audio_dir /path/to/audio/ \
  --model.sample_rate 22050 \
  --data.espeak_voice "en-us" \
  --data.cache_dir /path/to/cache/ \
  --data.config_path /path/to/output/config.json \
  --data.batch_size 32 \
  --ckpt_path /path/to/en_US-lessac-medium.ckpt

# Training parameters:
# - voice_name: Any descriptive name
# - csv_path: Pipe-delimited CSV (audio_file|text)
# - audio_dir: Directory containing WAV files
# - sample_rate: Audio sample rate (usually 22050)
# - espeak_voice: Language code (see: espeak-ng --voices)
# - cache_dir: Stores phoneme cache and processed audio
# - config_path: Output path for voice config JSON
# - batch_size: Training batch size (adjust for VRAM)
# - ckpt_path: Pre-trained checkpoint for transfer learning

# Show all training options
python3 -m piper.train fit --help
```

## Voice Training - Exporting Trained Model

```bash
# Export Lightning checkpoint to ONNX format
python3 -m piper.train.export_onnx \
  --checkpoint /path/to/lightning_logs/version_0/checkpoints/epoch=100.ckpt \
  --output-file /path/to/output/model.onnx

# Rename for Piper compatibility
# Format: <language>-<name>-<quality>.onnx
mv model.onnx en_US-myvoice-medium.onnx
mv config.json en_US-myvoice-medium.onnx.json

# Test the exported voice
python3 -m piper -m en_US-myvoice-medium -f test.wav -- 'Testing custom voice.'
```

## Voice Configuration - Understanding Config Files

```json
{
  "audio": {
    "sample_rate": 22050
  },
  "espeak": {
    "voice": "en-us"
  },
  "inference": {
    "noise_scale": 0.667,
    "length_scale": 1.0,
    "noise_w": 0.8
  },
  "num_speakers": 1,
  "num_symbols": 256,
  "phoneme_type": "espeak",
  "phoneme_id_map": {
    "^": [1],
    "$": [2],
    " ": [3],
    "h": [42],
    "ə": [15],
    "_": [0]
  },
  "speaker_id_map": {},
  "hop_length": 256
}
```

Piper serves as a versatile text-to-speech solution suitable for accessibility applications, voice assistants, automated narration, and embedded systems requiring offline speech synthesis. The engine's architecture prioritizes local execution, low latency, and minimal resource consumption while maintaining natural-sounding output. Integration options range from simple command-line usage for scripting and prototyping to full programmatic control via Python and C/C++ APIs for production applications.

The training workflow enables creation of custom voices for new speakers, languages, or specialized domains by fine-tuning from existing checkpoints. This transfer learning approach significantly reduces training time and data requirements compared to training from scratch. Multi-speaker models can combine multiple voices into a single model file, with speaker selection at inference time. The system's modular design separates phonemization (espeak-ng), neural acoustic modeling (ONNX), and audio generation, allowing flexibility in deployment configurations and potential integration with alternative phonemizers or model architectures.
