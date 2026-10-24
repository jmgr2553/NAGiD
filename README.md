# NAGiD 👑

**Non-exhaustive Accessible Genizah Database**

*Beta release v0.3.0* · Juan Moreno Gonzalez ([ORCID 0009-0003-6528-0736](https://orcid.org/0009-0003-6528-0736)), Faculty of Asian and Middle Eastern Studies, University of Cambridge

NAGiD is a JSON database of **10,952 Cairo Genizah letters**. It brings metadata and transcriptions from several open sources together into one record per shelfmark, and adds dates and language labels produced by AI where the sources had none.

> ⚠️ **Beta.** The data is incomplete and parts of it are machine-generated. Check anything important against the original sources.

---

## Download

| File | Size | Contents |
|---|---|---|
| `data/nagid_letters_v0.3-beta.json` | 23 MB | the full dataset |
| `nagid_letters_v0.3-beta.json.zip` | 7 MB | the same file, zipped (attached to the [release](https://github.com/jmgr2553/NAGiD/releases)) |

```python
import json

with open("data/nagid_letters_v0.3-beta.json", encoding="utf-8") as f:
    nagid = json.load(f)

letter = nagid["T-S 13J35.3 + AIU VII.A.23"]
print(letter["Info"], letter["dateYear"], letter["Language1"])
```

## Structure

The file is one JSON object. Each **key is a shelfmark**; joined fragments are written with ` + `, e.g. `"T-S 13J35.3 + AIU VII.A.23"`. Each value is a record with these fields:

| Field | Description | Values |
|---|---|---|
| `nliID` | National Library of Israel (Ktiv) system number | string; `0` if none was found |
| `pgpID` | Princeton Geniza Project document ID | integer |
| `Info` | Description of the document (from PGP) | free text |
| `editionTXT` | Transcription of the text | text; `"NONE"` if none is available |
| `edSource` | Where the transcription comes from | `"MiDRASH"`, `"PGP"`, `"NA"` |
| `dateYear` | Year of the letter (CE) | year; `"UNK"` unknown; `"MULTI"` several dates; `-1` undatable per PGP |
| `dateSource` | Where the date comes from | `"PGP"`, `"CUDL"`, `"AI"`, `"NA"` |
| `Language1` | Main language | e.g. `"Judaeo-Arabic"`, `"Hebrew"`, `"Arabic"`, `"multi"`, `"UNK"` |
| `Language2` | Second language, if any | same as above |
| `Sender`, `Addressee` | People | *not yet filled in (`"UNK"`)* |
| `Origin`, `Destination` | Places | *not yet filled in (`"UNK"`)* |
| `Topic` | Subject | *not yet filled in (`"UNK"`)* |

**Note on types:** in this beta, `dateYear` is an integer when it comes from PGP and a string when it comes from any other source. `nliID` is the integer `0` when there is no match. Convert both before you compare values.

## Coverage (v0.3.0-beta)

| | Records | Share |
|---|---|---|
| Letters | 10,952 | 100% |
| With transcription | 8,646 | 79% (MiDRASH 5,057 · PGP 3,590) |
| With NLI ID | 8,618 | 79% |
| With main language | 10,462 | 96% |
| With date | 2,008 | 18% (AI 885 · PGP 709 · CUDL 414) |

Main languages: Judaeo-Arabic 5,734 · Hebrew 1,602 · multi 1,600 · Arabic 1,326 · Ladino 116 · others < 30 each.

## Known limitations

- **Organised by shelfmark, not by fragment.** A shelfmark can contain several fragments, or be part of a join.
- **Not exhaustive.** Only letters that could be matched across the sources are included.
- **Machine-generated transcriptions.** Transcriptions with `edSource: "MiDRASH"` were produced automatically (HTR) and have not been corrected by hand.
- **AI-generated values.** Dates with `dateSource: "AI"` and the language labels were produced by models and may be wrong.
- **Empty fields.** People, places and topics are planned for later releases.

## Sources and credits

NAGiD is derived from the following sources:

- **Princeton Geniza Project (PGP)** — descriptions, IDs, dates and transcriptions. Rustow, M., Koeser, R. S., Richman, R., Ryzhova, K., Bensalim, A., & Abdellatif, M. (2026). *Princeton Geniza Project datasets* (Version v1.1) [Data set]. Zenodo. [doi:10.5281/zenodo.18716581](https://doi.org/10.5281/zenodo.18716581) · CC BY-NC 4.0
- **MiDRASH** — automatic (HTR) transcriptions. Stoekl Ben Ezra, D., Bambaci, L., Kiessling, B., Lapin, H., Ezer, N., Lolli, E., Rustow, M., Dershowitz, N., Kurar Barakat, B., Gogawale, S., Shmidman, A., Lavee, M., Siew, T., Raziel Kretzmer, V., Vasyutinsky Shapira, D., Olszowy-Schlanger, J., & Gila, Y. (2025). *MiDRASH Automatic Transcriptions of the Cairo Geniza Fragments* [Data set]. Zenodo. [doi:10.5281/zenodo.17734473](https://doi.org/10.5281/zenodo.17734473) · CC BY 4.0
- **Cambridge Digital Library (CUDL)** — dates for Taylor-Schechter letters
- **National Library of Israel / Ktiv** — manuscript identifiers
- **Dicta** — manuscript catalogue matching

## License

[CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/). Because NAGiD contains PGP data, which is licensed CC BY-NC 4.0, it is released under the same non-commercial license. When you use NAGiD, please also credit the original sources listed above.

## Citation

See [`CITATION.cff`](CITATION.cff), or use GitHub's **"Cite this repository"** button.
