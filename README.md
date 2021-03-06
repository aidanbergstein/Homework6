# Homework6

1. Data cleaning: the values “IAP”, “DK” and “NA” all encode missing values. Replace all of these instances by the value NA.

> HAPPY <- replace(HAPPY, HAPPY == "IAP", NA)
> HAPPY <- replace(HAPPY, HAPPY == "DK", NA)
> HAPPY <- replace(HAPPY, HAPPY == "NA", NA)

2. Check the type of the variable and cast into the right type (factor variable for categorical variables). For age, change “89 OR OLDER” to 89 and assume the variable should be numeric.

> str(HAPPY)
'data.frame':	62466 obs. of  11 variables:
  $ HAPPY   : chr  "NOT TOO HAPPY" "NOT TOO HAPPY" "PRETTY HAPPY" "NOT TOO HAPPY" ...
$ YEAR    : int  1972 1972 1972 1972 1972 1972 1972 1972 1972 1972 ...
$ AGE     : chr  "23" "70" "48" "27" ...
$ SEX     : chr  "FEMALE" "MALE" "FEMALE" "FEMALE" ...
$ MARITAL : chr  "NEVER MARRIED" "MARRIED" "MARRIED" "MARRIED" ...
$ DEGREE  : chr  "BACHELOR" "LT HIGH SCHOOL" "HIGH SCHOOL" "BACHELOR" ...
$ FINRELA : chr  "AVERAGE" "ABOVE AVERAGE" "AVERAGE" "AVERAGE" ...
$ HEALTH  : chr  "GOOD" "FAIR" "EXCELLENT" "GOOD" ...
$ WTSSALL : num  0.445 0.889 0.889 0.889 0.889 ...
$ PARTYID : chr  "IND,NEAR DEM" "NOT STR DEMOCRAT" "INDEPENDENT" "NOT STR DEMOCRAT" ...
$ POLVIEWS: chr  NA NA NA NA ...

> HAPPY <- HAPPY %>% mutate(
  +     age = replace(age, age == "89 AND OLDER", 89),
  +     age = as.numeric(age)
  + ) %>% select(-age)

3. Bring all levels of factors into a sensible order. For marital you could e.g. order the levels according to average age.

> HAPPY <- HAPPY %>% mutate(
  +     HEALTH = factor(tolower(HEALTH)),
  +     HEALTH = factor(HEALTH, levels=c("POOR", "FAIR", "GOOD", "EXCELLENT"))
  + ) %>% select(-HEALTH)

> HAPPY <- HAPPY %>% mutate(
  +     degree = factor(tolower(DEGREE)),
  +     degree = factor(degree, levels=c("lt high school", "high school", "junior college", "bachelor", "graduate school"))
  + ) %>% select(-DEGREE)

> HAPPY <- HAPPY %>% mutate(
  +     FINRELA = factor(tolower(FINRELA)),
  +     FINRELA = factor(FINRELA, levels=c("FAR BELOW AVERAGE", "BELOW AVERAGE", "AVERAGE", "ABOVE AVERAGE", "FAR ABOVE AVERAGE"))
  + ) %>% select(-FINRELA)

> HAPPY <- HAPPY %>% mutate(
  +     happy = factor(tolower(happy)),
  +     happy = factor(happy, levels=c("not too happy", "pretty happy", "very happy"))
  + ) %>% select(-happy)

4. Investigate the relationship between happiness and two other variables in the data. Find a visualization that captures the relationship and write a paragraph to describe it.

> ggplot(data = HAPPY)  + 
  +     geom_mosaic(aes(x = product(SEX), fill=happy, weight=1)) +
  +     facet_grid(degree~HEALTH)
  
To investigate the relationship between happiness and two other variables, I formed a mosaic plot which captures the relationship between happiness and the degree and health of a person. The mosaic plot shows that for the most part, the better health a person has, the more likely that they are to be happy. Additionally, the mosaic plot makes it difficult to establish a relationship between degree and happiness, however there are a few plots on the model that can be used to prove that the better degree a person has, the more likely that they are to be happy. 


5. Each member should study a different question (choose different variables to investigate).

The question that I would like to investiagte based on this dataset is whether or not a person's health is directly related to their happiness and if there is a direct correlation between being told you are in poor health and your happiness?
