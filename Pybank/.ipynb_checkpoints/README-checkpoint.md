# Python-homework
# Import Dependencies
from pathlib import Path
import csv

# Set the file path
csvpath_input = Path('budget_data.csv')
csvpath_output = Path('budget_analysis.txt')

# Defining list of activities
total_months  = 1
total_net = 0
month_of_change = []
net_change_list = []

greatest_increase = ['', 0]
greatest_decrease = ['', 9999999999999999999]

with open(csvpath_input, 'r') as csvfile:
    reader = csv.reader(csvfile)
    header = next(reader)
    first_row = next(reader)
    prev_net = int(first_row[1])
    for row in reader:
        total_net = total_net + int(row[1])
        total_months = total_months + 1
        net_change = int(row[1]) - prev_net
        prev_net = int(row[1])
        net_change_list = net_change_list + [net_change]
        month_of_change = month_of_change + [row[0]]
        if net_change > greatest_increase[1]:
           greatest_increase[0] = row[0]
           greatest_increase[1] = net_change
        if net_change < greatest_decrease[1]:
           greatest_decrease[0] = row[0]
           greatest_decrease[1] = net_change
           
output = (
   f"\n Financial Analysis \n"
   f"------------------------------\n"
   f"Total months: {total_months}\n"
   f"Total: ${total_net}\n"
   f"Average  Change: ${average_change:.2f}\n"
   f"Greatest Increase in Profits: {greatest_increase[0]} (${greatest_increase[1]})\n"
   f"Greatest Decrease in Profits: {greatest_decrease[0]} (${greatest_decrease[1]})\n")
   
   Financial Analysis 
------------------------------
Total months: 86
Total: $37514694
Average  Change: $-2315.12
Greatest Increase in Profits: Feb-12 ($1926159)
Greatest Decrease in Profits: Sep-13 ($-2196167)