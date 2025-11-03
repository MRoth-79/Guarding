function doGet() {
  try {
    // !!! שנה את "Shifts" לשם הגיליון (הטאב) שלך !!!
    const sheetName = "משמרות 2025";

    const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName(sheetName); 
    const values = sheet.getDataRange().getValues();
    const textData = values.map(row => row.join('\t')).join('\n');

    return ContentService.createTextOutput(textData)
             .setMimeType(ContentService.MimeType.TEXT);
  } catch (e) {
    return ContentService.createTextOutput(JSON.stringify({ error: e.message }))
             .setMimeType(ContentService.MimeType.JSON);
  }
}
