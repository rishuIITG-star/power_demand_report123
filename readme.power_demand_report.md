# Welcome to the Power Demand Forecaster! ⚡

Have you ever wondered how power grids know exactly how much electricity an entire city is going to use at any given moment? It's a massive balancing act, and getting it wrong can lead to blackouts or wasted energy. 

This project is our attempt to help solve that puzzle. We've built an automated pipeline that takes messy, real-world historical electricity data, cleans it up, and uses it to predict future power demand. Think of it as a crystal ball for the power grid, powered by machine learning!

## What Makes This Project Tick?

We designed this project to be as straightforward as possible, focusing on three main pillars:

* **🧹 Cleaning Up the Mess:** Real-world data is rarely perfect. Sensors break, clocks get out of sync, and weird spikes happen. Our code acts as an automated janitor, scrubbing the data clean before we use it.
* **⚙️ Giving the Data Context:** A computer can't predict the future just by looking at a single number. We transform the basic data into a rich "story" that helps our model understand trends and patterns.
* **📈 Looking into the Future:** We train a machine learning model to look at all this historical context and make educated guesses about what tomorrow's power demand will look like, complete with visual scorecards to see how well we did.

***

## How We Do It (The Step-by-Step)

Here is a plain-English look under the hood at how our pipeline actually works:

### 1. Wrangling the Raw Data
When we first load up the operational grid data, it can be a bit chaotic. Here is how we get it into shape:
* **Fixing the Clocks:** We make sure the computer perfectly understands the dates and times.
* **Tossing Out Impossible Numbers:** If a sensor accidentally records a demand of "zero" or spikes to a completely impossible high, we catch it and remove it so it doesn't confuse our model.
* **Filling in the Blanks:** If there's a tiny gap in the data (like a missing hour), we basically play connect-the-dots between the known points to fill it in safely. We also make sure brand-new power sources (like recently built solar farms) show up as "zero" for the years before they existed!

### 2. Teaching the Model (Feature Engineering)
To predict the future, you have to understand the past. We create special data points to give our model a "memory":
* **Looking in the Rearview Mirror:** We create columns that tell the model, *"Hey, here is what power demand looked like exactly 1 hour ago, 24 hours ago, and a week ago."* This helps the model spot daily and weekly routines.
* **Smoothing the Ride:** We calculate rolling averages (like the average demand over the last 24 hours). This helps the model ignore sudden, random hiccups and focus on the overall, steady trends. 

### 3. The Crystal Ball (Predictions & Grading)
Once the data is clean and full of context, it's time for the main event:
* **Making the Guesses:** We feed all our historical data into a machine learning model (specifically, a *Random Forest*) so it can learn the hidden rules of power consumption. 
* **Grading the Test:** We don't just blindly trust the model. We hold back some historical data, ask the model to predict it, and then grade its homework. We use standard metrics (like checking the exact Megawatt difference between the guess and reality) to see how accurate it is.
* **Drawing the Picture:** Finally, we plot the actual power demand right on top of our predicted demand. There's no better way to see how well the model works than looking at a beautiful chart!
