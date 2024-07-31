**CalendarSync: Auto Event Poster** is a Google Apps Script project designed to automate the process of creating and updating Google Calendar events based on data from a Google Sheets document. This tool simplifies calendar management by automatically generating all-day events and setting reminders, ensuring you never miss an important date.

## Key Features

### 1. Automatic Event Creation:
The tool automatically creates calendar events based on the information you input into a Google Sheets document.

### 2. All-Day Events:
Events are created as all-day entries, so you don’t need to worry about setting specific start and end times.

### 3. Custom Descriptions:
Each event includes a detailed description generated from specific columns in your Google Sheets, ensuring that you have all the necessary information at your fingertips.

### 4. Reminders:
The tool automatically sets a reminder for each event, notifying you one day in advance to help you stay on top of your schedule.

### 5. Real-Time Updates:
Whenever you update the Google Sheets document, the changes are reflected in your Google Calendar automatically, keeping everything synchronized.

## Prerequisites
- A Google account.
- Access to Google Sheets and Google Calendar.
- Basic knowledge of Google Apps Script.

## Setup Instructions

### Step 1: Set Up Your Google Sheets Document
1. Open Google Sheets and create a new spreadsheet or use an existing one.
2. Name your sheet (e.g., "new sheet").
3. Ensure your sheet has the following columns:
   - Column A: Event Name
   - Column B: Additional Description 1
   - Column C: Event Date

### Step 2: Get Your Google Calendar ID
1. Open Google Calendar.
2. Create an new calender or Go to the calendar you want to use and click on the three dots next to it.
3. Select "Settings and sharing."
4. Under "Integrate calendar," copy the "Calendar ID."

### Step 3: Set Up Google Apps Script
1. In your Google Sheets document, go to `Extensions > Apps Script`.
2. Delete any existing code in the script editor and paste the script from thefiles:
3. Replace YOUR_SPREADSHEET_ID with your actual Google Sheets document ID.
4. Replace your_calendar_id@group.calendar.google.com with your Google Calendar ID.

### Step 4: Authorize and Run the Script
1. Save the script.
2. Run the createCalendarEvent function for the first time to authorize the script.
3. A pop-up will ask you to authorize the script to access your Google Sheets and Google Calendar.

### Step 5: Set Up Triggers
1. In the Apps Script editor, go to the Triggers section (clock icon on the left).
2. Click on Add Trigger.
3. Choose the onEdit function.
4. Set the event type to "From spreadsheet" and "On edit."
 
### Manual Execution
You can manually run the script from the Apps Script editor by clicking the play button.
Alternatively, you can use the custom menu Calendar Events > Post to Calendar in your Google Sheet.
