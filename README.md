# Transcribe — Claude Code skill

Trascrive qualsiasi video da link (Instagram reel, TikTok, YouTube, YT Shorts, Twitter/X, Vimeo, ecc.) usando OpenAI Whisper in locale, gratis. Niente API key, niente upload, gira tutto sul tuo Mac.

## Come funziona

1. Mandi un link a Claude Code dicendo "trascrivi questo" o "transcribe this".
2. Claude scarica solo l'audio col tool `yt-dlp`.
3. Lo passa a `whisper` (locale) per la trascrizione.
4. Ti stampa il testo direttamente in chat.

## Installazione (5 minuti)

### 1. Installa le dipendenze (una volta sola)

Ti serve [Homebrew](https://brew.sh). Se non ce l'hai, installa prima quello.

```bash
brew install yt-dlp ffmpeg openai-whisper
```

### 2. Installa la skill

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/criscatalyst/transcribe-skill.git ~/.claude/skills/transcribe
chmod +x ~/.claude/skills/transcribe/transcribe.sh
```

### 3. Verifica

In una nuova sessione di Claude Code, scrivi:

> trascrivi questo: https://www.instagram.com/reel/...

Claude riconoscerà la skill `transcribe` e partirà. Alla prima esecuzione scarica i pesi del modello Whisper (~500MB per il default `small`), poi va in cache.

## Opzioni

- **Modello**: default `small` (veloce, buono per reel). Per audio sporco o accenti forti usa `medium`. Per video lunghi e qualità top, `large-v3` (lento).
- **Lingua**: auto-detect. Su clip corti capita che sbagli — basta dire "trascrivi in italiano" o "in english".

## Costi

Zero. Tutto locale. Nessuna API.

## Problemi comuni

- **Reel privato** → yt-dlp fallisce. Devi essere loggato; passa i cookies del browser (Claude te lo proporrà).
- **Lingua sbagliata** → digli quale lingua è e rilancia.
- **Video silenzioso / solo musica** → trascrizione vuota. Normale.

## Stack

- `yt-dlp` — download audio da praticamente qualsiasi sito video
- `ffmpeg` — conversione audio
- `openai-whisper` — modello speech-to-text di OpenAI, eseguito in locale

— Cris
