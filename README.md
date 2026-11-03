A simple Python script for translating .po files.

The script loads a PO file, iterates over each untranslated msgid using the googletrans library, and saves the translated text to the message's msgstr.


Requirements
Docker
Python 3.12
Dependencies listed in requirements.txt

Why Python 3.12?
This project uses googletrans==4.0.0-rc1 which 3.13 doesn't support


Get Started
Clone or download the repository and install the dependencies:

pip install -r requirements.txt
Place the .po file that you want to translate inside:

translation_input/
For example:

translation_input/messages.po
An example PO file is included in:

examples/example_messages.po
You can copy this into the input directory if you want to try the script:

cp examples/example_messages.po translation_input/
Run the Translation
Run:

python script.py
The script will ask for the PO filename:

Enter the PO filename, for example example_messages.po: example_messages.po
Enter the filename only. The script automatically looks inside translation_input/.

Next, enter the destination language code:

Enter the destination language code, for example fr, de, hi, or es: fr
For example:

fr — French
de — German
hi - Hindi
es — Spanish
it — Italian
pt — Portuguese
nl — Dutch
The script validates the language code before attempting the translation.

Output
Translated files are automatically saved inside:

translation_output/
The destination language code is appended to the filename.

For example:

translation_input/example_messages.po
translated to French becomes:

translation_output/example_messages_fr.po
Messages that already contain a translation are skipped.

Translation errors are logged to:

translation.log
Project Structure
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
├── script.py

examples/ contains a reference PO file.
translation_input/ contains files to be translated.
translation_output/ contains generated translations.

Files placed in translation_input/ and generated in translation_output/ are ignored by Git.


Keep in mind
This project deliberately uses:

googletrans==4.0.0-rc1
googletrans is an unofficial Python library that communicates with Google Translate and does not require a Google Cloud Translation API key.

Because it relies on undocumented Google Translate behaviour, it may stop working if Google changes the service.

The pinned 4.0.0-rc1 release relies on older HTTP dependencies and is the reason this project currently requires Python 3.12 rather than Python 3.13 or later.

If you encounter:

ModuleNotFoundError: No module named 'cgi'
check your Python version:

python --version
You are likely running Python 3.13 or later. Use Python 3.12 to run this project.
