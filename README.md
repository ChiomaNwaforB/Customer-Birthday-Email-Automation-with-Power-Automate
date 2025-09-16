# Customer-Birthday-Email-Automation-with-Power-Automate
A Power Automate workflow that sends personalized birthday emails automatically using customer data stored in Excel  file on a shared drive and sent through Outlook.

A client approached me with a challenge: their team was manually sending hundreds of customer birthday emails each day. The process was inefficient, time consuming and prone to human error.

To address this, I designed and implemented an automated workflow using Microsoft Power Automate. The solution retrieves customer data from an Excel file stored on a shared drive and automatically sends personalized birthday emails through Outlook.

This project demonstrates how low-code automation can streamline routine business processes, reduce errors and enhance customer engagement.

**What the Automation Does:**

-Reads customer data (Name, Email, Date of Birth) from an Excel file stored on a shared drive

-Identifies customers whose birthdays match the current date

-Sends automated, personalized birthday emails using Outlook

-Supports HTML formatting for rich, branded email content

**Tools and Technologies**

-Microsoft Power Automate

-Excel (structured as a table)

-Shared Drive / OneDrive / SharePoint

-Outlook (Office 365)

**Step by Step Setup**
Step 1: Excel Table Setup

-Create a file named CUST_DATA.xlsx

-Include the following columns: Customer Name, Email, Birthday

-Format the data as a table (Insert > Table > Assign a name, e.g., CustomerTable)

-Save the file on a shared drive accessible to Power Automate

Step 2: Create the Flow

-Go to Power Automate

-Create a new Scheduled Cloud Flow

-Name the flow: Customer Birthday Emails

-Configure the recurrence to run every day (set the correct time zone)

Step 3: List Rows from Excel

-Add the action List rows present in a table (Excel Online Business)

-Configure the connector to point to:

-File: CUST_DATA.xlsx

-Table: CustomerTable

Step 4: Apply to Each

-Add the Apply to each control

-Use the value output from the Excel action as input

Step 5: Add a Condition (Check Birthday)

-Inside the Apply to each loop, add a condition to compare the customer’s birthday to today’s date:

-formatDateTime(items('Apply_to_each')?['Birthday'], 'MM-dd')
is equal to
formatDateTime(utcNow(), 'MM-dd')


This ensures the flow triggers only when the day and month of a customer’s birthday match the current date.

Step 6: Send the Email

-In the If Yes branch of the condition:

-Add the action Send an email (V2) (Outlook).

**Configure as follows:**

To: Dynamic content → Email

Subject:

Happy Birthday @{items('Apply_to_each')?['Customer Name']}!


Body (HTML format):

Hi @{items('Apply_to_each')?['Customer Name']},

Wishing you a very Happy Birthday!  

Best regards,  
[Your Company Name]


Note: Additional branding elements, images, or styling can be embedded using HTML if desired.

Step 7: Save and Test

Save the flow in Power Automate.

Run a manual test.

If today’s date matches a birthday in the Excel list, the corresponding customer will receive the email.

**Results**

-Emails are automatically sent each day without manual input

-Messages are accurate, consistent, and personalized

-The solution significantly reduces staff workload and improves customer experience

**Use Cases**

-Birthday and anniversary greetings

-Membership renewal notifications

-Event reminders

-Any other date driven communication

**Key Learning**

Through this project, I demonstrated how low-code automation with Power Automate can:

-Replace repetitive manual tasks

-Reduce errors in customer communication

-Deliver measurable efficiency improvements
