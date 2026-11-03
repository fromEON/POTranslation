# POTranslation

A simple Python script for translating `.po` files with [`googletrans`](https://pypi.org/project/googletrans/).

The script reads a PO file, translates messages whose `msgstr` is empty, and saves the translated text to the corresponding `msgstr`. Messages that already have a translation are skipped.

## Requirements

- Docker
- Python 3.12
- Dependencies listed in [`requirements.txt`](requirements.txt)
- Docker (optional, if you prefer to use the included `Dockerfile`)

### Why Python 3.12?

This project uses `googletrans==4.0.0-rc1`, which is not compatible with Python 3.13 and later. The pinned release also relies on older HTTP dependencies.

## Getting started

Build the Docker Image:

```bash
docker build -t translation-tool .
```

```bash
docker run --rm -it \
  -v "$(pwd)/translation_input:/app/translation_input" \
  -v "$(pwd)/translation_output:/app/translation_output" \
  translation-tool
```



Place the `.po` file you want to translate in `translation_input/`. For example:

```text
translation_input/messages.po
```

An example PO file is available at [`examples/example_messages.po`](examples/example_messages.po). To use it:

```bash
cp examples/example_messages.po translation_input/
```

## Run a translation

When prompted, enter the PO filename (not the full path). The script looks for it in `translation_input/`:

```text
Enter the PO filename, for example example_messages.po: example_messages.po
```

Then enter the destination language code:

```text
Enter the destination language code, for example fr, de, hi, or es: fr
```

Some example language codes:

| Code | Language |
| --- | --- |
| `fr` | French |
| `de` | German |
| `hi` | Hindi |
| `es` | Spanish |
| `it` | Italian |
| `pt` | Portuguese |
| `nl` | Dutch |

The script validates the language code before translating.

## Output

Translated files are saved in `translation_output/`. The destination language code is appended to the output filename.

For example, translating `translation_input/example_messages.po` to French creates:

```text
translation_output/example_messages_fr.po
```

Translation errors are logged to `translation.log`.

## Project structure

```text
translation_tool/
├── Dockerfile
├── examples/
│   └── example_messages.po
├── translation_input/
│   └── .gitkeep
├── translation_output/
│   └── .gitkeep
├── .gitignore
├── README.md
├── requirements.txt
└── script.py
```

- `examples/` contains a reference PO file.
- `translation_input/` contains files to be translated.
- `translation_output/` contains generated translations.
- Files placed in `translation_input/` and generated in `translation_output/` are ignored by Git.

## Notes and troubleshooting

This project deliberately uses `googletrans==4.0.0-rc1`. `googletrans` is an unofficial library that communicates with Google Translate and does not require a Google Cloud Translation API key. It depends on undocumented Google Translate behavior, so it may stop working if Google changes the service.

If you see this error:

```text
ModuleNotFoundError: No module named 'cgi'
```

Check your Python version:

```bash
python --version
```

You are likely running Python 3.13 or later. Use Python 3.12 for this project.
