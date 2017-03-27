# We want to implement the specific SQL query below by using the ChicagoCubs dataset in python 3.5.

{Select Sum(Losses) From [ChicagoCubs_1874-2016]
Group BY Season_Year
Having Losses < 30}


First, we import the csv dataset and we define the 'groupby_sum' function with parameters group_column and having.
Then we create grouped_by data variable to store each sum of the value in the column. In our case, it is "Losses" column.
In our dataset, SELECT SUM(Losses) woule resturn the same values because we only have one distinct losses value in each row.
After assign the sum to the grouped_by variable, we created 'output' set, 'grouped' list, and 'idx' list.

The 'output' set will append the values of the "Losses" cloumn that is less than 30.
The 'idx' list will store the index of the row which the "Losses" clomun has value less than 30.
The 'grouped' list will store the Season_Year and returns the GroupBy(Season_Year) that has "Losses" values < 30.



------------------------------------------------------------------
#Select Sum(Losses) From [ChicagoCubs_1874-2016]
#Group BY Season_Year
#Having Losses < 30

import pandas as pd  # import the pandas api to read the csv data
from IPython.display import display # Allows the use of display() for DataFrames

#read the csv file
in_file = 'Chicago Cubs 1874-2016.csv'
data = pd.read_csv(in_file)
#Display the data set
#display(data)

# Assigned the data and drop the columns that we are not going to use, except Season_Year and Losses.
fixed_data = data.drop(["Team","Wins", "Place", "GB","Attendance","PCT"], axis=1)

# Create a function called group_column. The group_column and having parameters must be strings.
def groupby_sum(group_column, having):
    
    # Group By Season_Year by the Sum of the Losses.
    # In our dataset the SUM(Losses) will be equal 
    # to the original Losses values because the Season_Year are all distinct.
    grouped_by = fixed_data.groupby([group_column]).sum()
    
    # Create output variable to store the set of the values that Losses < 30.
    output = set()
    
    # Create grouped list to return the list of the result.
    # Create idx list to keep track the index of the row that has Losses value < 30.
    grouped = []
    idx = []
    
    # Loop through the grouped_by variable 
    # and add the Losses values to 'output' set, if the value is less than 30.
    for i in grouped_by[having]:
        if i < 30:
            output.add(i)
            
    # Loop through the 'output' set
    for j in output:
        # If the value of the 'output' is equal to the value of the 'Losses' columns,
        # then store the respective index number of the row to 'idx' list.
        idx = fixed_data[fixed_data[having] == j].index.tolist()
        
        # Append the 'grouped' list with the matching of the row index
        # and the SUM(Losses) values that is grouped by the Season_Year.
        grouped.append(fixed_data.loc[idx,having])
    
    # Return the final result
    return grouped
    
