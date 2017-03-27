# We want to implement the specific SQL query below by using the ChicagoCubs dataset in python 3.5.

{Select Sum(Losses) From [ChicagoCubs_1874-2016]
Group BY Season_Year
Having Losses < 30}




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
