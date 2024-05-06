# Google-Sheets-to-Forms
Creating Google Forms from Google Sheets - learning the code
Coding Google Sheet into Google Form

To automate the creation of a Google Form from a Google Sheet using Google Apps Script, you'll need to write a script that reads the data from the Sheets and uses it to populate a new Google Form. This process involves using Google Apps Script, a JavaScript-based platform that lets you extend Google Sheets, Docs, and Forms with custom functionality.

Below, I’ll walk you through a basic script that does the following:
- Reads questions from a Google Sheet.
- Creates a Google Form.
- Adds questions to the form based on the data in the Sheet.

### Step-by-Step Guide to Create the Script

#### 1. Prepare Your Google Sheet
Make sure your Google Sheet is formatted correctly. For example:
- Column A: Question Title
- Column B: Question Type (e.g., "multipleChoice", "text")
- Column C and onward: Options for multiple choice questions (if applicable)

#### 2. Open the Script Editor
- Open your Google Sheet.
- Click on `Extensions` > `Apps Script`.

#### 3. Write the Script
Replace the script in the Apps Script editor with the following code:

```javascript
function createForm() {
 // Open the Spreadsheet
 var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
 var rows = sheet.getDataRange().getValues();
  
 // Create a new Form
 var form = FormApp.create('New Form');

 // Iterate over the rows in the sheet
 for (var i = 0; i < rows.length; i++) {
  var questionTitle = rows[i][0];
  var questionType = rows[i][1];
  var options = rows[i].slice(2);

  // Add question based on type
  if (questionType === "text") {
   form.addTextItem()
     .setTitle(questionTitle);
  } else if (questionType === "multipleChoice") {
   var item = form.addMultipleChoiceItem();
   item.setTitle(questionTitle)
     .setChoiceValues(options);
  }
 }
}
```

#### 4. Save and Run the Script
- Save the script by clicking the disk icon or File > Save.
- Run the script by clicking on the play icon or Run > Run function > createForm.
- You might need to authorize the script the first time you run it.

#### 5. Check Your New Form
Once the script runs successfully, it will create a new Google Form based on the data from your Sheet. You can find the form in your Google Drive or by clicking on the recent forms in Google Forms.

### Advanced Customizations
Depending on your needs, you can customize the script to handle different types of questions, required fields, and other settings available in the Google Forms API.

This basic example demonstrates the core functionality of creating a Google Form programmatically. You can extend and modify the script to suit more complex requirements, like adding validation, branching logic, or customizing the form's appearance.
