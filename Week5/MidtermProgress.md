# Orbital Sandbox Simulator - Mid-Term Project

## Trial Codes:

[Required features in 2 bodies](https://editor.p5js.org/soumen02/sketches/Kz3qDskBg)

[Attempt to combine them into each object](https://editor.p5js.org/soumen02/sketches/nbZCqGCj9)

## Inspiration 

Back in 2007, the first games I ever played were on [Cool Math Games](https://www.coolmathgames.com/). The website used to come up with new games every week or so, adding on to a never ending collection of flash player games (which has now been discontinued). My favourite ones were the ones where some level of physics was involved, and it was in fact the source of my interest in the subject of physics as it gave me an unlimited playground to test out my imagination. 

For that reason, I chose to make a physics simulation based game - an orbit simulator! The game does not have an objective - other than that of testing out your imagination and have fun! 

## Concept

The game uses the Universal Law of Gravitation and other related Laws of Motion for its physics. It will be tweaked to make the game user friendly - in terms of the ratio of sizes, masses and force applied. 

![Universal Law of Gravitation](https://user-images.githubusercontent.com/38569809/156557073-a1aa6ff5-657a-4a23-82d6-35d25b1460bb.png)

THe game expects to have mechanics similar to the simulation shown below.

![PhET Gravity and Orbits](https://user-images.githubusercontent.com/38569809/156557743-602185bc-6116-42e8-bd1e-5b29c7bd9225.png)



The game expects to have multiple bodies which are given a mass, radius and an initial velocity by the user. Each body simulates motion by imposing gravity on every other body. Adding a trail to these bodies results in beautiful patters. 

## How to Play

A body is created at the point of mousePress(). Then, the body can be given a velocity by dragging in the opposite direction, much like a slingshot. 


## Development
### Initial Attempt 

I first started by trying to figure out the Physics. The Physics of attraction and gravity requires the use of vectors. 
I found the following nature of Code videos by The Coding Train to be immensly useful for understand how displacement, vectors and acceetarion works :
  - [The Acceleration Vector](https://www.youtube.com/watch?v=T84AWnntxZA&t=76s)
  - [Gravitataion Attraction](https://www.youtube.com/watch?v=EpgB3cNhKPM&t=522s)


### Current progress

I'm currently trying to implement force between two bodies in the form of a vector. 

## Challenges

Understanding the vector calculation that goes into the making of the framwork was a demanding task (which Daniel Shiffman's video made easier). 

Secondly, I'm facing a challenge figuring out the mechanics of applying this force across N bodies. For a simulation of gravity, I will need to find the net force on each body, requiring a high time complexity if I don't optimize the code (using memoization?).
