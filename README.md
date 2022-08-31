# Election_Analysis

## Project Overview
This project aimed to audit election results for a recent local congressional election in Colorado for the Colorado Board of Elections.

1. Calculate total number of votes cast
2. Get a complete list of candidates who receeived votes
3. Calculate the total number of votes each candidate received.
4. Calculate the percentage of votes for each candidate.
5. Determine winning candidate based on popular vote

## Resources
- Data source: election_results.csv
- Software: Python 3.6.1, Visual Studio Code, 1.38.1

## Summary
The analysis of the election show that:
- There were 369,711 votes cast
- The candidates were:
  -  Charles Casper
  -  Diana DeGette
  -  Raymon Anthony Doane
- The candidate results were:
  -  Charles Casper: 23.0%, 85,213 votes
  -  Diana DeGette: 73.8%, 272,892 votes
  -  Raymon Anthony Doane: 3.1%, 11,606 votes
-  The winner of the election was:
  - Diana DeGette, who received 73.8% of the total vote and 272,892 votes.

![election_Results](https://user-images.githubusercontent.com/110862583/187733347-4739c328-7d05-4909-8c61-175ff9e6e1ca.png)
(The image above displays the election results derived from running the code for the analysis.)


## Challenge Overview
For this challenge, I utilized VBS in order to run a code that would further analyze the data from election_results.csv in order to show which candidate and county won the local congressional election.

In order to calaculate the total number of votes for this election, I used the following code:
```
# Initialize a total vote counter.
total_votes = 0

# Candidate Options and candidate votes.
candidate_options = []
candidate_votes = {}

# 1: Create a county list and county votes dictionary.
county_list = []
county_votes = {}

# Track the winning candidate, vote count and percentage
winning_candidate = ""
winning_count = 0
winning_percentage = 0

# 2: Track the largest county and county voter turnout.
largest_county_turnout = ""
largest_turnout_count = 0
largest_percentage = 0

# Read the csv and convert it into a list of dictionaries
with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    # Read the header
    header = next(reader)

    # For each row in the CSV file.
    for row in reader:

        # Add to the total vote count
        total_votes = total_votes + 1

        # Get the candidate name from each row.
        candidate_name = row[2]

        # 3: Extract the county name from each row.
        county_name = row[1]


        # If the candidate does not match any existing candidate add it to
        # the candidate list
        if candidate_name not in candidate_options:

            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)

            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0

        # Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1

        # 4a: Write an if statement that checks that the
        # county does not match any existing county in the county list.
        if county_name not in county_list:
        

            # 4b: Add the existing county to the list of counties.
            county_list.append(county_name)


            # 4c: Begin tracking the county's vote count.
            county_votes[county_name] = 0



        # 5: Add a vote to that county's vote count.
        county_votes[county_name] += 1
 ```
 
From there, I used this code in order to find the number of votes for each county, as well as the percentage of votes for each county:
```
 # 6a: Write a for loop to get the county from the county dictionary.
    for county_name in county_list:

        # 6b: Retrieve the county vote count.
        county_vote = county_votes.get(county_name)

        # 6c: Calculate the percentage of votes for the county.
        county_vote_percentage = (float(county_vote) / float(total_votes)) * 100



         # 6d: Print the county results to the terminal.
        county_results = (
            f"{county_name}: {county_vote:,} {county_vote_percentage:.1f}\n")
        print(county_results, end="")

         # 6e: Save the county votes to a text file.
        txt_file.write(county_results)


         # 6f: Write an if statement to determine the winning county and get its vote count.
        if (county_vote > largest_turnout_count) and (
            county_vote_percentage > largest_percentage
         ):
            #True
            largest_turnout_count = county_vote
            largest_county_turnout = county_name
            largest_percentage = county_vote_percentage
```

Finally, in order to display the candidate with the largest number of votes, the following code was used:
```
# 7: Print the county with the largest turnout to the terminal.
    winning_turnout = (
            f"\nLargest County Turnout\n"
            f"----------------------\n"
            f"Largest County Turnout: {largest_turnout_count:,}\n")
    print(winning_turnout, end="")


    # 8: Save the county with the largest turnout to a text file.
    txt_file.write(winning_turnout)


    # Save the final candidate vote count to the text file.
    for candidate_name in candidate_votes:

        # Retrieve vote count and percentage
        votes = candidate_votes.get(candidate_name)
        vote_percentage = float(votes) / float(total_votes) * 100
        candidate_results = (
            f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

        # Print each candidate's voter count and percentage to the
        # terminal.
        print(candidate_results)
        #  Save the candidate results to our text file.
        txt_file.write(candidate_results)

        # Determine winning vote count, winning percentage, and candidate.
        if (votes > winning_count) and (vote_percentage > winning_percentage):
            winning_count = votes
            winning_candidate = candidate_name
            winning_percentage = vote_percentage

    # Print the winning candidate (to terminal)
    winning_candidate_summary = (
        f"-------------------------\n"
        f"Winner: {winning_candidate}\n"
        f"Winning Vote Count: {winning_count:,}\n"
        f"Winning Percentage: {winning_percentage:.1f}%\n"
        f"-------------------------\n")
    print(winning_candidate_summary)
 ```
 
 ## Summary
 
 This code allowed for an efficient method to anaylze and produce specific data from a large dataset. Thus, one may opt to use this code for larger elections, as users may narrow down the code even further in order to produce specific details, such as political parties, towns, districts, etc. For instance, if one was presented with a dataset outlining political parties, we may add further variables, such as "political_party_vote" and further implement that into our If statement : 
 ```
 if (political_party_vote > largest_political_count) and (
            political_party_percentage > largest_political_percentage
         ):
            #True
            largest_political_count = political_party_vote
            largest_political_count = party_name
            largest_political_percentage = political_party_percentage
  ```
  
  Additionally, this code pulls specifically from the indicated "Resources" folder, but--similar to the difference in my code--users may change the source of the data listed in
  ```
  # Add a variable to load a file from a path.
file_to_load = os.path.join("..", "election-analysis", "election_results.csv")
# Add a variable to save the file to a path.
file_to_save = os.path.join("..","election-analysis", "election_analysis.txt")
```
to fit the origin folder in order to pul lthe data from the intended dataset.
