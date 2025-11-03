/**
 * פונקציה זו מופעלת כשקוראים ל-URL של ה-Web App.
 * היא קוראת את הנתונים מהגיליון ומחזירה אותם כטקסט רגיל.
 * זוהי גרסה פשוטה יותר.
 */
function doGet(e) {
  try {
    // ודא ששם הגיליון (הטאב) אכן "משמרות 2025"
    const sheetName = "משמרות 2025";

    const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName(sheetName);
    
    if (!sheet) {
      return ContentService.createTextOutput("Error: Sheet not found. Check SHEET_NAME. It was set to: " + sheetName);
    }

    // --- *** התיקון כאן *** ---
    // קריאה רק מהטווח שביקשת (A1 עד O57)
    // זה מתעלם מכל מה שמימין לעמודה O ומתחת לשורה 57
    const values = sheet.getRange("A1:O57").getValues();
    
    const textData = values.map(row => row.join('\t')).join('\n');

    return ContentService.createTextOutput(textData)
                         .setMimeType(ContentService.MimeType.TEXT);
  } catch (err) {
    // אם משהו נכשל, נחזיר הודעת שגיאה ברורה
    return ContentService.createTextOutput("Error in Apps Script: " + err.message + " (Line: " + err.lineNumber + ")");
  }
}
