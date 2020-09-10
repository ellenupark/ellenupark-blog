---
layout: post
title:      "CLI Project Complete!"
date:       2020-09-10 19:07:22 +0000
permalink:  cli_project_complete
---


For my first solo coding project I created a Ruby gem containing a CLI program. I knew from the beginning that I wanted to focus my project on the topic of video games. In the end, I picked an Animal Crossing API to retrieve data and create a villager directory. 

Upon initialization, my program first greets the user and displays a list of 10 featured villagers. You can then select one of those villagers to view more detailed information. There is also an option to search by villager name when trying to find a specific villager. At any point, you can type “exit” to end the program.
	
Before starting this project the thought of writing my own program from scratch terrified me. I had no idea where to start. But thankfully, I learned about bundler while watching one of Avi’s videos. To put it simply, Bundler can generate standard gems which you can then build your Ruby project upon. I used Bundler to create my default gem with all my necessary files and folders already in place. This sped up my process a lot (but quickly slowed back down as I tried to decipher what all the files were supposed to do). 
	
After my gem was set up, I began the coding process. I created my executable file in my bin folder and my environment file in my lib folder. In addition I created 3 different files in the lib folder each with their own class. A Villager, API, and CLI class. I started with the API file. I wrote two methods, one to retrieve data from my API and the other to assign villager attributes based on the data. In the villager file, I had my Villager class. This was responsible for creating the actual villager instances. I also had my CLI folder which controlled how my program would actually run.

I easily spent the most time coding my CLI class. It was a fairly short process to get my program “working”, but it was a long process to clean up my code and try to make the user experience as pleasant as possible. Although I fulfilled the project requirements with just my main page listing 10 featured villagers, I knew I wanted to implement some type of feature that would allow the user to access the entire villager database. I achieved this by adding a "search” function. If the user types “search” it will allow them to search alphabetically by name to find any specific villager. This feature alone accounted for the majority of my coding time. But once I had it running smoothly it was also the most rewarding. 

All in all I had a great time working on this project. I feel that I’ve learned a lot about the relationship between objects and how they work together to form a program. I’ve also gained a lot of knowledge about gems and their structure. And of course, I’ve learned about APIs. In the past, I would hear “API” and have absolutely no clue what it meant. But now, I do know what it means. And that may seem small, but to me it is a huge milestone. It’s a sign that I am actually learning and progressing towards my goal.
