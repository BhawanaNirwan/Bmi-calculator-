BMI Calculator with History and Trend Analysis:
This project is a BMI (Body Mass Index) Calculator application developed using Python and Tkinter. It allows users to calculate their BMI, save the data, view their BMI history, and analyze trends over time. The data is saved in a CSV file for persistence.

Features:
BMI Calculation: Users can input their name, weight (in kg), and height (in meters) to calculate their BMI.
Data Persistence: Calculated BMI data is saved in a bmi_data.csv file.
View History: Users can view a history of all BMI calculations saved in the CSV file.
Trend Analysis: Visualize BMI trends over time with a line chart using Matplotlib.

Requirements:
Python 3.x
Required Python libraries:
tkinter (standard library)
pandas
matplotlib
numpy

How to Run:
Clone the repository or download the script.
Make sure you have Python 3.x installed on your system.
Install the required libraries by running:
pip install pandas matplotlib

Run the script:
python bmi_calculator.py

Usage:
Calculate BMI:
Enter your name, weight (in kg), and height (in meters).
Click the Calculate BMI button.
The calculated BMI will be displayed, and the data will be saved in bmi_data.csv.
View History:
Click the View History button to open a new window displaying all saved BMI records.
BMI Trend:
Click the BMI Trend button to view a line chart of BMI values over time.
File Structure
bmi_calculator.py: The main script containing the application code.
bmi_data.csv: The file where all BMI calculation records are saved. This file is created automatically if it doesn't exist.
Code Overview
CSV File Management:

The script checks if the bmi_data.csv file exists. If not, it creates one with the appropriate columns.
BMI Calculation:

BMI is calculated using the formula: BMI = Weight / (Height^2).
Data is saved along with the current date.
History Display:

A new window opens displaying all saved BMI data in a text widget.
Trend Analysis:

The script uses Matplotlib to plot BMI values against dates.
Example Output
BMI Calculation:

Input: Weight = 70 kg, Height = 1.75 m
Output: BMI = 22.86
History:

Name       Weight    Height     BMI     Date
John    70        1.75       22.86   2025-01-06
Trend Chart: A line graph showing BMI changes over time.

Notes
Ensure valid inputs for weight and height (positive numbers only).
The application uses the current system date for each BMI record.
