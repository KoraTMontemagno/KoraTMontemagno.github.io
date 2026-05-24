---
title: 2. The quest for a pleasure threshold
excerpt: How do you find which stimuli are pleasurable for each participant? 
categories:
- Tutorials
---

So, we have set all our hardware connections and can tell our vibrator to vibrate via our Python script. How do we use it in an actual behavioural experiment?

First of all, we will define the pleasure threshold as the stimulus intensity associated to 50% probability of the participant reporting that it was pleasurable - so, in the perfect world, if you give them 10 stimuli, the will say that 5 were pleasurable and 5 not.

There are several ways to measure sensory thresholds - we will not cover them in this tutorial, but you can find an [overview here](https://link.springer.com/chapter/10.1007/978-1-4419-6488-5_6#Sec15) (it is not specific to pleasure, but some of the methods can be applied across different sensory modalities).
The method we are using is called an **adaptive method** - meaning that 1) we will present a stimulus to a participant, 2) ask whether it was pleasurable, and 3) *based on the response* given by the participant we will finally select the next stimulus in a way that progressively gets closer to the threshold.

#### Useful preliminary observations

Before proceeding, I think most of you will have an objection to this definition and method:

> But doesn't pleasure depend on the participant's arousal?

Yes, it probably does - this phenomenon is referred to as state dependency: the participant response will depend on the state they are in at that moment. There are methods that can take it into account, but they are more complex (and I still have to pilot them): so let's start from the simple bases and build up to them in another tutorial. So bear with me with the simple approach, because it can be that in *some* experimental contexts it is a good way to start.

A different but related complication is that maybe participants may get more sensitive or insensitive to stimuli delivered sequentially, even if they have the same intensity - think about how much rythm, pace, pauses matter in a sexual context. This phenomena are referred to as habituation and sensitivization, and in order to minimize this effects we will try both not to deliver very strong stimuli, and to set a relatively long inter-stimulus interval. Having breaks usually "resets" a bit the perception, but experiments with a lot of stimuli will still probably suffer from this phenomenon.

The third observation is that there may be some intensities that are perceived as too strong or painful by participants - so it is always a good check to test some sample stimuli to get both the participant acquainted with the task and get some feedback before starting the actual experiment to get a higher intensity limit for the algorithm (you could also use a pain threshold paradigm, but your risk delivering too intense stimuli and compromise the future sensation for the pleasure threshold).

Finally, maybe the most important things - pleasure is subjective! We are testing *one* dimension of it, just because it is the thing that we can easily control and quantify, but the assumption we are making is that intensity and pleasure are correlated *somehow*, given a certain type of stimuli in a given parameter space.

#### Let's start programming

We now know all the reasons why this may be a terrible idea - but we want to try somehow. How do we do it? We will explore a tutorial using an adaptive threshold paradigm that you can find [here](https://github.com/KoraTMontemagno/pleasure_experiments) - it is a vit of spaghetti coding, apologies! I hope to make it better when I have more time :)

[To be continued...]


