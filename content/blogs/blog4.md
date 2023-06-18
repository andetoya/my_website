---
categories:
- ""
- ""
date: "2017-10-31T22:42:51-05:00"
description: Analysis of mass shootings in USA by race

draft: false
image: mass.png
keywords: ""
slug: massshootings
title: Mass Shooting By Race
---
#Graph of Shootings by Race
#Create a table data shows the number of shootings per
shoot_per_year <- mass_shootings %>% 
  group_by(year)%>%
  summarise(shootings = n())
•	Generate a bar chart that identifies the number of mass shooters associated with each race category. The bars should be sorted from highest to lowest and each bar should show its number.
#Create a table that counts the number of shootings per race 
shoot_per_race <- mass_shootings %>%
  group_by(race)%>%
  summarise(shootings = n())

#Create the bar chart in descendent order
ggplot(shoot_per_race, aes(x = reorder(race, -shootings), y = shootings)) +
  geom_bar(stat = "identity", fill = "steelblue") +
  labs(x = "Race Category", y = "Number of Shooters") +
  ggtitle("Number of Mass Shooters by Race") + geom_text(aes(label = shootings), vjust = -0.5, color = "black")

knitr::include_graphics("/img/mass.jpg",error=FALSE)
