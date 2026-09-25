# Data Quality Notes

Counts below are for the full downloaded catalogue. Figures restricted to the
Turkey bounding box are marked as such.

## Finding 1 — A gap in the AFAD catalogue, December 2013

**What it is**

December 2013 is missing data. The catalogue holds 324 records for that month,
while the other eleven months of 2013 average 2,117 records each.

**Evidence**

- 324 records in December 2013 against a 2,117/month average for the rest of the
  year — about one sixth.
- Every day of the month is present, but each day is reduced by roughly the same
  proportion. An outage in the recording network would leave some days empty and
  others normal. This is not that shape.
- 31 December 2013 has no records at all. Of the fifteen Decembers in the data,
  fourteen have records on the 31st, between 38 and 130 of them. Only 2013 has none.
- Querying AFAD's own download interface for December 2013, using the same
  coordinate box, returns 325 records. My file holds 324. The one-record
  difference is most likely the UTC / local-time boundary.

**How I found it**

I was not looking for it. I ran `describe()` on the monthly counts and the
minimum came back as 289 (Turkey box only). The rest of 2013 averages over two
thousand records a month, so a month in the low hundreds surprised me. My first
thought was that something had gone wrong in my own download.

**Why it is not a download error**

If the download had been made in chunks and one chunk ended at
`31-12-2013 00:00:00`, 31 December would be missing by construction. So I checked
every year. All fourteen other Decembers have records on the 31st; only 2013
does not. AFAD's own interface returns the same monthly count as my file. The
gap is in the source, not in my copy.

**A hypothesis I ruled out**

My first explanation was a change in detection threshold — that small
earthquakes were not being processed that month, so only larger ones entered the
catalogue. If that were true, December's smallest recorded magnitude would sit
above its neighbours'.

It does not. November 2013, December 2013 and January 2014 all bottom out at
magnitude 0.0, and December's median magnitude (1.7) is *lower* than November's
(2.2). December's records skew smaller, not larger — the opposite of what a
raised threshold produces. The hypothesis is dead.

I have no explanation for the gap, and the catalogue offers none.

**Why it matters**

This project asks whether earthquakes are becoming more frequent. A gap like
this is a serious problem for that question: it means I cannot tell whether the
count genuinely rose or fell from 2012 to 2013, because part of 2013 is simply
not there. The shortfall is roughly 1,800 records, about 7% of the year.

Anyone counting rows per year absorbs this hole without seeing it, and 2013 comes
out looking quieter than it was.

**What I do about it**

I flag it rather than delete it. Deleting the month would throw away 324 real
records. Leaving it unmarked would be worse: someone reading the data later would
take December 2013 at face value and never know what was missing. The flag puts
the gap in the data itself, not only in this file.

In the monthly chart the gap shows up as a dip. I do not patch or interpolate it.
Showing the hole is more honest than filling it.