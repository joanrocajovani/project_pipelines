# Project Movies
## Introduction:
For this project, I took a csv dataset with the 1000 best rated movies in IMBD. Then, using web scrapping I got a list of all movies awarded with Best Picture by the Academy Awards (Oscars).
The main idea was to find who makes more money, the movies awarded by the Academy or the movies rated by the people.

### Web Scrapping:
I found a list on the IMBD website containing all the Best Picture winning movies. I scrapped the website and with some fixing I obtained a full list.
From there, I created a new column which was true if the movie was in the list of Oscar winners.
Then, I filled all the remaining values with false, so I finally got a column telling me if the movie had won the oscar or not.

<img src="images/screenshots/oscar_column.png" width="75" height="250">>

### Cleaning:
Initially the data frame contained these columns:
- Poster_Link - Link of the poster that imdb using
- Series_Title = Name of the movie
- Released_Year - Year at which that movie released
- Certificate - Certificate earned by that movie
- Runtime - Total runtime of the movie
- Genre - Genre of the movie
- IMDB_Rating - Rating of the movie at IMDB site
- Overview - mini story/ summary
- Meta_score - Score earned by the movie
- Director - Name of the Director
- Star1,Star2,Star3,Star4 - Name of the Stars
- Noofvotes - Total number of votes
- Gross - Money earned by that movie

From those, I didn't need the Poster Link, the Certificate, the Overview and the Meta Score, so I dropped them.

__Columns Cast Fix:__
For the cast I had 4 columns containing one actor each. Even though I didn't analyze the actors I grouped them into one column with a list.

__Released Year Fix:__
The years were strings and for converting them into integers I had to manually type the release year for one movie which year was "PG". The movie was Apollo 13 which was released in 1995. Then I turned the column into integers.

__Gross Money Made Fix:__
This column was a numeric string with thousand comma separators, so first I used the Regex Code: [\&,)] to eliminate the commas and then turned into an integer.
Then I divided all the elements by 1.000.000 to show it in millions since it was better visually and finally I wanted to adjust that for inflation.
To do it I found that the average inflation rate for the last 100 years was 3.8% so I found the Present Value of the Money Made in the past with the following formula: *Amount * (1+0.038)**(2022-Released Year)*.
With this, I got the inflation adjusted money made by each film.

__Column Genre Fix:__
For this one I deleted " min" with the regex code: '[^0-9]'. And them converted the column into integers too.


## Visualiztion:
### IMDB Rating Analysis:
<img src="images/screenshots/RatingHistogram.png" width="500" height="300">
We can see that the higher the rating, the less movies there are, as it is normal, since it is harder to get.
It should be pointed out that this is just the 1000 movies with highest grade so the distribution is partial and focused on the higher end.

Let's take a closer look at the distribution:
<img src="images/screenshots/RatingBoxPlot.png" width="500" height="300">
<img src="images/screenshots/RatingDescriptive.png" width="250" height="200">

We can see that 50% of the top 1000 movies have a rating between 7.7 and 8.1, which is a tight inverval.

Finally, I wanted to check if there is a linear relationship between the rating and the number of votes:
<img src="images/screenshots/ratingvsvotes.png" width="500" height="300">

We can appreciate how the best rated films have on average a higher number of votes. The reason for that is that these movies are legendary and so many people have seen them.

### Inflation adjusted gross money made analysis:
Lets take a look at the histogram:
<img src="images/screenshots/moneyhistogram.png" width="500" height="300">
We can see that the vast majority of movies have made less than $1B. But let's quantify that with more detail.
<img src="images/screenshots/moneyboxplot.png" width="500" height="300">
<img src="images/screenshots/moneydescribe.png" width="250" height="200">

Just 250 movies have a PV of the money they made higher than $226B. For the boxplot I eliminated outliers because you can see the max is a movie with a PV of $4.3B, but is a movie made in 1930.

### Top 1000 movies made by year:
Now let's check the distribution of released year for the top 1000 movies:
<img src="images/screenshots/yearhistogram.png" width="500" height="300">
We can see that there are much more "new" movies than "old" movies in the Top 1000. I believe that the reason for that is that the voters in IMBD are "young" people and today's movies are more the taste of younger generations. I don't imagine my grandfather voting and if I told them that today's movies are better than his time's he would absolutely disagree.

### Which director has been more succesful?
To perform this analysis I grouped by directors and checked 3 things:
- How many of the top 1000 movies are theirs.
- How many best picture awards do they have.
- How much money have their films made.

<img src="images/screenshots/directorscount.png" width="500" height="300">
We can see that Alfred Hitchcook leads with 14 movies followed by Steven Spilberg, Hayao Miyazaki and Martin Scorcese.
My personal favorite, Quentin Tarantino has 8 movies in the Top 1000, which is amazing since he only has 10 movies, so 80% for him.

<img src="images/screenshots/oscardirectors.png" width="500" height="300">
This graph show that no director has more than 2 movies awarded with Best Picture by the Academy.

<img src="images/screenshots/amountdirectors.png" width="500" height="300">
Steven Spielberg leads with $2.5B generated, followed by Anthony Russo and Christopher Nolan.

## Main Hypothesis: Which movies generate more money on average, Oscar Awarded or Best Rated?
To perform this analysis, first I dropped a movie that had an inflation adj amount of over $4B because it would distort the results.
Since there are now 56 Oscar Winning movies among the top 1000, I chose on one hand the top 56 rated and on the other hand the 56 Oscar winners. And the Results are the following:
### Top Rated Movies:
<img src="images/screenshots/topmovieshistogram.png" width="500" height="300">
<img src="images/screenshots/topmoviesdescriptive.png" width="250" height="200">

### Oscar Winners:
<img src="images/screenshots/oscarhist.png" width="500" height="300">
<img src="images/screenshots/oscardescriptive.png" width="250" height="200">

### Conclusion:
We can see that the Oscar winning movies have a higher average of inflation adjusted amount made.
It is interesting to see that the median is almost exactly the same, and that top movies have a higher 75% than the Oscar Winners.
So we can't take sound conclusions about these data. So winning an Oscar is as good as being extremely well rated by the audience in terms of the amount that the money can make.