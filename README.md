# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file.
2. Mail server access for Notification.
3. PDF report generator.
4. Access to write/store the PDF report in server.


### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Computation of minimum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No 			| We do not test the PDF converter
Counting the breaches       | Yes	 		| This is part of the software being developed
Detecting trends            | Yes			| This is part of the software being developed
Notification utility        | No			| We do not test the End mail notification

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

Positive Flow Test Cases:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings.
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data.
3. Write "Breach counts" to the PDF when the input cross the threshold.
4. check whether Breach not counted when the input < threshold(Ensure threshold Boundary).
5. check whether Breach is counted when the input > threshold(Ensure threshold Boundary).
6. Write "Trends" to the PDF when the reading was continuously increasing for 30 minutes
7. Check the PDF report of the analysis is storing in every week.
8. Check whether Notification is sent when a new report is available.
10. Check Notification message contents are proper/correct.

Negative Flow Test Cases:

1. Write "valid input" to the PDF when the csv contain expected data.
2. check whether Breach not counted when the input < threshold(Ensure threshold Boundary).
3. Don't Write "Trends" to the PDF when the reading was continuously increasing for below 30 minutes.
4. Check the PDF report of the analysis is generating/storing on other daysPDF report count per week == 1).
5. Check whether Notification is not sent when a new report is not available.


### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | PDF Generated| Connect mail server         | Mock the Notification function
Report inaccessible server | PDF file 	  | Report storage server       | Fake the server store
Find minimum and maximum   | csv data	  | Min and Max stored entires  | None - it's a pure function
Detect trend               | csv data	  | Trend               		| None - it's a pure function
Write to PDF               | internal data-structure| PDF file			| Mock the PDF converter function
