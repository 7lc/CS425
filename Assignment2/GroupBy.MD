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
The 'grouped' list will store the Season_Year and returns the Season_Year that has "Losses" values < 30.


// Group_column and having must be string.

def groupby_sum(group_column, having):
    grouped_by = fixed_data.groupby([group_column]).sum()
    output = set()
    grouped = []
    idx = []
    for i in grouped_by[having]:
        if i < 30:
            output.add(i)
    print(output)
    
    for j in output:
        idx = fixed_data[fixed_data[having] == j].index.tolist()
        grouped.append(fixed_data.loc[idx,group_column])
    
    return grouped
