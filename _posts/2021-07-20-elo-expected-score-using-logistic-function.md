---
layout: post
title: "Using the Logistic Function to Compute Elo"
date: Tue Jul 20 20:53:38 PDT 2021
---

When designing ordered rankings (sports, gaming, even [dating](https://beyondmatching.com/tinder-elo-explained/)),
the [Elo Rating System](https://en.wikipedia.org/wiki/Elo_rating_system) in chess has proven very useful.

[FIDE](https://www.fide.com/) has tweaked the original rating scheme over the years, but in its current form it is:

$$E_A = \frac{1}{1 + 10^\frac{R_B - R_A}{400}}$$

$$E_A$$ represents the probability (expected outcome) of Player A beating Player B. The base of 10 and standard
deviation of 400 have been chosen such that when players have a 400 point difference, there is a 90% chance that
the stronger player will win:

$$\frac{1}{1 + 10^\frac{-400}{400}} = \frac{1}{1 + 10^{-1}} = \frac{1}{\frac{11}{10}} = 0.90$$

And a 50/50 chance for either player winning when they have equal ratings:

$$\frac{1}{1 + 10^\frac{0}{400}} = \frac{1}{1 + 1} = \frac{1}{2} = 0.50$$

After a given outcome has occurred, the formula below is used to update each player's rating is:

$$R' = R + K(S - E)$$

This updates a player's rating given: current rating $$R$$, expected probability of winning $$E$$, and outcome $$S$$.

Some new variables that require definitions: $$K$$ is the K-factor constant controlling the sensitivity of update:
larger for more sensitive and smaller for less. $$S$$ is the score which takes value 1 for win, 0 for loss, and 0.5
for tie.
