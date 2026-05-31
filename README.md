# dococr-skill

`dococr-skill` is a Codex skill for working with [docOCR](https://github.com/riddleling/docOCR).

The docOCR project repository is [riddleling/docOCR](https://github.com/riddleling/docOCR). docOCR is a local macOS OCR-to-Markdown tool. It can convert images in batch from the CLI, run a local HTTP server, and expose a JSON OCR API at `/api/ocr`.

## Purpose

This skill gives Codex reusable context and workflows for docOCR-related tasks, including:

- Explaining docOCR CLI, server, and API usage.
- Running docOCR on images and producing Markdown output.
- Debugging local API, multipart upload, port, or server startup issues.

## Installation

Clone this repository to any local directory:

```bash
git clone https://github.com/riddleling/dococr-skill.git
```

Then link the skill into Codex's skills directory:

```bash
mkdir -p ~/.codex/skills
ln -s /path/to/dococr-skill ~/.codex/skills/dococr-skill
```

After installation, start a new Codex thread or restart Codex so it reloads available skills.

## Usage

Explicitly invoke the skill in Codex with `$dococr-skill`:

```text
Use $dococr-skill to explain how docOCR's /api/ocr endpoint works.
```

```text
Use $dococr-skill to OCR /path/to/Desktop/01.png and output Markdown.
```

```text
Use $dococr-skill to OCR /path/to/Desktop/01.png through the local API at http://127.0.0.1:8080/api/ocr and return the Markdown text.
```

```text
Use $dococr-skill to troubleshoot a failed docOCR upload to http://127.0.0.1:8080/api/ocr.
```

To run OCR for real, docOCR must be installed locally. See [riddleling/docOCR](https://github.com/riddleling/docOCR) for docOCR installation and usage details.

## Directory Structure

```text
dococr-skill/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── README.md
└── .gitignore
```

`SKILL.md` contains the main skill instructions. `agents/openai.yaml` contains Codex UI metadata.
