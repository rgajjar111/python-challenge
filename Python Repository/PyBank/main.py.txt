# Import the required modules
import pandas as pd
from pathlib import Path

# Create a variable to store the path of the csv file
file = Path("Resources/budget.csv")

# Create a data frame using the read_csv function of pandas
Budget_df=pd.read_csv(file)
Budget_df.head()

# Calculate the total number of months
total_months = len(Budget_df)
print(total_months)

# Calculate the net total amount of "Profit/Losses"
total_amt = Budget_df["Profit/Losses"].sum()
print(total_amt)

# Calculate the changes in "Profit/Losses" over the entire period
Change_df = Budget_df["Profit/Losses"].diff()

#Calculate the average of changes in "Profit/Losses"
average_change_df = Change_df.mean()
print(average_change_df)

# Storing the index of the max value in the Change_df
greatest_increase_index = Change_df.idxmax()

# Using the index to find the corresponding date in the Budget_df
greatest_increase_date = Budget_df.loc[greatest_increase_index, "Date"]

# Calculating the greatest increase value
greatest_increase_amount = Change_df.max()

#Printing the greatest increase in profits (date and amount) over the entire period
print(f"Greatest Increase in Profits: {greatest_increase_date} {greatest_increase_amount}")

# Storing the index of the min value in the Change_df
greatest_decrease_index = Change_df.idxmin()

# Using the index to find the corresponding date in the Budget_df
greatest_decrease_date = Budget_df.loc[greatest_decrease_index, "Date"]

# Calculating the greatest decrease value
greatest_decrease_amount = Change_df.min()

#Printing the greatest decrease in profits (date and amount) over the entire period
print(f"Greatest Decrease in Profits: {greatest_decrease_date} {greatest_decrease_amount}")

#Write the output into a txt file
with open("financial_analysis.txt", "w") as file:
    file.write("Financial Analysis\n")
    file.write("----------------------------\n")
    file.write(f"Total Months: {total_months}\n")
    file.write(f"Total: ${total_amt:.2f}\n")
    file.write(f"Average Change: ${average_change_df:.2f}\n")
    file.write(f"Greatest Increase in Profits: {greatest_increase_date} (${greatest_increase_amount:.2f})\n")
    file.write(f"Greatest Decrease in Profits: {greatest_decrease_date} (${greatest_decrease_amount:.2f})\n")

print("Analysis results have been saved to 'financial_analysis.txt'.")