# Zotero references script (and app)
This project aims to create a flexible, minimalistic CL-interface that enables retrieving reference collections from Zotero
and pasting them into a docx file. It is also my final project for [CS50](https://cs50.harvard.edu/x/2021/), an incredible and free course on computer science I can highly recommend.
Find a short demo video [here](https://youtu.be/3eVLcyNsKpE), at YouTube.
At this stage, the tool is far from complete, but it already does what it's supposed to do. Find the project on github at [rrodorr/zot_ref_export](https://github.com/rrodorr/zot_ref_export).

## What is a 'reference collection'?
A reference collection is a collection of project references (in my case: contract work we did at the company where I work) stored as Zotero items of the type 'document'. The idea is
to enable building reference lists with descriptions and other important project informations automatically, e.g. for
project applications. It's a very specific use case, but it can be adapted to fit your individual needs. The config file
(see below) yields some options and could be expanded. It's supposed to be distributed to (non-technical) colleagues for
easy everyday usage.

## File requirements
zot_ref_export requires two JSON files, `config.json` and `locale.json`. The former holds information on multiple things,
e.g. the library ID and the key required to access it (see the pyzotero [getting started page](https://pyzotero.readthedocs.io/en/latest/) to find out where to find both), as well as fields that contain the items to retrieve and their output positions etc. If the file is not found, an *incomplete* template will be created.
Locale holds the messages that are displayed, as well as language-specific field descriptions. Currently, there is no
mechanism to build it if it is missing, though this could be easily implemented.

## Building with PyInstaller
There is a spec that specifies the JSON files as datas. It is not otherwise modified.
Run `pyinstaller --clean --noconfirm zot_ref_export.spec` to build. If the file is missing, run PyInstaller on the script
and specify the files as options `pyinstaller --add-data="config.json;." --add-data="locale.json;." zot_ref_export.py`

## Design considerations
Because of `pyzotero`'s web API calls, the current implementation means that an internet connection is required. It also means that any change to the Zotero library needs to be synced to Zotero's servers before the script can process it.  
This is mainly due to the fact that Zotero's local API is poorly documented. This however doesn't mean that a local mode couldn't be implemented. Ideally, the tool would offer both routes.

Overall, there is plenty of room for improvements. The code should be refactored to make it more legible. Finding a way to offer users more flexibility with how the output is formatted without making matters too complicated or re-implementing `python-docx` is a priority.