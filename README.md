# PFC Localization Dictionaries

Translation dictionaries for the open source [PowerBuilder Foundation Class (PFC) libraries](https://github.com/OpenSourcePFCLibraries). Each file maps the English text the PFC shows users (button captions, window titles, MicroHelp, toolbar text, messages built in scripts and so on) to its translation in one language.

The files are meant for the **PowerBuilder Translation Toolkit**, the tool that ships with PowerBuilder in its `TransTlk` folder. The toolkit uses a dictionary to translate a copy of the PFC libraries into another language without changing the original source.

## Files

| File | Language | Toolkit language ID | Entries |
|---|---|---|---|
| `danish.dic` | Danish | 7 | 926 |
| `dutch.dic` | Dutch | 8 | 964 |
| `french.dic` | French | 12 | 924 |
| `german.dic` | German | 15 | 908 |
| `italian.dic` | Italian | 24 | 928 |
| `norway.dic` | Norwegian | 31 | 903 |
| `spanish.dic` | Spanish | 40 | 908 |
| `swedish.dic` | Swedish | 42 | 933 |

In every dictionary, some entries (between 30 and 94) have a translation identical to the English text. Some are words that are the same in both languages, such as `OK`. Others may simply not have been translated yet.

## Where they came from

These files are copies of the `Dict` folder in the PowerBuilder 2025 Translation Toolkit:

```
C:\Program Files (x86)\Appeon\PowerBuilder 25.0\TransTlk\Dict\
```

The files there are dated April 22, 2024. They're kept in this repository so they don't get lost if PowerBuilder is uninstalled or reinstalled.

## File format

Each file is plain text with one entry per line and tab-separated fields:

| Field | Contents | Example (`german.dic`) |
|---|---|---|
| 1 | (empty) | |
| 2 | Toolkit language ID (see the table above) | `15` |
| 3 | Translated text | `Abbrechen` |
| 4 | Access key of the translated text (the letter after `&` in a caption), or empty | `A` |
| 5 | English source text | `Cancel` |
| 6 | Access key of the English text, or empty | `C` |
| 7 | Toolkit code for the kind of text | `4` |
| 8 | Where the text appears, e.g. `Text`, `Microhelp`, `ToolBarItemText`, `Title`, `Item[]`, `Variable`, `Event Script`, `Function Script` | `Text` |
| 9 | Comment | `Created from PTT Dictionary File` |

Values that contain tabs or line breaks, such as DataWindow expressions, are wrapped in double quotes and may span several lines.

### Encoding

The files use the Windows ANSI code page (Windows-1252/ISO-8859-1) with Windows (CRLF) line endings, which is what the Translation Toolkit reads and writes. Accented characters such as `é` and `ß` are single bytes. **Don't re-save the files as UTF-8**, or those characters may come out garbled in the toolkit. GitHub may also show some accented characters incorrectly for the same reason.

## PFC language files (PFC 2025 and later)

PFC 2025 has a language service (`n_cst_language`) that translates PFC at run time from a language file, the same way PowerBuilder 2025 R2 translates its runtime messages with `lang\default.lng`. One copy of PFC serves every language, and the translations survive PFC fixes. The `lang` folder here has a first language file for each dictionary:

| Folder | Language |
|---|---|
| `lang/danish` | Danish |
| `lang/dutch` | Dutch |
| `lang/french` | French |
| `lang/german` | German |
| `lang/italian` | Italian |
| `lang/norwegian` | Norwegian |
| `lang/spanish` | Spanish |
| `lang/swedish` | Swedish |

To use one, copy its `pfc.lng` to the `lang` folder of your application (next to the executable), and turn the service on with `gnv_app.of_SetLanguage(TRUE)` before opening windows.

The files were made from the dictionaries by `tools\New-PfcTranslation.ps1` in the [2025-Solution](https://github.com/OpenSourcePFCLibraries/2025-Solution) repository, from the English `lang\pfc.lng` there:

- About 87% of the entries are translated. The rest are at the end of each file, still in English, under "Not translated yet".
- Messages the dictionary only had in pieces are marked "Check the word order".
- The dictionaries have some mistakes, which carry over: for example, `german.dic` translates "Buffers" as "Rechner".
- Texts the dictionaries don't have, such as the messages of the OpenID Connect logon window, are translated by hand in each folder's `additions.lng`. The script takes them from there before it looks in the dictionary, so they're kept each time the files are made again. They haven't been reviewed by native speakers yet.

The files are made again whenever PFC gets new texts. Please review them. Pull requests with corrections are welcome: put them in the folder's `additions.lng`, in the same format as `pfc.lng`. A correction made directly in `pfc.lng` would be lost the next time the file is made.

The language files are UTF-16 text, like PowerBuilder's `default.lng`; `additions.lng` is UTF-8, so that changes to it show up in diffs. Each line is an entry: a message by its ID (`pfc_logon_enterid="..."`) or a caption by its English text (`"&Cancel"="&Abbrechen"`). The PFC documentation describes the format and the service.

## Using a dictionary

1. Start the Translation Toolkit (for example `ptt250.exe` in the PowerBuilder 2025 `TransTlk` folder) and open or create a project for the PFC libraries.
2. Import the dictionary for the language you want.
3. Have the toolkit apply the translations and produce the translated libraries.

The exact steps are in the toolkit's help file, `ptt.chm`, in the same folder.

Translated libraries are generated output. Keep the dictionaries as the source of truth, and regenerate the libraries from the current PFC source whenever the PFC changes. That way fixes made to the PFC since the last translation are kept.
