# Raw data

`afad_2011_2026.csv` is not committed to this repository (about 44 MB).
It is the unmodified export of AFAD's earthquake catalogue, and can be
downloaded again from the source.

## How to reproduce it

1. Open AFAD's earthquake catalogue: https://deprem.afad.gov.tr/event-catalog
2. Set the query:

   | Field | Value |
   |---|---|
   | Time zone | **TSİ** (Turkish time, UTC+3), not UTC |
   | Date range | 17-09-2011 00:00:00 → 19-09-2026 23:59:59 |
   | Latitude | 27.5959 – 48.4219 |
   | Longitude | 18.7733 – 51.7763 |
   | Depth, magnitude | left empty |
   | Location | left empty |
   | Özellikler | Tümü, Sadece Katalog |

3. Export as CSV and save it here as `afad_2011_2026.csv`.

Set the end time to `23:59:59`. With `00:00:00` the query stops at the
start of the last day and silently leaves that whole day out.

## What the file should contain

- 481,591 records
- First record: 17/09/2011 21:51:54 · last record: 19/09/2026 20:24:25 (TSİ)
- Columns: `Date, Longitude, Latitude, Depth, Rms, Type, Magnitude, Location, EventID`
- `Date` is day-first text (`DD/MM/YYYY HH:MM:SS`)
- Encoding: UTF-8 with BOM

My copy was downloaded on 19 September 2026. AFAD can revise catalogue
entries after publication, so a later download may differ slightly. If
the record count does not match, `validate()` in `notebooks/02_clean.ipynb`
will stop with an error rather than letting the difference pass silently.
