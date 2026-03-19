# San Francisco.
Data Mining course project based on the data sets from https://data.sfgov.org/ 

# Overview
I aim to use KNIME and the Association rule to analyze the San Francisco Dataset and find relationships between the Incident Time, Incident Category, and the Police District so that I can figure out what incident would most likely occur at a given time in a given location. The 3 ioncedent types I will be looking at include Larceny theft, Assault, and Vehicle theft.

# Workflow

CSV Reader
Reads my San Francisco Dataset

Column Filter
Removes all unnecessary columns so that I can just focus on what's important, being the Incident Time, Incident Category, and the Police District.

Rule-Based Row Filter
Filters out all unnecessary rows that include a missing entry for and of my columns as they are not needed

Rule Engine
Uses the Incident time column in order to separate them into a new column called Time Zones. I make all times from 00:00 -> 06:00 be considered Night, 06:00 -> 12:00 be considered Morning, 12:00 -> 18:00 be Afternoon, and any other time (18:00 -> 00:00) be Evening. This will make the time column much easier to work with when looking for patterns.

Column Filter
Incident time is no longer needed now that I used it for Time zones so I removed it here

Rule-Based Row Filter
As mentioned before, I will only be focusing on the incidents Larceny theft, Assault, and Vehicle theft, so I filter out all other incidents here.

Columns to Collection
In order to get the Association Rule Learner node to work, I needed to format all the information I would be feeding it as a single collection of items, so I used this node in order to do that and called this column Collection.

Association Rule Learner
This generates the Association rules from the Collection column from before. I used 0.01 for the minimum Support so that I wouldn't find any rare patterns, and for the minimum confidence, I used 0.5 so that the pattern is correct more than 50% of the time in order to be considered an actual rule.

Rule-Based Row Filter
It tried to create a lot of rules where the consequent was the time of day, which is not what I was looking for, so I removed all rows that had those in order to only look for the consequents involving the incident category.

Sorter
I sorted the data on the Lift and Confidence, both in descending order, so that the top of my table is the rules that are the most accurate.

Table View
Here, I simply display the final table that shows the rules we found so that we can see what type of incident would most likely occur given certain conditions.

# Results
I found that the most predictable Incident from the 3 we looked at was Larceny theft, with many different rules that have an expected outcome of this type of theft. It was especially dominant in the morning and afternoon times of day and in the Richmond area, which actually took up the 3 most accurate rules I found. Sadly, I only ended up with rules involving Larceny theft when I set my confidence to 0.5. There were a few assaults when I had it at 0.3, but I decided to keep it increased to only show more accurate rules

# Conclusion
I was able to successfully use Association Rule Learner in order to find patterns within the San Francisco Dataset that could help someone understand their biggest threats to look out for, given what time of day it is or where they are located. For example, if they were in the Richmond area and it was either morning or in the afternoon, there is a high possibility of larceny theft taking place, so they should be on the lookout. While I am disappointed that I didn't end up with any rules regarding Assault or Vehicle theft, I guess it could be considered a good thing because there's no rule that is so accurate to predict them, therefore they are not nearly as big of an issue as I thought they would be.


