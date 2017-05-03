# xls2inv-cli #

xls2inv-cli is a command line version of [xls2inv](https://github.com/gtownlawlib/xls2inv) that can be run from a local terminal with no need for the AWS cloud services used in the original application.

xls2inv-cli is a Python 2.7 application that parses credit card order logs in Excel format and converts them to [.inv format](http://vendordocs.iii.com/#serials_elec_invoicing.html), a plain text file format used by Sierra ILS to batch upload serials invoices.

## Requirements ##

* [openpyxl Python library](http://openpyxl.readthedocs.io)

## Installation ##

1. Download xls2inv-cli:
```bash
git clone https://github.com/gtownlawlib/xls2inv-cli.git
```

2. Turn your downloaded xls2inv-cli directory into a Python virtual environment and install the openpyxl library:
```bash
virtualenv -p python2.7 path/to/xls2inv-cli
source path/to/xls2inv-cli/bin/activate
pip install openpyxl
```

## Running the Application ##

To convert an Excel file, run xls2inv-cli.py from within your virtual environment with two arguments:
1. an Excel source file (a properly-formatted Excel file in .xlsx format; see below for formatting guidelines)
2. a desired output file name (with an .inv file extension)
```bash
python path/to/xls2inv-cli.py path/to/source.xlsx path/to/output.inv
```

## Excel Formatting Guidelines ##

* Spreadsheets must be in .xlsx format.
* Each row must contain a Sierra order record number.
* Spreadsheets must contain 500 or fewer rows, not including header row. (This limitation is not enforced by the application, but Sierra will not accept .inv files with more than 500 line items.)
* Spreadsheets must contain a header row. (The application ignores row 1 of all worksheets.)
* Spreadsheet data must be contained in a single worksheet titled 'Sheet1.'
* Data must follow template column order (see below), numbered from left. (Application expects column headers but ignores header values.)
* In first row of last (8th) column, enter a procurement card name/ID (7 characters or less) that will be used to create a header invoice number. (This is used to identify the import in Sierra).
* Refunds/rebates and other negative dollar values must be preceded by a negative sign.
* All monetary values must be in U.S. dollars.
* Only the first 29 characters of the "NOTE" column will be used.

Data must appear in the following column order:
1. ORDER DATE
2. ORDER NUMBER
3. \# OF COPY
4. PRICE($)
5. S/H CHARGE &/OR SALES TAX (%)
6. TOTAL COST ($)
7. NOTE
8. STAFF CODE (row 2 only; first 7 characters used to generate header invoice ID)

A properly-formatted Excel template file (proc-card-log-TEMPLATE.xlsx) is included with the application.

## Developer Information ##

Developed by:  
Tom Boone  
Associate Law Librarian for Electronic Resources and Services  
Georgetown Law Library  
<trb74@georgetown.edu>
