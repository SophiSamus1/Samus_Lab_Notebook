---
layout: post
title: RNAseq library prep options
date: '2026-01-14'
tags: [ RNAseq ]
---

several different options for 'opihi library prep and sequencing:
several pools (low conc. and high conc.), seq coverage

# From initial QC at core

| sample | 	treatment	 | < 500 ng input | < 50 ng input | low quality | Max Input (ng) |
| ------ | ------------- | -------------- | ------------- | ----------- | -------------- |
| B047   | control   	 | no - good 	  | no - good	  | no			| 540		 	 |
| B037	 | control   	 | no - good 	  | no - good	  | no			| 1410			 |
| B043	 | control   	 | no - good 	  | no - good	  | no			| 585		 	 |
| B033	 | control   	 | no - good 	  | no - good	  | no			| 3175		 	 |
| B039	 | control   	 | no - good	  | no - good	  | no			| 685		 	 |
| B025   | control   	 | **yes - bad**  | **yes - bad** | **YES**		| 1.5		 	 |
| B048	 | control   	 | no - good 	  | no - good	  | no			| 775		 	 |
| B031	 | control   	 | **yes - bad**  | **yes - bad** | no			| 12.6		 	 |
| B045	 | thermal   	 | no - good 	  | no - good	  | no			| 915		 	 |
| B030	 | thermal   	 | **yes - bad**  | no - good	  | no			| 142		 	 |
| B050	 | thermal   	 | no - good 	  | no - good	  | no			| 1025		 	 |
| B042	 | thermal   	 | no - good 	  | no - good	  | no			| 2850		 	 |
| B040   | thermal   	 | **yes - bad**  | no - good	  | no			| 303		 	 |
| B064   | thermal   	 | **yes - bad**  | no - good	  | no			| 110		 	 |
| B024   | thermal   	 | **yes - bad**  | **yes - bad** | **YES**		| 9.8		 	 |
| B034   | thermal   	 | **yes - bad**  | no - good	  | no			| 228		 	 |
| B063	 | desiccation	 | no - good 	  | no - good	  | no			| 2550 		 	 |
| B026	 | desiccation	 | no - good 	  | no - good	  | no			| 985		 	 |
| B032	 | desiccation	 | no - good 	  | no - good	  | no			| 870		 	 |
| B049	 | desiccation	 | no - good 	  | no - good	  | no			| 1750		 	 |
| B046	 | desiccation	 | no - good 	  | no - good	  | no			| 2700		 	 |
| B044	 | desiccation	 | no - good 	  | no - good	  | no			| 1815		 	 |
| B038   | desiccation	 | no - good 	  | no - good	  | no			| 1100		 	 |
| B041   | desiccation	 | **yes - bad**  | no - good	  | **YES**		| 93		 	 |

*note: 8 each treatment*

# Is it worth trying to sequence as much as possible or just choose same number from each group that are most likely to be successful?
_Cutoff are usually based on RIN. Our RIN scores are pretty good and consistent. Concentration is the issue. Do people normally sequence a high and low concentration pool? Or have a cutoff for concentration as well?_

### Getting rid of JUST low quality and separating into low and high concentrations:
_I'm assuming low quality samples are not worth it_

| sample | 	treatment	 | < 500 ng input | < 50 ng input | low quality | Max Input (ng) |
| ------ | ------------- | -------------- | ------------- | ----------- | -------------- |
| B031	 | control   	 | **yes - bad**  | **yes - bad** | no			| 12.6		 	 |
| B047   | control   	 | no - good 	  | no - good	  | no			| 540		 	 |
| B043	 | control   	 | no - good 	  | no - good	  | no			| 585		 	 |
| B039	 | control   	 | no - good	  | no - good	  | no			| 685		 	 |
| B048	 | control   	 | no - good 	  | no - good	  | no			| 775		 	 |
| B037	 | control   	 | no - good 	  | no - good	  | no			| 1410		 	 |
| B033	 | control   	 | no - good 	  | no - good	  | no			| 3175		 	 |

*7 control*
*could get rid of B031, even 6 - 3 low conc. 3 high conc.*

| sample | 	treatment	 | < 500 ng input | < 50 ng input | low quality | Max Input (ng) |
| ------ | ------------- | -------------- | ------------- | ----------- | -------------- |
| B064   | thermal   	 | **yes - bad**  | no - good	  | no			| 110		 	 |
| B030	 | thermal   	 | **yes - bad**  | no - good	  | no			| 142		 	 |
| B034   | thermal   	 | **yes - bad**  | no - good	  | no			| 228		 	 |
| B040   | thermal   	 | **yes - bad**  | no - good	  | no			| 303		 	 |
| B045	 | thermal   	 | no - good 	  | no - good	  | no			| 915		 	 |
| B050	 | thermal   	 | no - good 	  | no - good	  | no			| 1025		 	 |
| B042	 | thermal   	 | no - good 	  | no - good	  | no			| 2850		 	 |

*7 thermal*
*could get rid of one (B064 I guess?) and do the same as with control - 6 total: 3 low, 3 high conc.*
*or could seq all to have most data possible just in case and separate 64,30,34,40 into low pool and 45,50,42 into high pool.*

| sample | 	treatment	 | < 500 ng input | < 50 ng input | low quality | Max Input (ng) |
| ------ | ------------- | -------------- | ------------- | ----------- | -------------- |
| B032	 | desiccation	 | no - good 	  | no - good	  | no			| 870		 	 |
| B026	 | desiccation	 | no - good 	  | no - good	  | no			| 985		 	 |
| B038   | desiccation	 | no - good 	  | no - good	  | no			| 1100		 	 |
| B049	 | desiccation	 | no - good 	  | no - good	  | no			| 1750		 	 |
| B044	 | desiccation	 | no - good 	  | no - good	  | no			| 1815		 	 |
| B063	 | desiccation	 | no - good 	  | no - good	  | no			| 2550 		 	 |
| B046	 | desiccation	 | no - good 	  | no - good	  | no			| 2700		 	 |

*7 desiccation*
*this group is difficult because all have relatively high concentrations. There is not a need for two pools. Does this pose an issue for design if we this were the only group to not be separated into two pools?*
*we could still split into two pools: 32,26,38 in low conc. and 49,44,63,46 in high ?*



### Just getting rid of low quality, there are 7 libraries in each treatment. 


