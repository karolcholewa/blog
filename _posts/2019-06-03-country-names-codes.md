---
layout: post
title: "Convert Full Country Names Into Country Codes"
categories: MSExcel
---

This one is useful for data preparation before importing records to a standard data extension. For example you will filter N records by a column Country. If you build a set of filters and filtered data extensions from scratch - this is not an issue. Look up the Country column in your source data file and make sure your filter uses the same value in the criteria property. What if you want to reuse a set of existing filters, filter activities and make your life easier but your filters contain abbreviated country codes and the input file has full names in the Country column. Values don’t match but this is a simple formula for MS Excel file does the trick. You could do a conversion directly in the DE using the SQL CASE statement but in case you need to use an Excel file and import it, here is how. 


## Reference table for country names and codes



1. In MS Excel create a new file
2. Enter the following column heading names: _Country, ISO-2, ISO-3, FIPS_
3. Fill out each column with relevant data for example: _Austria, AT, AUT, AU_
4. Save As _countryCodes.xlsx_

_Table 1 - countryCodes.xlsx file_


<table>
  <tr>
   <td><strong>Country</strong>
   </td>
   <td><strong>ISO-2</strong>
   </td>
   <td><strong>ISO-3</strong>
   </td>
   <td><strong>FIPS</strong>
   </td>
  </tr>
  <tr>
   <td>Austria
   </td>
   <td>AT
   </td>
   <td>AUT
   </td>
   <td>AU
   </td>
  </tr>
  <tr>
   <td>Poland
   </td>
   <td>PL
   </td>
   <td>POL
   </td>
   <td>PL
   </td>
  </tr>
  <tr>
   <td>United Kingdom
   </td>
   <td>GB
   </td>
   <td>GBR
   </td>
   <td>UK
   </td>
  </tr>
</table>



## Find and Replace Cells in the Source Input File

_Table 2 - dataInput.xlsx file_


<table>
  <tr>
   <td><strong>A</strong>
   </td>
   <td><strong>B</strong>
   </td>
   <td><strong>C</strong>
   </td>
   <td><strong>D</strong>
   </td>
  </tr>
  <tr>
   <td>12345678
   </td>
   <td>heidi@domain.at
   </td>
   <td><strong>AT</strong>
   </td>
   <td>Austria
   </td>
  </tr>
  <tr>
   <td>14101939
   </td>
   <td>janusz@domain.pl
   </td>
   <td><strong>PL</strong>
   </td>
   <td>Poland
   </td>
  </tr>
  <tr>
   <td>87654321
   </td>
   <td>sam@domain.uk
   </td>
   <td><strong>GB</strong>
   </td>
   <td>United Kingdom
   </td>
  </tr>
</table>


To change country names to country codes do the following:



1. Open the file
2. Insert a new column adjacent to the country column (column C in the example)
3. In the C column enter the formula:

```
=vlookup(D1,countryCodes!A:D,2,FALSE)
```



**Result**: The formula retrieves a country code from the column_index 2 of the countryCodes.xlsx file, that is ISO-2. To retrieve ISO-3 value, use the 3 for column_index and 4 to get FIPS codes.


## Resources



*   [https://countrycode.org/](https://countrycode.org/)
*   [https://en.wikipedia.org/wiki/ISO_3166-1](https://en.wikipedia.org/wiki/ISO_3166-1)
*   [https://en.wikipedia.org/wiki/List_of_FIPS_country_codes](https://en.wikipedia.org/wiki/List_of_FIPS_country_codes)
*   [https://stackoverflow.com/questions/37297197/convert-three-letter-country-codes-to-full-country-name-in-excel](https://stackoverflow.com/questions/37297197/convert-three-letter-country-codes-to-full-country-name-in-excel)
*   [https://raw.githubusercontent.com/mysociety/gaze/master/data/fips-10-4-to-iso-country-codes.csv](https://raw.githubusercontent.com/mysociety/gaze/master/data/fips-10-4-to-iso-country-codes.csv) 
*   [https://exceljet.net/excel-functions/excel-vlookup-function](https://exceljet.net/excel-functions/excel-vlookup-function)