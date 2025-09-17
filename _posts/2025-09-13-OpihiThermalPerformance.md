---
layout: post
title: Update on ʻopihi thermal performace curves
date: '2025-09-13'
tags: [ Thermal Performance ]
---

A brief explanation:

For each trial (1 animal), I count heart rate for every waveform (1 wav = 10 sec) 3 different ways: manually (counting the beats myself), FFT (using the spectrum analysis in PicoScope to determine HZ), and then I take an aversge of the two. These three measurements usually result in the same breakpoint temperatures so I choose to use the average (HRavg) most of the time bc it looks the best. For some, the breakpoint temperatures are not the same across the three. This can sometimes be fixed by cleaning up the data a little (removing erronious measurements, getting rid of temps from when the probe came out, averaging 1 min etc.) but for some, nothing changes. I need to figure out the best way to decide which measurement (HR_10, HRspec, or HRavg) is best and if itʻs okay if they donʻt all agree.

Another problem is that not all curves look the same. Some have the expected shape: increase in HR with body temp up to a certain point, past which HR drastically decreases. Some have more of a plateau and slow drop off rather than a specific, sharp drop. How can I treat these all the same way?

The purpose of this post is to have a place to put all of the curves next to each other and discuss next steps/problems/solutions for each, as well as keep track of how many are done.

# ʻOpihi 1 - Trial on July 3, 2025
**Treatment: Desiccation**
**L:34.4 W:27.1 H:11.6**

![ʻOpihi 1](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi1HRavg.png?raw=true)
^This is the segmented model using HRavg

![ʻOpihi 1 GAM](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi1HRavg-GAM.png?raw=true)
^This is the segmented model with a GAM on top. The purple line is the max point of GAM. The purple breakpoint is within the ABT of the segmented model and off by ~0.2 ºC.

### There is still a lot of spread so letʻs try averaging HR every minute, both across a sliding window and not.

![ʻOpihi 1 min sliding window](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi1slidingwindowvsraw.png?raw=true)
^This is the normal 1 min sliding window average vs the normal raw


![ʻOpihi ABT 1 min sliding window vs normal](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ABTnormalvsslidingwindow.png?raw=true)
^This is ABT normal vs 1 min average sliding window

### Still a little messy, letʻs see what it looks like just averaged every minute, not over sliding window.

![1 min avg](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi1_1minavgnoSW.png?raw=true)
^normal, not ABT, 1 min average vs raw

![all ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi1allABT.png?raw=true)
^this is all ABT for opihi 1 (normal, SW, 1 min avg)

The ABT changed from 33 ºC to 34 ºC when averaged every minute, not over sliding window.

# ʻOpihi 2 - Trial on July 4, 2025
**Treatment: thermal**
**L:34.1, W:27.8, H:12.1**

![ʻOpihi2 ABT original](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi2ABT.png?raw=true)
This is ABT figures for HR_10, HRavg, HRspec

Now add smoothing GAM to get max
![ʻOpihi 2 ABT and GAM](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi2ABTplusGAM.png?raw=true)
ABT+GAM for all 3, HRavg, HRspec, HR_10
GAM BP only within 95% CI of ABT for HR_10. HRsec and HRavg GAM BP is 37 ºC, HR_10 GAM BP is 38 ºC, ABTs are 39 ºC

![ʻOpihi2 SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi2SWvsnot.png?raw=true)
^this is SW vs not for all 3

![ʻOpihi2 ABT SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi2ABT_SW.png?raw=true)
ABT SW vs not

![ʻOpihi2 1 min avg, no SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi21minavg_noSW.png?raw=true)
1 min avg for all 3, no sw vs raw

![ʻOpihi2 all ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi2allABT.png?raw=true)
opihi 2 all abt

