# Import the required modules
import pandas as pd
from pathlib import Path

# Create a variable to store the path of the csv file
file = Path("Resources/election_data.csv")

# Create a data frame using the read_csv function of pandas
election_data_df = pd.read_csv(file)
election_data_df.head()

# Calculate the total number of Votes
Total_votes = len(election_data_df)
print(Total_votes)

# Calculate the unique values of the Candidate column
candidate_list = election_data_df["Candidate"].unique()
print(candidate_list)

# Calculate the votes each candidate received
votes = election_data_df.groupby("Candidate")["Ballot ID"].count()
print(votes)

# Calculate the percentage of votes each Candidate recieved
Percentage = (votes/Total_votes)*100
Percentage

# Calculate the winner
winner = votes.idxmax()
winner

# Export the results into a txt file
with open("voting_analysis.txt", "w") as file:
    file.write("Election Results\n")
    file.write("-------------------------\n")
    file.write(f"Total Votes: {Total_votes}\n")
    file.write("-------------------------\n")
    for candidate in candidate_list:
       file.write(f"{candidate}: {Percentage[candidate]:.3f}% ({votes[candidate]})\n")
    file.write("-------------------------\n")
    file.write(f"Winner: {winner}\n")
    file.write("-------------------------\n")

print("Analysis results have been saved to 'voting_analysis.txt'.")
