
function doGet(e) {
  try {
   
    const sheetName = "משמרות 2025";

    const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName(sheetName);
    
    if (!sheet) {
      return ContentService.createTextOutput("Error: Sheet not found. Check SHEET_NAME. It was set to: " + sheetName);
    }

    const values = sheet.getRange("A1:O64").getValues();
    
    const textData = values.map(row => row.join('\t')).join('\n');

    return ContentService.createTextOutput(textData)
                         .setMimeType(ContentService.MimeType.TEXT);
  } catch (err) {
   ה
    return ContentService.createTextOutput("Error in Apps Script: " + err.message + " (Line: " + err.lineNumber + ")");
  }
}
