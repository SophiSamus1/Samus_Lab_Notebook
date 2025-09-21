---
layout: post
title: Update on ʻopihi thermal performace curves
date: '2025-09-13'
tags: [ Thermal Performance ]
---

A brief explanation:

For each trial (1 animal), I count heart rate for every waveform (1 wav = 10 sec) 3 different ways: manually (counting the beats myself), FFT (using the spectrum analysis in PicoScope to determine HZ), and then I take an aversge of the two. These three measurements usually result in the same breakpoint temperatures so I choose to use the average (HRavg) most of the time bc it looks the best. For some, the breakpoint temperatures are not the same across the three. This can sometimes be fixed by cleaning up the data a little (removing erronious measurements, getting rid of temps from when the probe came out, averaging 1 min etc.) but for some, nothing changes. I need to figure out the best way to decide which measurement (HR_10, HRspec, or HRavg) is best and if itʻs okay if they donʻt all agree.

Another problem is that not all curves look the same. Some have the expected shape: increase in HR with body temp up to a certain point, past which HR drastically decreases. Some have more of a plateau and slow drop off rather than a specific, sharp drop. How can I treat these all the same way?
also need to pay attention to end of curves - is there a common cutoff temp that may make them look cleaner/smoother?

The purpose of this post is to have a place to put all of the curves next to each other and discuss next steps/problems/solutions for each, as well as keep track of how many are done.

*just realized for sliding window, do I need to average bodytemp over 1 minute window as well? bc I havenʻt been*

# ʻOpihi 1 - Trial on July 3, 2025
**Treatment: Desiccation**
**L:34.4 W:27.1 H:11.6**

![ʻOpihi 1](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi1HRavg.png?raw=true)
* segmented model using HRavg
* ABT = 33.96 ºC


![ʻOpihi 1 GAM](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi1HRavg-GAM.png?raw=true)
* This is the segmented model (red) with a GAM (blue) on top. 
* The purple line is the max point of GAM - is within the 95% CI of ABT from the segmented model and off by ~0.2 ºC.
* Breakpoint using GAM is 34.19 ºC

### There is still a lot of spread so letʻs try averaging HR every minute, both across a sliding window and not.

![ʻOpihi 1 min sliding window](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi1slidingwindowvsraw.png?raw=true)
* 1 minute sliding window on the left, raw data on the right
* From top to bottom: HR_10, HRspec, HRavg


![ʻOpihi ABT 1 min sliding window vs normal](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ABTnormalvsslidingwindow.png?raw=true)
* Original segmented models with ABT (top 3) vs 1 minute sliding window (bottom 3)
* From left to right: HRavg, HR_10, HRspec
* All 6 ABTs are 33 ºC (33.76 ºC - 33.97 ºC)


### Letʻs see what it looks like averaging HR every minute, NOT over a sliding window.

![1 min avg](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi1_1minavgnoSW.png?raw=true)
* 1 minute average (left) vs raw (right)
* From top to bottom: HR_10, HRspec, HRavg

![all ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi1allABT.png?raw=true)
* These are the segmented models with ABT for everything: raw, sliding window, 1 min averages for HRavg, HR_10, and HRspec
* Averaging HR every minute, not across a sliding window does increase ABT slightly. From ~33.8 ºC to ~34.2 ºC

### Overall, the breakpoint temperature of ʻopihi 1 is around 33-34 ºC and generally, there is agreement among methods.


# ʻOpihi 2 - Trial on July 4, 2025
**Treatment: thermal**
**L:34.1, W:27.8, H:12.1**

There was a problem during this trial: the temp probe came out for an extended period of time and left a hole in the data. This trial is likely unusable but I should come back to it.

![ʻOpihi2 ABT original](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi2ABT.png?raw=true)
* Segmented models with ABT for HRavg, HR_10, and HRspec
* All ABTs are 39 ºC (39.34-39.6)

Now add smoothing GAM to get max
![ʻOpihi 2 ABT and GAM](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi2ABTplusGAM.png?raw=true)
* Segmented models with ABT plus GAM (blue) for all 3, HRavg, HRspec, HR_10
* The max point of GAM is in purple
* GAM BP is much lower than ABT and only within 95% CI of ABT for HR_10. HRsec and HRavg GAM BP is 37 ºC, HR_10 GAM BP is 38 ºC, ABTs are 39 ºC

![ʻOpihi2 SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi2SWvsnot.png?raw=true)
* HR averaged over 1 min sliding window (left) vs raw (right)

![ʻOpihi2 ABT SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi2ABT_SW.png?raw=true)
* Segmented models with ABTs for raw (top) vs 1 min sliding window (bottom)
* Only ABT that didnʻt change is HR_10, the reset decreased after applying 1 min averages over sliding window

![ʻOpihi2 1 min avg, no SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi21minavg_noSW.png?raw=true)
* 1 min avg, no sliding window (left) vs raw (right)

![ʻOpihi2 all ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi2allABT.png?raw=true)
* All segmented models with ABTs
* ABTs for 1 min averages (bottom 3) are all 39 ºC, same as original ABTs (top row). Sliding window (middle) changes ABT.

### Overall, the curves donʻt look very good and there is a lot of spread. However, with the exception of the ABTs from HR 1 minute averages over sliding window (and GAM maxes), the ABT is consistently ~39 ºC. This breakpoint temperature is much higher than ʻopihi 1 (thermal vs desiccation).


# ʻOpihi B072 - Trial on August 12, 2025
**Treatment: desiccation**
**L:, W:, H:**

![B072 original ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B072originalABT.png?raw=true)
* all original ABT

![B072 ABT+GAM](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B072_ABTplusGAM.png?raw=true)
* ABT+GAM

![B072 ABT SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B072_ABToriginalvsSW.png?raw=true)
* ABT SW vs original

![B072 all ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B072allABT.png?raw=true)
* all ABT


# ʻOpihi B074 - Trial on August 12, 2025
**Treatment: thermal**
**L:, W:, H:**

![B074 original ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B074originalABT.png?raw=true)
* all 3 original ABT, HRavg, HR_10, HRspec
* spec looks crazy but at least theyʻre all 33 ºC

![B074 ABT+GAM](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B074_ABTplusGAM.png?raw=true)
* ABT+GAM smoothing
* obviously spec doesnt work but rest are w/in 95% CI

![B074 ABT SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B074_ABToriginalvsSW.png?raw=true)
* ABT original vs SW

![B074 all ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B074allABT.png?raw=true)
* all ABT


# ʻOpihi B075 - Trial on August 26, 2025
**Treatment: thermal**
**L:41.1, W:34.0, H:14.7**

![B075 original ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B075originalABT.png?raw=true)
* original ABTs - 1 and 2 BPs
* wll probably benefit from smoothing and 1 minute averages

![B075 Body Temp](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B075bodytempTime.png?raw=true)
* may need to come back to this and get rid of small section

![B075 ABT+GAM 2 BP](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B075_ABTplusGAM.png?raw=true)
* ABT+GAM for 2 BP, may want to add figs for 1 BP too

![B075 1 ABT SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B075_1ABT_SW.png?raw=true)
* 1 ABT SW vs original

![B075 2 ABT SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B075_2ABT_SW.png?raw=true)
* 2 ABT SW vs original

![B075 all ABT 1](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B075_all1ABT.png?raw=true0
* all ABT (1 breakpoint)


![B075 all ABT 2](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B075_all2ABT.png?raw=true)
* all ABT (2 breakpoints)









