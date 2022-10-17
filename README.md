# INFOSYS 300 / SOFTENG 762 Team 3 Project Implementation

[Environmentally Friendly Second-hand Cars](https://github.com/lin8231/762-impl)

---

## Implementation by

- **Mercury Lin**: Scraping data and storing to Excel
- **Siwei Yang**: Excel data sanitisation/manipulation
- **Kirsty Gong**: Export sanitised data to pdf
- **Molina Vincent**: Exception Handling and Testing

## Prerequisites

- **Edge is installed**
- **The UiPath extension for Edge is installed and enabled**, give all permissions.
  - This can be installed via UiPath Studio in `Home > Tools > UiPath Extensions > Edge`

## Final Result

1. **processedData.csv**: Contains the Make, Model, Year, Mileage, ImportHistory and FuelEconomy of all the listing
2. **report.pdf**: Contains a summarises record and graph for all the different PHEV models and their manufacturing year.

## Usage

### Run with UiPath Studio

1. Clone this repository and open the project in UiPath
2. Open file named `Main.xaml`
3. **Make sure there are no instances of the relevant trademe page running on Edge**
4. **Make sure all the spreadsheet files are NOT opened or being accessed somewhere else**
5. Press `Ctrl + F5` or click **_Run_** to run the project (This will take a long while, please don't close UiPath or terminate the automation within this time)
6. After the automation is completed
   - the results of the scraping can be found in `results.xlsx` under the root directory.
   - the results of the sanitisation and manipulation can be found in `processedData.csv` and `reportData.xlsx` under the root directory.
   - `reportData.xlsx` will be further process to extract the data for each car manufactures.
   - Generate a bar graph for each car manufactures data.
   - Insert each car manufacture data and the corresponding graph into a word document `report.docx`.
   - Export the word document to PDF `report.pdf`.

### Run with UiPath Assistant

1. Sign off from UiPath Assistant if you are already signed in.
2. Use UiPaht Assistant with offline mode.
3. Copy and paste `Auto-Generate-PHEV-Car-Report.1.0.3.nupkg` to `C:\ProgramData\UiPath\Packages`.
4. Install the package.
5. **Make sure there are no instances of the relevant trademe page running on Edge**
6. Run the installed package (This will take a long while, please don't close UiPath or terminate the automation within this time).
7. After the automation is completed, open the folder `%USERPROFILE%\.nuget\packages\auto-generate-phev-car-report\1.0.3\lib\net45`.
   - the results of the scraping can be found in `results.xlsx` under the directory.
   - the results of the sanitisation and manipulation can be found in `processedData.csv` and `reportData.xlsx` under the directory.
   - `reportData.xlsx` will be further process to extract the data for each car manufactures.
   - Generate a bar graph for each car manufactures data.
   - Insert each car manufacture data and the corresponding graph into a word document `report.docx`.
   - Export the word document to PDF `report.pdf`.

## Implementation Notes

### Scraping

> - Edge is used as the browser for this automation as it is more stable than Chrome for UiPath. UiPath is frequently unable to detect that the UiPath extension is installed on Chrome.
> - There is a 2 second delay when navigating to each new page to allow the new listings to load.
> - The price column is extracted as a block of text instead of a single number, because the element for the price number is inconsistent depending on the type of sale. Hence, it is easier to extract the whole price block, and sanitise in the data manipulation stage.
> - Inorder to scrap the import history, we scrapped the search with no import filter, nz new filter and the imported filter. Then we compare the three scrap result to determine the search history for each lists

### Data processing

> - The data sanitisation and manipulation removed and handled unwanted data, and then transfered the data and saved it to a spreadsheet aligned with the required format in project PDF.
> - This process also generates a spreadsheet containing the subset of the data in the above spreadsheet and the counts of each PHEV for the convience of the report generation.

### Generate PDF

> - Produce a csv file for each car brand in a new Folder call graphProcess.
> - Use BlaReva.Excel package to produce a graph for each car brand in graphProcess.
> - Write each car brand data and graph to a word document.
> - Export the word document to PDF.

### Exception Handling and Testing

> - Try Catch element added to points of potential failure
> - Some delays replaced using element exists
> - Make - Model split using web URL instead of text displayed assuming the URL layout is the same for all data points
> - Closing applications that the process will edit to avoid potential errors if the user forgets to close these files from a previous run
> - Testing the final report output against expected data retrieved through manual extraction
