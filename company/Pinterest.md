# Building a real-time user action counting system for ads 
https://medium.com/pinterest-engineering/building-a-real-time-user-action-counting-system-for-ads-88a60d9c9a

**Aperture**, an in-house data storage and online events tracking service
## user action counts
the count for a Pinner’s past clicks, impressions and other actions on ads
## frequency control 
which sets a maximum number of times an ad is shown to a Pinner

## Fatigue model
Fatigue happens when a Pinner becomes tired of viewing the same ad. This usually has negative impact on CTR (click-through rate). Our ads system has a training pipeline for the fatigue model for pCTR (predictive CTR). 
At the request time, several user counting features are fetched for the user fatigue model. A Pinner’s fatigue is measured at different campaign levels. Our campaign structure has four levels:
Advertisers: the account
Campaigns: houses of ad groups
Ad groups: container of Promoted Pins
Promoted Pins: ads
The required actions are impressions and clicks. First, our ads serving system fetches a Pinner’s past engagement counts over a time range for a list of ads candidates at four campaign levels. Then, the counting features are fed to fatigue models for CTR prediction.

