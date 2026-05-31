---
name: dococr-skill
description: Use when working with docOCR, a macOS local OCR-to-Markdown tool, including README-grounded usage help, CLI OCR to stdout, batch Markdown file output, local HTTP server usage, JSON OCR API examples, OCR execution, and troubleshooting.
---

# docOCR

## Core Context

docOCR is a macOS command-line OCR tool that converts document images into Markdown text. It can run as:

- A CLI tool that prints OCR Markdown to stdout when called with image paths.
- A batch CLI tool that writes `.md` files next to input images when called with `-o`.
- A local Vapor HTTP server with a browser upload page.
- A JSON upload API for local clients.

The docOCR project repository is https://github.com/riddleling/docOCR. When `docOCR` is not installed locally, direct the user there for installation instructions.

Keep the product scope concrete: local macOS OCR to Markdown, using Apple's `RecognizeDocumentsRequest`, with no external OCR service required for recognition. Always mention the macOS 26+ requirement when setup, compatibility, or usage questions could otherwise imply broader support.

## Workflow

1. Identify whether the user needs usage help, API integration, OCR execution, or troubleshooting.
2. For usage/API answers, ground the response in the commands below and adapt paths/ports to the user's context.
3. For actual OCR execution, prefer the installed `docOCR` command. If it is unavailable, tell the user to install docOCR from the project repository.

## CLI Usage

Use these commands as the baseline:

```bash
docOCR -h
docOCR --help
docOCR -V
docOCR --version
docOCR ~/Desktop/book_imgs/*.jpg
docOCR -o ~/Desktop/book_imgs/*.jpg
docOCR -s
docOCR -s -p 8000
```

Calling `docOCR` with only image paths prints OCR Markdown to stdout. Use this mode when the user asks to see or capture the OCR result directly.

The `-o` option writes Markdown next to each source image with the same basename and a `.md` extension, overwriting existing matching `.md` files. Use `-o` when the user asks to generate files.

The `-s` server mode and `-o` file-output mode are mutually exclusive.

If `docOCR` is not found on `PATH`, direct the user to the docOCR project repository for installation instructions.

## HTTP Server And API

Default server command:

```bash
docOCR -s
```

Default browser URL:

```text
http://0.0.0.0:8080
```

Browser uploads use:

```text
POST /upload
```

JSON API clients use:

```text
POST /api/ocr
```

Example:

```bash
curl -X POST http://127.0.0.1:8000/api/ocr \
  -F "file=@01.png"
```

The multipart field can be `file` or `image`.

Successful API shape:

```json
{
  "success": true,
  "message": "OK",
  "text": "OCR text..."
}
```

Error API shape:

```json
{
  "success": false,
  "message": "Error message",
  "text": ""
}
```

When helping a user debug API calls, check: server port, route path, multipart field name, source file path, and whether the server is actually running.
