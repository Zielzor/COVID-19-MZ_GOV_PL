# COVID-19-MZ_GOV_PL
COVID-19 statistics for Poland, captured from Polish Health Ministry's Twitter @MZ_GOV_PL

## Why from Twitter

Polish Ministry of Health does not publish data in human-readable format.

On the Ministry of Health website, the <a href="https://www.gov.pl/web/koronawirus/wykaz-zarazen-koronawirusem-sars-cov-2">the incidence table</a> shows only the current day status and only in two categories: Number of confirmed cases (cumulative) and number of deaths (cumulative).

On <a href="https://twitter.com/MZ_GOV_PL">their Twitter account</a>, the Ministry of Health shows data in 7 categories in 3 ways:

* The number of confirmed cases (cumulative) and the number of deaths (cumulative) - in text form, as numbers in tweets.
* The number of tests performed (cumulative) - as a bitmap image(!)
* Hospitalized (for the current day), quarantined (for the current day), under surveillance (for the current day), recovered (cumulative) - as another bitmap image(!)

I automated downloading these data from Twitter using scripts in Python.

To read numbers from bitmaps, I used Python packages for image recognition (to filter colors in the background and then to OCR the text).

I will make the code available soon - when I organize it and improve it a bit.

Data in other columns were entered manually.
## CSV file description:
`data` directory contains CSV files.
### Format
The following is a bit inconsistent but for historical reasons: 
* Column names are in Polish; in particular, the date column name is 'Data'. 
* However, dates in the date column are in American date format: `"%m/%d/%Y"`
* File name: `"cor." + "%Y.%m.%d" + ".csv"`

### Column headers
For convenience of users, below I explain the column headers:
| Polish | English | Comment |
|--------|---------|---------|
| "Data" |  "date" |         | 
| "Dzień" |  "day"|   since the 1st case | 
| "Wykryci zakażeni"| "confirmed"|  cumulative| 
| "Testy" |  "tested"|  cumulative| 
| "Hospitalizowani" |  "hospitalized"| for a given day, not cumulative| 
| "Zmarli" |  "deaths"|  cumulative| 
| "Kwarantanna" |  "quarantined"| for a given day, not cumulative| 
| "Nadzór" |  "surveillance"|   under epidemiological surveillance; for a given day, not cumulative| 
| "Testy, wartości przybliżone" |  "tests, approximate"|  there were no data for one day, just an approximate number was given on Twitter @MZ_GOV_PL; cumulative| 
| "Kwarantanna po powrocie do kraju" | "quarantined after return to Poland"| for a given day, not cumulative| 
| "Wydarzenia" | "events"| restrictions introduced by Polish government (described in Polish)| 
| "Wyzdrowiali" |  "recovered"|  cumulative| 

Here, column headers as a dictionary (perhaps this will be useful for copy-pasting into Python code): 

`original_Polish_header : English_translation # comment` 

```
"Data" : "date", 
"Dzień" : "day",  #  since the 1st case 
"Wykryci zakażeni" : "confirmed",  # cumulative
"Testy" : "tested",  # cumulative
"Hospitalizowani" : "hospitalized", # for a given day, not cumulative
"Zmarli" : "deaths", # cumulative
"Kwarantanna" : "quarantined", # for a given day, not cumulative
"Nadzór" : "surveillance",  # under epidemiological surveillance; for a given day, not cumulative
"Testy, wartości przybliżone" : "tests, approximate",  # there were no data for one day, 
                                                       # just an approximate number was given 
                                                       # on Twitter @MZ_GOV_PL; cumulative
"Kwarantanna po powrocie do kraju" : "quarantined after return to Poland", # for a given day,
                                                                           # not cumulative
"Wydarzenia" : "events",  # restrictions introduced by Polish government (described in Polish)
"Wyzdrowiali" : "recovered" # cumulative
```
#### Restrictions introduced by Polish government
For convenience of users, below I explain the cells content in `"Wydarzenia"` ("events") column: 

| Polish | English | Comment |
|--------|---------|---------|
|"Zamknięcie szkół i instytucji kulturalnych"| "Closing schools and cultural institutions|
|"Ogłoszenie stanu epidemii"|"State of epidemic announced"|
|"Dalsze restrykcje (zgromadzenia max 2 os.)" | "Further restrictions (public meetings  not allowed for more than 2 people)"|
|"Kolejne restrykcje (zakaz wychodzenia młodzieży, 2 m odstępu, zamknięcie salonów fryzjerskich etc.)" | "Next restrictions (going out not allowed for youth < 18 years old, maintain a distance of at least  2 m in public, closing of hairdressing salons, etc.")|

Here, cells content in `"Wydarzenia"` ("events") column is shown as a dictionary (perhaps this will be useful for copy-pasting into Python code): 
`original_Polish_header : English_translation # comment` 

```
"Zamknięcie szkół i instytucji kulturalnych" : "Closing schools and cultural institutions",
"Ogłoszenie stanu epidemii" : "State of epidemic announced",
"Dalsze restrykcje (zgromadzenia max 2 os.)" : "Further restrictions (public meetings \
  not allowed for more than 2 people)",
"Kolejne restrykcje (zakaz wychodzenia młodzieży, 2 m odstępu, zamknięcie salonów fryzjerskich etc.)" : \
  "Next restrictions (going out not allowed for youth < 18 years old, maintain a distance of at least \
  2 m in public, closing of hairdressing salons, etc.)"
```
