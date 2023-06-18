---
categories:
- ""
- ""
date: "2017-10-31T22:42:51-05:00"
description: #Create a table that counts the number of shootings per race 
shoot_per_race <- mass_shootings %>%
  group_by(race)%>%
  summarise(shootings = n())

#Create the bar chart in descendent order
ggplot(shoot_per_race, aes(x = reorder(race, -shootings), y = shootings)) +
  geom_bar(stat = "identity", fill = "steelblue") +
  labs(x = "Race Category", y = "Number of Shooters") +
  ggtitle("Number of Mass Shooters by Race") + geom_text(aes(label = shootings), vjust = -0.5, color = "black")

draft: false
image: pic07.jpg
keywords: ""
slug: Mass Shootings By Race
title: Mass Shooting By Race
---
