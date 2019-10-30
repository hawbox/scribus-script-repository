# Mail merge

This is a small Mail merge solution for Scribus.

Its default behavior is to look for `csv` files with the same name as the `sla` file and create one `pdf` per row.

Configuration is planned trough a `yaml` file with the same name as the Scribus file.

## Status

This script is in its early stages.

- At the time of writing, you need to [patch Scribus](https://bugs.scribus.net/view.php?id=15886) to get the `revertDoc()` scripter command and run this script.
- The script cannot yet be configured, only the default behavior is implemented.
- It goes through the whole document and looks for placeholders (_labels_ between `{` and `}`) in all text frames and stores the list of frame names and placeholder positions.
- It reads a `csv` file with the same name as the Scribus file, stored next to it.
- The first line of the `csv` file is a header with the name of the fields.
- You need to save the _template_ document before running the script (unsaved changes will be used for the first row and then discarded for the other rows).
- The script replaces all occurences of the placeholders with the matching values in the current row of the `csv` file.
- It creates one Pdf per row, stores it next to the Scribus file and adds the value of each first field to the file name.
- After each row, the document is reverted to the saved state and the replacements are discarded.

## Usage

- Create a Scribus document.
- Define the placeholders with the `{` and `}` _markers_ and save the document.
- The formatting of the placeholders will be kept (the first character between the markers will be determinant).
- Put a `csv` with the same name as the Scribus document close to it (if your document is named `letter.sla` you will need a `letter.csv` as the data source).
- In the first line of the `csv` file put the name of the placeholders, separated by commas (it must be a valid `csv` file: you will probably want to generate the file with a spreadsheet and avoid filling it by hand)
- The other rows of the `csv` files will contain the values, also speparated by commas.


## Todo

- support images.
  - For image placeholder use names like `images/portrait-{name}.jpg`. The images will then need to be in the given directory (mostly, in the same one as the placeholder)
- read data from json files
- define and support the `yaml` project file.
  - alternative placeholder markers
  - data source
  - custom separator for json files?
  - pdf
    - version
    - target directory
    - variable file name field
    - base name
- log errors
  - unmatched fields

# Future plans

- Allow the creation of a single Pdf with all the created content.