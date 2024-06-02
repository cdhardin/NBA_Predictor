# NBA Ball Possession Markov Chains

## Project Overview

This project involves collecting and analyzing NBA player passing data to create ball possession Markov chains for each team. Using these Markov chains, we simulate games and entire seasons. The data was collected from NBA.com and Basketball Reference using web scrapers.

## Table of Contents

1. [Introduction](#introduction)
2. [Data Collection](#data-collection)
3. [Markov Chains](#markov-chains)
4. [Game and Season Simulation](#game-and-season-simulation)

## Introduction

The goal of this project is to model and simulate NBA games and seasons using statistical methods. By analyzing player passing data, we can build Markov chains that represent ball possession transitions within a team. These chains serve as the foundation for simulating realistic games and seasons.

## Data Collection

### Sources

- **NBA.com**: Official site for NBA stats and data.
- **Basketball Reference**: Comprehensive database of basketball statistics.

### Web Scrapers

We have implemented web scrapers to extract the necessary data from the above sources. The scripts for web scraping are located in the `scrapers` directory.

### Data Extraction

The collected data includes:
- Player passing statistics
- Team rosters
- Game schedules
- Historical game results

## Markov Chains

Using the extracted player passing data, we construct Markov chains for each team. These chains model the probability of the ball being passed between players and other events such as shooting or turnovers.

A deeper look into the dynamics of a team’s possession reveals that public data from NBA.com provides the probability of a player passing to any other player on his team. Using this information, a transition matrix can be created for each team.

### Game State Definition

A game state can be defined by two random variables:
- **Team Possession**: Which belongs to either team A or team B.
- **Ball Possession**: Which can belong to any player \(i\) on team \(j\), where team \(j\) is the team with possession.

### Simulation Steps

At each change in ball possession, the model takes the following steps for player \(i\):

1. **Time Calculation**: Use player \(i\)’s average time per possession to pull a Poisson random number with that mean to determine how much time runs off during this possession.

2. **Shot Clock Check**: If the time run-off will lead to team \(j\)’s total time of possession reaching 24 seconds (the length of the shot clock), player \(i\) shoots. If not, player \(i\) has some probability of shooting.

3. **Shot Determination**: If player \(i\) shoots, use his data to determine if he shoots a 2 or 3 pointer, and then determine if he makes or misses the shot. Additionally, every shot has some probability of the player then taking a free throw.

4. **Transition Matrix Check**: If player \(i\) is not shooting, check the transition matrix to determine where the possession goes next. There is some probability \(prob\_TOV\) that player \(i\) turns the ball over and team possession changes teams. If not, pull from the transition matrix to see where ball possession will go next, and repeat all the past steps.

An example transition matrix can be seen in figure 5.

## Game and Season Simulation

With the Markov chains in place, we can simulate:
- **Individual games**: Using the team's Markov chain to determine the flow of possession and the outcome.
- **Seasons**: Simulating a series of games according to the NBA schedule to predict overall team performance.

The simulation scripts are located in the `simulations` directory.

---

### Contributions
Thank you to Tim Najar who collaborated on this project. He created a different markov chain model based on team stats instead of player stats. Our models produced similar results.

Feel free to reach out with any questions or feedback! We hope this project provides valuable insights into the dynamics of NBA games through the lens of Markov chains.
