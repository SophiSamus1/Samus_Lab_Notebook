---
layout: post
title: Update on ʻopihi thermal performace curves
date: '2025-09-13'
tags: [ Thermal Performance ]
---

A brief explanation:

For each trial (1 animal, 1 curve), I count heart rate for every waveform (1 wav = 10 sec) 3 different ways: manually (counting the beats myself), FFT (using the spectrum analysis in PicoScope to determine HZ), and then I take an average of the two: HR_10, HRspec, HRavg, respectively. These three measurements usually result in the same breakpoint temperatures so I choose to use the average (HRavg) most of the time bc it looks the best. For some, the breakpoint temperatures are not the same across the three. This can sometimes be fixed by cleaning up the data a little (removing erronious measurements, getting rid of temps from when the probe came out, averaging 1 min etc.) but for some, nothing changes. I need to figure out the best way to decide which measurement (HR_10, HRspec, or HRavg) is best and if itʻs okay if they donʻt all agree.

Another problem is that not all curves look the same. Some have the expected shape: increase in HR with body temp up to a certain point, past which HR drastically decreases. Some have more of a plateau and slow drop off rather than a specific, sharp drop. How can I treat these all the same way?
also need to pay attention to end of curves - is there a common cutoff temp that may make them look cleaner/smoother?

The purpose of this post is to have a place to put all of the curves next to each other and discuss next steps/problems/solutions for each, as well as keep track of how many are done.

*note: for sliding window, do I need to average bodytemp over 1 minute window as well? bc I havenʻt been --> no, this doesnʻt change anything (9/22)*

ABT = Arrhenius breakpoint temperature. Arrhenius curves show inverse body temp (1/K) vs ln(heart rate). ABT is the breakpoint calculated based on this curve using the segmented package in R.
GAM = general additive model. used to smooth curves. the max point on the smoothed curve may indicate breakpoint temperature.
HR = heart rate
SW = sliding window
BP = breakpoint (not arrhenius)

# ʻOpihi 1 - Trial on July 3, 2025
## **Treatment: Desiccation**	**L:34.4 W:27.1 H:11.6**


### ʻOpihi 1 ABT - original

![ʻOpihi 1 ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/Opihi1_ABT_original.png?raw=true)
* ABT of HRavg, HR_10, and HRspec with segmented model
* HRavg ABT = 33.96 ºC
* HR_10 ABT = 33.97 ºC
* HRspec ABT = 33.76 ºC

*in this case, since they all ABTs are 33.XX ºC, I would consider them in agreement and move on with HRavg since this curve looks the best*


### ʻOpihi 1 ABT + GAM

![ʻOpihi 1 ABT+GAM](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/Opihi1_allABTplusGAM.png?raw=true)
* ABT + GAM (blue). Max point of GAM is dashed purple line.
* GAM BP (purple) is within 95% CI of ABT for HRavg and HRspec, not HR_10
* GAM BPs: HRavg = 34.19 ºC, HR_10 = 34.96 ºC, HRspec = 33.68 ºC


### Average across 1 minute sliding window

![ʻOpihi ABT 1 min sliding window vs normal](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ABTnormalvsslidingwindow.png?raw=true)
* Original segmented models with ABT (top 3) vs 1 minute sliding window (bottom 3)
* From left to right: HRavg, HR_10, HRspec
* All 6 ABTs are 33 ºC (33.76 ºC - 33.97 ºC)

*might want to see what HR_10 looks like with 2 BPs*


### 1 minute averages (not over sliding window)

![all ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi1allABT.png?raw=true)
* These are the segmented models with ABT for everything: original, sliding window, 1 min averages for HRavg, HR_10, and HRspec
* Averaging HR every minute, not across a sliding window does increase ABT slightly. From ~33.8 ºC to ~34.2 ºC


### Overall, the breakpoint temperature of ʻopihi 1 is around 33-34 ºC and generally, there is agreement among methods.


# ʻOpihi 2 - Trial on July 4, 2025
## **Treatment: thermal**	**L:34.1, W:27.8, H:12.1**

*There was a problem during this trial: the temp probe came out for an extended period of time and left a hole in the data. This trial is likely unusable but I should come back to it, I think I can get rid of the hole.*


### ʻOpihi 2 ABT - original

![ʻOpihi2 ABT original](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi2ABT.png?raw=true)
* Segmented models with ABT for HRavg, HR_10, and HRspec
* All ABTs are 39 ºC (39.34-39.6)


### ʻOpihi 2 ABT + GAM

Now add smoothing GAM to get max
![ʻOpihi 2 ABT and GAM](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi2ABTplusGAM.png?raw=true)
* Segmented models with ABT plus GAM (blue) for all 3, HRavg, HRspec, HR_10
* The max point of GAM is in purple
* GAM BP is much lower than ABT and only within 95% CI of ABT for HR_10. HRsec and HRavg GAM BP is 37 ºC, HR_10 GAM BP is 38 ºC, ABTs are 39 ºC
	* No agreement between GAM and ABT


### Average across 1 minute sliding window

![ʻOpihi2 ABT SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi2ABT_SW.png?raw=true)
* Segmented models with ABTs for raw (top) vs 1 min sliding window (bottom)
* Only ABT that didnʻt change is HR_10, the reset decreased after applying 1 min averages over sliding window

*I think because HRspec is so bad, itʻs making HRavg bad bc HR_10 looks okay*


### 1 minute averages (not over sliding window)

![ʻOpihi2 all ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi2allABT.png?raw=true)
* All segmented models with ABTs
* ABTs for 1 min averages (bottom 3) are all 39 ºC, same as original ABTs (top row). Sliding window (middle) changes ABT.

### Overall, the curves donʻt look very good and there is a lot of spread. However, with the exception of the ABTs from HR 1 minute averages over sliding window (and GAM maxes), the ABT is consistently ~39 ºC. This breakpoint temperature is much higher than ʻopihi 1 (thermal vs desiccation).


# ʻOpihi B072 - Trial on August 12, 2025
**Treatment: desiccation**	**L:33.0, W:26.3, H:10.5**


### B072 ABT - original

![B072 original ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B072originalABT.png?raw=true)
* Original segmented models with ABT
* HRavg ABT = 33.36 ºC
* HR_10 ABT = 33.97 ºC
* HRspec ABT = 32.52 ºC :/


### B072 ABT + GAM

![B072 ABT+GAM](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B072_ABTplusGAM.png?raw=true)
* GAM BP is within ABT 95% CI for HRavg and HRspec, but not for HR_10
* GAM BP and ABT agree for HR_10 and HRspec, not for HRavg

*no agreement or clear path forward here*


### Average across 1 minute sliding window

![B072 ABT SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B072_ABToriginalvsSW.png?raw=true)
* complete agreement between original ABT and SW ABT
* all SW ABT do not agree, though - HRspec still 32ºC


### 1 minute averages (not over sliding window)

![B072 all ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B072allABT.png?raw=true)
* HR_10 is the only of the three that ABT changes 
* averaging over 1 minute adds more variation - no agreement


### Breakpoint temps vary from 32-34 ºC


# ʻOpihi B074 - Trial on August 12, 2025
**Treatment: thermal**	**L:33.0, W:26.3, H:10.5**


### B074 ABT - original

![B074 original ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B074originalABT.png?raw=true)
* original segmented models with ABT
* HRavg ABT = 33.3 ºC
* HR_10 ABT = 33.59 ºC
* HRspec ABT = 33.1 ºC
* HRspec looks crazy but at least theyʻre all 33 ºC

### B074 ABT + GAM

![B074 ABT+GAM](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B074_ABTplusGAM.png?raw=true)
* Segmented models with ABT plus GAM smoothing
* GAM BPs are higher (34 ºC)
* obviously spec doesnt work but rest are within 95% CI of ABT


### Average across 1 minute sliding window

![B074 ABT SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B074_ABToriginalvsSW.png?raw=true)
* Original (top) and 1 min SW (bottom) segmented models with ABT
* ABT stays the same  (33ºC) for all except HRspec (same problem as GAM)


### 1 minute averages (not over sliding window)

![B074 all ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B074allABT.png?raw=true)
* Segmented models with ABT for all methods
* HRavg ABT decreased (32 ºC) for 1 min average (no SW), stayed the same (33 ºC) for HR_10, and HRspec doesnʻt work

*I wonder if added BPs to HRspec for the averages would fix the problem*


### Good agreement from the beginning despite terrible looking curves - thereʻs so much spread even in the 1 min averages. Breakpoint temp is ~ 33 ºC.


# ʻOpihi B075 - Trial on August 26, 2025
**Treatment: thermal**	**L:41.1, W:34.0, H:14.7**


### B075 ABT - original

![B075 original ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B075originalABT.png?raw=true)
* original segmented models with ABTs - top is 1 BP and bottom is 2 BPs
	* with 1 BP, HRspec is the only correct one. And with 2 BPs, the first is never the correct one.
	* the only reason itʻs identifying a BP at low temps is because of the weird spread 
* wll probably benefit from smoothing and 1 minute averages
* with 2 ABTs, the second:
	* HRavg: 37.86 ºC
	* HR_10: 37.56 ºC
	* HRspec: 38.07 ºC
* The ABT of HRspec with only 1 BP is 37.88 ºC 

*note: some of the names in the captions are wrong. this is B075*


### Note about body temp

![B075 Body Temp](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B075bodytempTime.png?raw=true)
* This is bodytemp through time
* There is a small section with unusually high body temps, I could remove them and this might help

*come back to this*


### B075 ABT + GAM

![B075 ABT+GAM 2 BP](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B075_ABTplusGAM.png?raw=true)
* Segmented models with ABT (2 BP) and GAM
	* may want to add figs for 1 BP too
* GAM BPs consistently 36 ºC and almost (just outside for some) within 95% CI of ABT


### Average across 1 minute sliding window

![B075 1 ABT SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B075_1ABT_SW.png?raw=true)
* Segmented models with 1 ABT, original (top) and average 1 min SW (bottom)
* the SW fixes HRavg! ABT = 37.39 ºC
	* with 2 ABTs, HRavg is 37.86 ºC

![B075 2 ABT SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B075_2ABT_SW.png?raw=true)
* Segmented models with 2 ABTs, original (top) and average 1 min SW (bottom)
* Now, all ABTs but original HRspec are 37.XX ºC


### 1 minute averages (not over sliding window)

![B075 all ABT 1](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B075_all1ABT.png?raw=true)
* Segmented models with 1 ABT for all methods (original, SW, 1 min avg)
* 1 min averages (no SW) doesnʻt fix anything with only 1 ABT


![B075 all ABT 2](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B075_all2ABT.png?raw=true)
* Segmented models with 2 ABTs for all methods (original, SW, 1 min avg)
* all ABTs are 37.XX ºC except for original HRspec and 1 min avg HRspec (38 ºC, but only barely)

### General agreement around 37 ºC


# ʻOpihi B052 - Trial on August 28, 2025
**Treatment: desiccation**	**L:32.4, W:26.3, H:11.5**

### B052 ABT - original

![B052 original ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B052originalABT.png?raw=true)
* original segmented models with ABT
* HRavg = 30.53 ºC
* HR_10 = 32.65 ºC
* HRspec = 29.5 ºC
* No agreement :/

*forgot to put HRavg, HR_10 and HRspec in figure titles*


### B052 ABT + GAM

![B052 ABT+GAM](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B052_ABTplusGAM.png?raw=true)
* ABT + GAM
* GAM BP within (or almost) 95% CI of ABT for all
* No agreement among GAM BPs (31, 33, 30)


### Average across 1 minute sliding window

![B052 ABT SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B052_ABT_SW.png?raw=true)
* Segmented model with ABT, original (top) and SW (bottom)
* SW matches original, no agreement among HRavg, 10, and spec


### 1 minute averages (not over sliding window)

![B052 all ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B052_allABT.png?raw=true)
* all ABT
* still no agreement among avg, 10, and spec
* ABT same among original, SW, and 1 min avg


### No ABT agreement between HRavg, HR_10, and HRspec but stays the same across original, SW, and 1 min avg. ABT ranges from 29-32 ºC


# ʻOpihi B053, Trial on August 28, 2025
**Treatment: thermal**	**L:37.2, W:29, H:12.8**

### B075 ABT - original

![B053 original ABT](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B053_originalABT.png?raw=true)
* original ABT, 1 BP and 2 BPs
* these curves look much better than the rest
* 2 BPs seems to fit better
* ABTs variable with only 1 ABT, with 2 ABTs all are 37 ºC (2nd BP)


### B075 ABT + GAM

![B053 ABT+GAM](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B053_ABTplusGAM_1and2BP.png?raw=true)
* ABT+GAM, 1 and 2 BPs
* GAM BPs generally outside of ABT 95% CI
* BPs either 36 or 37 ºC


### Average across 1 minute sliding window

![B053 1 ABT SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B053_1ABT_SW.png?raw=true)
* ABT sliding window vs original, 1 breakpoint
* same as original, no total agreement

![B053 2 ABT SW](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B053_2ABTSW.png?raw=true)
* ABT sliding window vs original, 2 breakpoints
* with 2 BPs, the SW ABT of HR_10 changes to 36 ºC

*this one might benefit from some cutoff towards the end*


### 1 minute averages (not over sliding window)

![B053 all ABT1](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B053_allABT_1.png?raw=true)
* all ABT 1 breakpoint
* ABTs match among methods (original, SW, 1 min avg), but not measurements (avg, 10, spec)

![B053 all ABT2](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/B053_allABT_2.png?raw=true)
* all ABT 2 breakpoints
* the only ones that are not 37 ºC are SW (36.51 ºC) and 1 min avg for HR_10 (36.99 ºC)

### There is agreement among originals with 2 ABT (37 ºC) but changes a little with averages.


# In total: 7 ʻopihi (trails, curves), 4 thermal, 3 desiccation. Thermal ABTs: 37 ºC, 37 ºC, 39 ºC, 33 ºC. Desiccation ABTs: 33-34 ºC, 32-34 ºC, 29-32 ºC. ABTs of thermal treatment ʻopihi are generally much higher (greater heat tolerance when wet). Desiccation group ʻopihi may also be more difficult to get ABT (less agreement, more difficult curves).





NOTES:
-try 30 sec or 1 min average
-matt likes sliding window
-arbitrRy interval changing the answer - there is something in the interval choice
	-if averge every 30 sec, could get more variance between averages

double check july 4 with gap - SW  across gap? should I do two separate sliding windows?

ask keith about the spread - natural variation? is there a reason some curves look so much worse than others?

look at starting curves exactly at 25 body temp - does it matter that they acclimate at the same temperature or reach the same equilibrium temp ?
look at body temp vs time curves - add these to the post

how muh effort to continue to do picoscope and normal counts





















