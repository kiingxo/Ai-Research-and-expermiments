# Speech & Audio APIs

## Common Voice

**Use Case**: Speech recognition training, accent diversity, multilingual ASR

**Key Features**:
- 100+ languages
- 2 million+ validated recordings
- Crowdsourced, open dataset
- Free to download

**Getting Started**:
```python
from datasets import load_dataset

# Load Common Voice
cv = load_dataset("mozilla-foundation/common_voice", "en", split="train", streaming=True)

for sample in cv.take(5):
    print(f"Audio: {sample['audio']}")  # Has audio data and sampling rate
    print(f"Transcript: {sample['sentence']}\n")

# Access audio file
import librosa
audio, sr = librosa.load(sample['path'])
```

**Languages**: 100+
**Cost**: Free
**Size**: ~500+ hours per language
**Documentation**: https://commonvoice.mozilla.org/

---

## LibriSpeech

**Use Case**: English ASR, clean high-quality speech data

**Key Features**:
- 1000+ hours of English speech
- Read from audiobooks (clean pronunciation)
- Pre-split train/test sets
- Transcriptions included

**Getting Started**:
```python
from datasets import load_dataset

librispeech = load_dataset("librispeech_asr")

# Different splits available
for split in ["train.clean.100", "test.clean"]:
    ds = load_dataset("librispeech_asr", split=split)
    print(f"{split}: {len(ds)} samples")
    
    sample = ds[0]
    print(f"Audio: {sample['audio']}")
    print(f"Transcript: {sample['text']}\n")
```

**Cost**: Free
**Size**: 1000+ hours
**Quality**: Very high (audiobooks)
**Documentation**: https://www.openslr.org/12

---

## AudioSet

**Use Case**: Audio event detection, environmental sound analysis, audio tagging

**Key Features**:
- 2 million+ audio clips
- 527 audio event categories
- Balanced and comprehensive
- YouTube-sourced

**Getting Started**:
```python
# AudioSet provides links to YouTube videos and timestamps
# Download requires YouTube-DL

import yt_dlp
import pandas as pd

# Load AudioSet metadata
audioset_meta = pd.read_csv("audioset_eval_segments.csv")

# Download a sample
ydl_opts = {'format': 'bestaudio/best'}
for idx, row in audioset_meta.head(5).iterrows():
    youtube_id = row['YTID']
    url = f'https://www.youtube.com/watch?v={youtube_id}'
    
    with yt_dlp.YoutubeDL(ydl_opts) as ydl:
        ydl.download([url])
```

**Cost**: Free (YouTube videos)
**Size**: Massive (2M+ clips)
**Documentation**: https://research.google.com/audioset/

---

## VoxCeleb

**Use Case**: Speaker recognition, speaker verification, speaker embeddings

**Key Features**:
- 1M+ sentences
- 7000+ celebrities
- Diverse and large-scale
- Speaker identities labeled

**Getting Started**:
```python
# VoxCeleb requires registration and manual download
# After downloading:

from datasets import load_dataset

# Community hosted version
voxceleb1 = load_dataset("voxceleb", "voxceleb1_full", split="train")

sample = voxceleb1[0]
print(f"Speaker: {sample['speaker_id']}")
print(f"Audio: {sample['audio']}")
```

**Cost**: Free (with registration)
**Size**: 1M+ utterances
**Uses**: Speaker verification, speaker recognition
**Documentation**: https://www.robots.ox.ac.uk/~vgg/data/voxceleb/

---

## TIMIT

**Use Case**: Phoneme recognition, acoustic modeling, speech analysis

**Key Features**:
- Phoneme-level annotations
- Clean recording environment
- English utterances
- Established benchmark

**Getting Started**:
```python
from datasets import load_dataset
import librosa

# Load TIMIT dataset (requires timit package)
timit = load_dataset("timit_asr", split="train")

sample = timit[0]
print(f"Audio: {sample['audio']}")
print(f"Phonemes: {sample['phonetic_detail']}")
print(f"Words: {sample['word_detail']}\n")

# Spectogram visualization
import matplotlib.pyplot as plt
audio_data = sample['audio']['array']
sr = sample['audio']['sampling_rate']

D = librosa.feature.melspectrogram(y=audio_data, sr=sr)
plt.imshow(librosa.power_to_db(D, ref=np.max))
plt.show()
```

**Cost**: Free
**Size**: ~3.7 hours
**Languages**: English
**Documentation**: https://huggingface.co/datasets/timit_asr

---

## Multilingual LibriSpeech (MLS)

**Use Case**: Multilingual ASR, cross-lingual speech processing

**Key Features**:
- 8 languages
- 44,000+ hours
- Transcriptions included
- Large-scale multilingual

**Getting Started**:
```python
from datasets import load_dataset

# Available languages: Dutch, French, German, Italian, Portuguese, Spanish, Polish
mls = load_dataset("facebook/multilingual_librispeech", "portuguese", split="train")

sample = mls[0]
print(f"Audio: {sample['audio']}")
print(f"Transcript: {sample['transcript']}\n")
```

**Languages**: 8 major languages
**Cost**: Free
**Size**: 44,000+ hours
**Documentation**: https://huggingface.co/datasets/facebook/multilingual_librispeech

---

## SLT Arctic

**Use Case**: Text-to-speech synthesis, voice conversion

**Key Features**:
- Clean phonetically rich sentences
- Single speaker
- Parallel text-audio
- High quality recordings

**Cost**: Free
**Size**: ~1 hour
**Uses**: TTS, voice cloning
**Website**: https://www.cstr.ed.ac.uk/projects/arctic/

---

## ESC-50

**Use Case**: Environmental sound classification

**Key Features**:
- 2000 labeled audio clips
- 50 environmental sound classes
- 5 seconds each
- Well-balanced

**Getting Started**:
```python
from datasets import load_dataset

esc50 = load_dataset("ashraq/esc50")

sample = esc50["train"][0]
print(f"Audio: {sample['audio']}")
print(f"Target: {sample['target']}")  # Class label
```

**Cost**: Free
**Size**: 2000 clips
**Uses**: Environmental sound classification
**Documentation**: https://github.com/karolpiczak/ESC-50

---

## Comparison Table

| Dataset | Language | Size | Use Case | Cost |
|---------|----------|------|----------|------|
| Common Voice | 100+ | 500+ hours/lang | Multilingual ASR | Free |
| LibriSpeech | English | 1000 hours | English ASR | Free |
| AudioSet | Multilingual | 2M+ clips | Audio events | Free |
| VoxCeleb | Multilingual | 1M+ utts | Speaker recognition | Free |
| TIMIT | English | 3.7 hours | Phoneme recognition | Free |
| MLS | 8 languages | 44k hours | Multilingual ASR | Free |
| ESC-50 | Any | 2000 clips | Sound classification | Free |

---

## Quick Start by Task

- **Automatic Speech Recognition (ASR)**: LibriSpeech, Common Voice, MLS
- **Speaker Recognition**: VoxCeleb
- **Phoneme Recognition**: TIMIT
- **Sound Classification**: ESC-50, AudioSet
- **Text-to-Speech**: SLT Arctic
- **Voice Conversion**: Arctic datasets
