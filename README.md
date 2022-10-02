# 762 Team 3 Project Implementation 

## Prerequisites
* **Edge is installed**
* **The UiPath extension for Edge is installed and enabled**, give all permissions.
  * This can be installed via UiPath Studio in `Home > Tools > UiPath Extensions > Edge`
 

## Usage

1. Clone repo and open process in UiPath
2. Open file named FindPHEVs.xaml
3. **Make sure there are no instances of the relevant trademe page running on Edge**
4. **Make sure the `results.xlsx` file is NOT open or being accessed somewhere else**
5. Press `Ctrl + F6` to run (This will take approx 5 minutes, please don't close UiPath or terminate the automation within this time)
6. After the automation is completed, the results of the scraping can be found in `results.xlsx` under the root directory. 


## Implementation Notes
* Edge is used as the browser for this automation as it is more stable than Chrome for UiPath. UiPath is frequently unable to detect that the UiPath extension is installed on Chrome. 
* There is a 6 second delay when the browser is first started up to allow the webpage to load.
* There is a 4 second delay when navigating to each new page to allow the new listings to load.
