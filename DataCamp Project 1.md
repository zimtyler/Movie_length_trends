# Investigating Netflix Movies and Gueest Stars in The Office
```
# Create the years and durations lists
years = [2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020]
durations = [103, 101, 99, 100, 100, 95, 95, 96, 93, 90]

# Create a dictionary with the two lists
movie_dict = {'years': years, 'durations': durations}
# Print the dictionary
print(movie_dict)

```
* ***dict(zip(list1, list2)) creates a dictionary from two lists using their indexes to pair them***
```
# Import pandas under its usual alias
import pandas as pd

# Create a DataFrame from the dictionary
durations_df = pd.DataFrame(movie_dict)
# Print the DataFrame
print(durations_df)
```
```
# Import matplotlib.pyplot under its usual alias and create a figure
import matplotlib.pyplot as plt
fig = plt.figure()

# Draw a line plot of release_years and durations
plt.plot(durations_df['years'], durations_df['durations'])


# Create a title
plt.title("Netflix Movie Durations 2011-2020")

# Show the plot
plt.show()
```
* If we need to create a plot with bottom coordinates set to 0, 0, use 
plt.xlim([0, x_max])
```
x_max = max(col_1)
y_max = max(col_2)
plt.xlim([0, x_max])
plt.ylim([0, y_max])
```

```
# Read in the CSV as a DataFrame
netflix_df = pd.read_csv("datasets/netflix_data.csv")

# Print the first five rows of the DataFrame
print(netflix_df[0:5])

# Subset the DataFrame for type "Movie"
netflix_df_movies_only = netflix_df[netflix_df['type'] == 'Movie']

# Select only the columns of interest
netflix_movies_col_subset = netflix_df_movies_only[['title', 'country', 'genre', 'release_year', 'duration']]

# Print the first five rows of the new DataFrame
print(netflix_movies_col_subset[0:5])```
* Column can be used as df index
* The filtered df column can then be used as a filter to select only those values where 'type' = 'Movie'

# Create a figure and increase the figure size
fig = plt.figure(figsize=(12,8))

# Create a scatter plot of duration versus year
plt.scatter(netflix_movies_col_subset['release_year'], netflix_movies_col_subset['duration'])

# Create a title
plt.title('Movie Duration by Year of Release')

# Show the plot
plt.show()

# Filter for durations shorter than 60 minutes
short_movies = netflix_movies_col_subset[netflix_movies_col_subset['duration'] < 60]

# Print the first 20 rows of short_movies
print(short_movies[0:20])

# Define an empty list
colors = []

# Iterate over rows of netflix_movies_col_subset
for x in netflix_movies_col_subset['genre'] :
    if x == 'Children' :
        colors.append('red')
    elif x == 'Stand-Up' :
        colors.append('blue')
    elif x == 'Documentaries' :
        colors.append('green')
    else:
        colors.append('black')
        
# Inspect the first 10 values in your list        
print(colors[0:11])
```
# Create a figure and increase the figure size
fig = plt.figure(figsize=(12,8))

# Create a scatter plot of duration versus year
plt.scatter(netflix_movies_col_subset['release_year'], netflix_movies_col_subset['duration'])

# Create a title
plt.title('Movie Duration by Year of Release')

# Show the plot
plt.show()
```
* Way too much data, but we clearly see that while there are more movies made as time goes on, there are also a lot of shorter duration movies popping up. Is this a product of simply the increase in the # made, or is there a trend
```
# Filter for durations shorter than 60 minutes
short_movies = netflix_movies_col_subset[netflix_movies_col_subset['duration'] < 60]

# Print the first 20 rows of short_movies
pd.DataFrame.head(short_movies, 20)

# Define an empty list
colors = []

# Iterate over rows of netflix_movies_col_subset
for x in netflix_movies_col_subset['genre'] :
    if x == 'Children' :
        colors.append('red')
    elif x == 'Stand-Up' :
        colors.append('blue')
    elif x == 'Documentaries' :
        colors.append('green')
    else:
        colors.append('black')
        
# Inspect the first 10 values in your list        
print(colors[0:11])

# Set the figure style and initalize a new figure
plt.style.use('fivethirtyeight')
fig = plt.figure(figsize=(12,8))

# Create a scatter plot of duration versus release_year
plt.scatter(netflix_movies_col_subset['release_year'], netflix_movies_col_subset['duration'], color = colors)

# Create a title and axis labels
plt.title('Movie duration by year of release')
plt.xlabel('Release year')
plt.ylabel('Duration (min)')

# Show the plot
plt.show()
```
