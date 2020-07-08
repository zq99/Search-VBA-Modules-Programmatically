## Search VBA Code Editor From An External Workbook

### Purpose

This is demonstration of a class that can search the code in a VBA Editor of project for a particular phrase.

This VBA editor can be in any Microsoft Office Product (Excel/Access/PowerPoint/Word).

The class can be used to form the basis of your own "search VBA code" tool.

The code is useful for finding any hardcoded references when you have several projects to search.

### Requirements

You must have the following VBA Project references installed in the VBE Editor reference window (minimum versions stated):

- Visual Basic For Applications
- Microsoft Excel 14.0 Object Library
- OLE Automation
- Microsoft Scripting Runtime
- Microsoft Visual Basic for Applications Extensibility 5.3
- Microsoft Access 14.0 Object Library
- Microsoft PowerPoint 14.0 Object Library
- Microsoft Word 14.0 Object Library

### Caveats

- You only be able to search the VBA code in applications that do not have the VBA editor locked (unfortunately, there is no way to programmatically unlock the VBA editor)
- For some Excel spreadsheets, you will have to make sure that the option “Trust access to the VBA project object model” has been checked. This can be found under the Macro settings option, within Trust Center.

### Implementation

This would be the code required to search the VBA code in a file called 'TestMacro.xlsm' for the word 'Hello':


    Dim oSearch     As New csSearchVBA
    Dim coResults   As New Collection
    Dim oResult     As csResults
    Dim lRow        As Long
    
    oSearch.addWord "Hello"
    oSearch.fileName = "C:\TEST\TestMacro.xlsm"
    Set coResults = oSearch.GetSearchResults
    If Not coResults Is Nothing Then
        lRow = 1
        For Each oResult In coResults
            With Sheet1
                .Cells(lRow, 1).value = oSearch.fileName
                .Cells(lRow, 2).value = oResult.Module
                .Cells(lRow, 3).value = oResult.ProcName
                .Cells(lRow, 4).value = oResult.LineOfCode
                .Cells(lRow, 5).value = oResult.LineNo
                .Cells(lRow, 6).value = oResult.ColumnNo
                .Cells(lRow, 7).value = oResult.ProcStartLineNo
                .Cells(lRow, 8).value = oResult.ProcNumberOfLines
                .Cells(lRow, 9).value = oResult.SearchValue
                lRow = lRow + 1
            End With
        Next
    End If
    
    Set oSearch = Nothing
    Set coResults = Nothing
    Set oResult = Nothing
    

### Further information

https://datapluscode.com/general/programmatically-search-vba-code/


