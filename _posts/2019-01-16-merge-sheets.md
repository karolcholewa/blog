---
layout: post
title: "Combine Multiple Worksheets Into One"
categories: [MSExcel]
---


I haven’t tested it for some time, but this should work for merging two Excel worksheets, in one spreadsheet, into a third one - Combined.

1. Hold down the **ALT + F11** keys, and it opens the Microsoft Visual Basic for Applications window.
2. Click **Insert > Module**, and paste the following code in the Module Window

```
Sub Combine()
Dim J As Integer
On Error Resume Next
Sheets(1).Select
Worksheets.Add
Sheets(1).Name = "Combined"
Sheets(2).Activate
Range("A1").EntireRow.Select
Selection.Copy Destination:=Sheets(1).Range("A1")
For J = 2 To Sheets.Count
Sheets(J).Activate
Range("A1").Select
Selection.CurrentRegion.Select
Selection.Offset(1, 0).Resize(Selection.Rows.Count - 1).Select
Selection.Copy Destination:=Sheets(1).Range("A65536").End(xlUp)(2)
Next
End Sub
```

3. Then press **F5** key to run the code, and all the data in the workbook has been merged into a new worksheet named **Combined** which will add before all worksheets.

## Resources
*   [Merge Multiple Worksheets Into One](https://www.extendoffice.com/documents/excel/1184-excel-merge-multiple-worksheets-into-one.html)
*   [Paste Unique](https://www.extendoffice.com/documents/excel/2891-excel-paste-unique.html)
*   [Convert Text to Columns](https://support.office.com/en-us/article/Split-text-into-different-columns-with-the-Convert-Text-to-Columns-Wizard-30B14928-5550-41F5-97CA-7A3E9C363ED7)




