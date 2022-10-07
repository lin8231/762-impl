# 762 Team 3 Project Implementation

Environmentally Friendly Second-hand Cars

## Implementation by

* **Mercury Lin**: Scraping data and storing to Excel
* **Siwei Yang**: Excel data sanitisation/manipulation
* **Kirsty Gong**: Export sanitised data to pdf

## Prerequisites

* **Edge is installed**
* **The UiPath extension for Edge is installed and enabled**, give all permissions.
  * This can be installed via UiPath Studio in `Home > Tools > UiPath Extensions > Edge`

## Usage

1. Clone repo and open process in UiPath
2. Open file named FindPHEVs.xaml _<= To be change to Main.xaml_
3. **Make sure there are no instances of the relevant trademe page running on Edge**
4. **Make sure all the spreadsheet files are NOT opened or being accessed somewhere else**
5. Press `Ctrl + F6` to run (This will take approx 5 minutes, please don't close UiPath or terminate the automation within this time)
6. After the automation is completed
    * the results of the scraping can be found in `results.xlsx` under the root directory.
    * the results of the sanitisation and manipulation can be found in `processedData.csv` and `reportData.xlsx` under the root directory.
7. _<= More steps to be added here_

## Implementation Notes

### Scraping

> * Edge is used as the browser for this automation as it is more stable than Chrome for UiPath. UiPath is frequently unable to detect that the UiPath extension is installed on Chrome.
> * There is a 6 second delay when the browser is first started up to allow the webpage to load.
> * There is a 4 second delay when navigating to each new page to allow the new listings to load.
> * The price column is extracted as a block of text instead of a single number, because the element for the price number is inconsistent depending on the type of sale. Hence, it is easier to extract the whole price block, and sanitise in the data manipulation stage.

### Data processing

> * The data sanitisation and manipulation removed and handled unwanted data, and then transfered the data and saved it to a spreadsheet aligned with the required format in project PDF.
> * This process also generates a spreadsheet containing the subset of the data in the above spreadsheet and the counts of each PHEV for the convience of the report generation.

### Generate PDF
> * Produce a csv file for each car brand in a new Folder call graphProcess.
> * Use BlaReva.Excel package to produce a graph for each car brand in graphProcess
> * Write each car brand data and graph to a word document (report.docx)
> * Export the word document to PDF (report.pdf)
