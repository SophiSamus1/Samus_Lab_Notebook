---
layout: post
title: Update on ʻopihi thermal performace curves
date: '2025-09-13'
---

A brief explanation:

For each trial (1 animal), I count heart rate for every waveform (1 wav = 10 sec) 3 different ways: manually (counting the beats myself), FFT (using the spectrum analysis in PicoScope to determine HZ), and then I take an aversge of the two. These three measurements usually result in the same breakpoint temperatures so I choose to use the average (HRavg) most of the time bc it looks the best. For some, the breakpoint temperatures are not the same across the three. This can sometimes be fixed by cleaning up the data a little (removing erronious measurements, getting rid of temps from when the probe came out, averaging 1 min etc.) but for some, nothing changes. I need to figure out the best way to decide which measurement (HR_10, HRspec, or HRavg) is best and if itʻs okay if they donʻt all agree.

Another problem is that not all curves look the same. Some have the expected shape: increase in HR with body temp up to a certain point, past which HR drastically decreases. Some have more of a plateau and slow drop off rather than a specific, sharp drop. How can I treat these all the same way?

The purpose of this post is to have a place to put all of the curves next to each other and discuss next steps/problems/solutions for each, as well as keep track of how many are done.

# ʻOpihi 1 - Trial on July 3, 2025
**Treatment: Desiccation**
**L:34.4 W:27.1 H:11.6**

![ʻOpihi 1](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/opihi1HRavg.png?raw=true)
