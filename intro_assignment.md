Intro Assignment
================

The goal of this assignment is to get you warmed up with git, GitHub,
markdown, and R. The first few seminars will cover all you need to know
for completing this practice assignment.

Note that this practice assignment, just like the later Analysis
Assignment, will need to be done in Rmarkdown (`.Rmd`) because it
requires R code. You can start with the `.Rmd` version of this file, and
fill it in where necessary. Note that Question 1 asks you to add an
additional file.

Check out the [assignment
tips](https://stat540-ubc.github.io/submission_guide.html#general-tips-for-working-on-the-assignments)
to make sure your report meets our standards. It’s important to write up
organized reports that are clear and easy to follow, so that your
collaborators and the future you can understand what you are doing. To
ensure you earn full marks on this and future assignments, be sure to
address the following points:

- Well-formatted markdown (use of headings, subheadings, and numbering
  that makes sense)
- Codes are commented when needed and output is interpreted
- Properly labeled graphs
- No broken code
- Rmarkdown is properly knitted and the `.md` is rendered on Github
  (including any figures/images)

Be sure to commit, push your completed assignment, and submit the
repository URL on Canvas before the deadline. Anything submitted or
modified after the deadline will not be marked.

## QUESTION 1: Create a README in your repo (1pt)

Once you have accepted this assignment through the Canvas invite link
and have a repository set up (in the format of
`STAT540-UBC-2023/intro-assignment-yourgithubID`), you can start
personalizing it by adding a README.md file. This would help people who
visit your repository understand who you are and what your repository is
about.

Please be sure that your markdown is properly formatted. See this
[markdown
reference](https://guides.github.com/features/mastering-markdown/) from
GitHub if you need help getting started.

Add some information to this README.md file to introduce yourself to the
teaching team. Some things you may wish to include:

- Your name, your program
- Links to other profiles (e.g. Mastodon, a personal website, other
  relevant links, etc)
- What you hope to achieve in this course
- What this repository is for (example: “This repository contains the
  intro assignment for STAT540”)
- Anything else that you want. You can add images or emoji, too!

## QUESTION 2: Data inspection with R (2pt)

When answering the following questions, please always “sandwich” your R
code with some text. Ensure fluency by avoiding inserting R code or
outputs without any explanation. For example, if the question asks you
what is `x + y` given `x=1` and `y=2`, you can answer it like this:

------------------------------------------------------------------------

Now we want to find the sum of x and y.

``` r
x <- 1  # Note how I assign them to variables instead of just priting 1+2
y <- 2 
z <- x + y
z # By doing this, I can print out the output of z. Alternately, you can also do (z <- x+y). 
```

    ## [1] 3

Conclusion: we found that `x + y` is 3 **(notice here I’m using inline R
code to print the value of `z`)**.

------------------------------------------------------------------------

If you are looking at the `.Rmd` of this file (the Rmarkdown that
creates the markdown `.md` file), you’ll see that I have used inline R
code in the previous line to refer to the variable `z` instead of
directly typing `3`. This is because if we ever need to change the
values of `x` and `y,` we could possibly forget to update where we typed
in `3` as well. You can imagine that if you have to change the initial
inputs of a long statistical reports, all your numbers in the rest of
the report will change. You don’t want to have to look through every
sentence to make sure that your report is still up-to-date.

By using variables and inline R code, I can change the value of `x`
and/or `y`, and rest assured that when I re-knit my Rmarkdown, my
conclusion statement will be updated.

There are some [data
sets](https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/00Index.html)
in base R for you to play around with. We will explore the Titanic
dataset. You can view it by typing `Titanic`. Just like with functions,
you can use the question mark `?Titanic` to see more information about
the dataset.

Answer the following questions by subsetting, printing out the result or
by graphing.

### 2.1 Passenger breakdown (1pt)

- Convert the array into a data frame by using `data.frame()` function.
- How many children were on Titanic?
- How many adults were on Titanic?
- Were there more female adult or male adult passengers?

Find the answers these questions by adding code to the code block below.

#### Making the data frame

``` r
titanic_df = data.frame(Titanic) 
```

The function data.frame converts the data found in the Titanic file into
a nicely structured table.

#### Total number of children and adults

``` r
children_total = sum(titanic_df$Freq[titanic_df$Age == "Child"])
adults_total = sum(titanic_df$Freq[titanic_df$Age == "Adult"])
```

The total number of children on Titanic was found by summing the number
in the Freq column if they are categorized as Child in the Age column.
The same was done to find the number of adults, by switching from Child
to Adult in the Age column. Number of children: 109 Number of adults:
2092

#### Total number of men and women

``` r
women_total = sum(titanic_df$Freq[titanic_df$Age == "Adult" & titanic_df$Sex == "Female"])
men_total = sum(titanic_df$Freq[titanic_df$Age == "Adult" & titanic_df$Sex == "Male"])
```

The total number of male and female adults was found by summing up the
number of adults of female and male sex, respectively. It was found that
there were more male than female adults on Titanic. 1667 men compared to
425 women.

### 2.2 Survival (1pt)

Using the same data frame, examine the survival rates.

- Did the children had better survival rate than the adults?
- Order the classes of passengers (Crew, 1st, 2nd, and 3rd) by survival
  rate **worst to best**.

Find the answers these questions by adding code to the code block below.

#### Survival rates for children and adults

``` r
#survival rates for children and adults
child_survival = sum(titanic_df$Freq[titanic_df$Age == "Child" & titanic_df$Survived == "Yes"])
adult_survival = sum(titanic_df$Freq[titanic_df$Age == "Adult" & titanic_df$Survived == "Yes"])

survivalrate_children = child_survival/children_total
survivalrate_adults = adult_survival/adults_total
```

child_survival sums up the number of children that survived and then the
ratio of child survival was found by dividing by the total number of
children. The same was done for adults. The survival rate of children
was then found to be 0.5229358, and for adults it was 0.3126195. So yes,
the children had higher survival rate than the adults.

#### Survival rates for the different classes

``` r
#Survival rate for crew
crew_survival = sum(titanic_df$Freq[titanic_df$Class == "Crew" & titanic_df$Survived == "Yes"])
crew_total = sum(titanic_df$Freq[titanic_df$Class == "Crew"])
survivalrate_crew = crew_survival/crew_total

#Survival rate for 1st class
first_survival = sum(titanic_df$Freq[titanic_df$Class == "1st" & titanic_df$Survived == "Yes"])
first_total = sum(titanic_df$Freq[titanic_df$Class == "1st"])
survivalrate_1st = first_survival/first_total

#Survival rate for 2nd class
second_survival = sum(titanic_df$Freq[titanic_df$Class == "2nd" & titanic_df$Survived == "Yes"])
second_total = sum(titanic_df$Freq[titanic_df$Class == "2nd"])
survivalrate_2nd = second_survival/second_total

#Survival rate for 3rd class
third_survival = sum(titanic_df$Freq[titanic_df$Class == "3rd" & titanic_df$Survived == "Yes"])
third_total = sum(titanic_df$Freq[titanic_df$Class == "3rd"])
survivalrate_3rd = third_survival/third_total
```

The survival rates were forund using the same approach as in the
previous task. The order of survival rate from worst to best: Crew
(0.239548) - 3rd Class (0.2521246) - 2nd Class (0.4140351) - 1st Class
(0.6246154)

## 3. Data visualization (2pt)

Here you’ll practice reading data from a text file and do some graphing.
The file
[“PaintedTurtles.txt”](https://raw.githubusercontent.com/STAT540-UBC/intro-assignment/main/PaintedTurtles.txt)
contains data on several variables for a sample of Painted turtles.

- Create a figure to visualize at least 3 variables from this dataset
  (choose whatever graph you’d like!)
- Explain how your graph is informative: what does it tell you about the
  relationship between the variables? Also explain why you choose to
  present the data in this way.

Add code to the code block below to complete these tasks.

#### Plot of length vs. width of turtles, including the height (size of points) and sex (colour) variables

``` r
library(ggplot2)
turtle_df = read.table("https://raw.githubusercontent.com/STAT540-UBC/intro-assignment/main/PaintedTurtles.txt", header = TRUE, sep = "\t")

ggplot(data = turtle_df, aes(x = length, y = width, color = sex, size = height)) + 
    geom_point() +
    xlab('Length') + ylab('Width') +
    scale_color_manual(
      name = 'Sex',
      labels = c('Male', 'Female'),
      values = c('coral2', 'dodgerblue')
    )
```

![](intro_assignment_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

The graph shows the length on the x-axis and the width on the y-axis,
and we can see that there is a linear relationship between these two
variables. The same seems to be true for the height, as the points get
bigger as the turtler are wider and longer (which is what we would
expect). The sex was also included, and it is evident that the male
turtles are the biggest ones, while the female ones are smaller. I chose
to present the data in this way because it clearly pictures the
relationships between different size variables, as well as the sex
differences.
