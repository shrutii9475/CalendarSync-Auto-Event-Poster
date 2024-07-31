# CalendarSync-Auto-Event-Poster
CalendarSync: Auto Event Poster is a Google Apps Script project designed to automate the process of creating and updating Google Calendar events based on data from a Google Sheets document. This tool simplifies calendar management by automatically generating all-day events and setting reminders, ensuring you never miss an important date.

# CalendarSync: Auto Event Poster

**CalendarSync: Auto Event Poster** is a Google Apps Script project designed to automate the process of creating and updating Google Calendar events based on data from a Google Sheets document. This tool simplifies calendar management by automatically generating all-day events and setting reminders, ensuring you never miss an important date.

## Features
- Automatically create all-day events in Google Calendar from Google Sheets data.
- Add event descriptions using specified columns from the Google Sheets document.
- Set reminders for events one day in advance.
- Update calendar events whenever the Google Sheets document is edited.

## Prerequisites
- A Google account.
- Access to Google Sheets and Google Calendar.
- Basic knowledge of Google Apps Script.

## Setup Instructions

### Step 1: Set Up Your Google Sheets Document
1. Open Google Sheets and create a new spreadsheet or use an existing one.
2. Name your sheet (e.g., "All applications").
3. Ensure your sheet has the following columns:
   - Column B: Event Name
   - Column C: Additional Description 1
   - Column D: Additional Description 2
   - Column E: Additional Description 3
   - Column F: Event Date
   - Column H: Additional Description 4

### Step 2: Get Your Google Calendar ID
1. Open Google Calendar.
2. Go to the calendar you want to use and click on the three dots next to it.
3. Select "Settings and sharing."
4. Under "Integrate calendar," copy the "Calendar ID."

### Step 3: Set Up Google Apps Script
1. In your Google Sheets document, go to `Extensions > Apps Script`.
2. Delete any existing code in the script editor and paste the following updated script:

   ```javascript
   function createCalendarEvent() {
     var sheetUrl = 'https://docs.google.com/spreadsheets/d/YOUR_SPREADSHEET_ID/edit'; // Replace with your Google Sheets URL
     var spreadsheet = SpreadsheetApp.openByUrl(sheetUrl);
     var sheetName = 'All applications';
     var sheet = spreadsheet.getSheetByName(sheetName);
     
     if (!sheet) {
       Logger.log("Sheet not found: " + sheetName);
       return;
     }
     
     var calendarId = 'your_calendar_id@group.calendar.google.com'; // Replace with your Google Calendar ID
     var calendar = CalendarApp.getCalendarById(calendarId);
     
     var data = sheet.getDataRange().getValues();
     
     for (var i = 1; i < data.length; i++) {
       var eventTitle = data[i][1]; // Event name from 2nd column
       var eventDate = new Date(data[i][5]); // Date from 6th column
       var col3 = data[i][2]; // Data from 3rd column
       var col4 = data[i][3]; // Data from 4th column
       var col5 = data[i][4]; // Data from 5th column
       var col8 = data[i][7]; // Data from 8th column

       // Creating a description using columns 3, 4, 5, and 8
       var description = "Column 3: " + col3 + "\n" +
                         "Column 4: " + col4 + "\n" +
                         "Column 5: " + col5 + "\n" +
                         "Column 8: " + col8;

       // Creating an all-day event
       var event = calendar.createAllDayEvent(eventTitle, eventDate, {description: description});

       // Adding a reminder 1 day before the event
       event.addPopupReminder(24 * 60);
     }
   }

   function onOpen() {
     var ui = SpreadsheetApp.getUi();
     ui.createMenu('Calendar Events')
         .addItem('Post to Calendar', 'createCalendarEvent')
         .addToUi();
   }

   function onEdit(e) {
     createCalendarEvent();
   }
