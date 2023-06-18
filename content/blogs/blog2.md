---
categories:
- ""
- ""
date: "2017-10-31T22:26:09-05:00"
description: Analysis of Credit Card Fraud
draft: false
image: creditfraud.jpg
keywords: ""
slug: magna
title: Credit Fraud Analysis
---

Exploring credit card fraud
•	In this dataset, how likely are fraudulent transactions? Generate a table that summarizes the number and frequency of fraudulent transactions per year.
# Create a table that sums the total amount of fraud transactions and calculate the % per year
per_year <- card_fraud %>%
  group_by(trans_year) %>%
  summarize(total_transactions = n(),
            fraudulent_transactions = sum(is_fraud),
            fraudulent_frequency = sum(is_fraud) / total_transactions * 100)

# Print the summary table
print(per_year)
# A tibble: 2 × 4
  trans_year total_transactions fraudulent_transactions fraudulent_frequency
       <dbl>              <int>                   <dbl>                <dbl>
1       2019             478646                    2721                0.568
2       2020             192382                    1215                0.632
•	How much money (in US$ terms) are fraudulent transactions costing the company? Generate a table that summarizes the total amount of legitimate and fraudulent transactions per year and calculate the % of fraudulent transactions, in US$ terms.
# Create a table that sums the total value of fraud transactions and calculate the % per year
valueper_year <- card_fraud %>%
  group_by(trans_year) %>%
  summarize(total_legitimate_amt = sum(amt[is_fraud == 0]),
            total_fraudulent_amt = sum(amt[is_fraud == 1]),
            total_amt = sum(amt),
            fraudulent_percentage = (total_fraudulent_amt / total_amt))

#Show the table
print(valueper_year)
# A tibble: 2 × 5
  trans_year total_legitimate_amt total_fraudulent_amt total_amt
       <dbl>                <dbl>                <dbl>     <dbl>
1       2019            32182901.             1423140. 33606041.
2       2020            12925914.              651949. 13577863.
# ℹ 1 more variable: fraudulent_percentage <dbl>
•	Generate a histogram that shows the distribution of amounts charged to credit card, both for legitimate and fraudulent accounts. Also, for both types of transactions, calculate some quick summary statistics.
#Filter for na
filtered_transactions <- card_fraud[!is.na(card_fraud$amt) & is.finite(card_fraud$amt) & card_fraud$amt >= 0, ]

#Create a category variable for type of transaction
filtered_transactions$tran_cat <- ifelse(card_fraud$is_fraud == 1, "Fraudulent", "Legitimate")

#Plot density graph for both types of transactions
ggplot(filtered_transactions, aes(x = amt, fill = tran_cat)) +
  geom_density(alpha = 0.5) +
  labs(x = "Transaction Value", y = "Frequency", title = "Distribution of Transaction Values", fill = "Type of transaction") +
  xlim(0, 200) 
Warning: Removed 31953 rows containing non-finite values (`stat_density()`).

knitr::include_graphics("/img/creditfraud.jpg",error=FALSE)
