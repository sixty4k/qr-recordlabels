This is a small program to generate labels from Discogs CSV dumps, with the unique Discogs URL as a QR code.

These labels can be used by for example record stores or dealers at a record fair to mark records. Users could then simply scan the QR code and be taken to the appropriate Discogs page if, of course, the information has been correctly entered ("garbage in, garbage out").

A few notes:

* the labels are generated for a particular label layout (A4, 3 columns, 8 rows) because those are the only labels that I have available right now
* only Discogs collection CSV dumps can be processed, not any of the other lists
* depending on your printer some of the labels might not be printed correctly. This is because some printers cannot print borderless

Blog post: https://vinylanddata.blogspot.com/2017/09/generating-qr-stickers-from-discogs.html

## Usage

```bash
$ python generate_labels.py -h
usage: generate_labels.py [-h] [-c FILE] [-f FILE] [-o FILE] [-p PROFILE]

optional arguments:
  -h, --help            show this help message and exit
  -c FILE, --config FILE
                        path to configuration file
  -f FILE, --file FILE  path to CSV file
  -o FILE, --out FILE   path to output PDF file
  -p PROFILE, --profile PROFILE
                        name of label profile
```

## Config file format

The `[genral]` section options:
 * swap columns: by default labels have text on the left, QR code on the right.  Setting this to `yes` reverses that.
 * type: should always be `general`, honestly not sure why the general section should have a type...

A config file can have multiple profiles, which define an output format, the options for a profile are:
 * type: should be `profile` 
 * rows: how many rows
 * columns: how many columns
 * height: 

```ini
[general]
type = general
#swap-columns = yes

[dymo11356]
type = profile
rows = 1
columns = 1
height = 44
width = 89
unit = mm
description = Dymo 11356 labels
fields = artist:title:media:sleeve

[a4-8x3]
type = profile
rows = 8
columns = 3
description = A4 sheet with labels, no extra margins
pagesize = A4
```
