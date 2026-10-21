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
| 4 | (empty) | |
| 5 | English source text | `Cancel` |
| 6 | (empty) | |
| 7 | Toolkit code for the kind of text | `4` |
| 8 | Where the text appears, e.g. `Text`, `Microhelp`, `ToolBarItemText`, `Title`, `Item[]`, `Variable`, `Event Script`, `Function Script` | `Text` |
| 9 | Comment | `Created from PTT Dictionary File` |

Values that contain tabs or line breaks, such as DataWindow expressions, are wrapped in double quotes and may span several lines.

### Encoding

The files use the Windows ANSI code page (Windows-1252/ISO-8859-1) with Windows (CRLF) line endings, which is what the Translation Toolkit reads and writes. Accented characters such as `é` and `ß` are single bytes. **Don't re-save the files as UTF-8**, or those characters may come out garbled in the toolkit. GitHub may also show some accented characters incorrectly for the same reason.

## Using a dictionary

1. Start the Translation Toolkit (for example `ptt250.exe` in the PowerBuilder 2025 `TransTlk` folder) and open or create a project for the PFC libraries.
2. Import the dictionary for the language you want.
3. Have the toolkit apply the translations and produce the translated libraries.

The exact steps are in the toolkit's help file, `ptt.chm`, in the same folder.

Translated libraries are generated output. Keep the dictionaries as the source of truth, and regenerate the libraries from the current PFC source whenever the PFC changes. That way fixes made to the PFC since the last translation are kept.
