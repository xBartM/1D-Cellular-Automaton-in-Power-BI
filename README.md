# 1D Cellular Automaton in Power BI

## Table of contents
* [General info](#general-info)
* [Glossary of Terms](#glossary-of-terms)
* [Functionality](#functionality)
* [Limitations](#limitations)

## General info

This Power BI report enables the user to traverse any[^1] conceivable ruleset within 1D Cellular Automaton domain. Logic behind it is written using Power Query M formula language.  


| <img src="README/rule30.PNG" /> | 
|:--:| 
| *Rule 30, two states, three neighbours* |

| <img src="README/threestate.PNG" /> | 
|:--:| 
| *Rule 3500019999922, three states, three neighbours* |

| <img src="README/fiveneighbours.PNG" /> | 
|:--:| 
| *Rule 2294967786, two states, five neighbours* |

## Glossary of Terms

| Term | Meaning |
|:-----|:--------|
| Edge of Chaos | Value of Langton's Parameter where the most interesting patterns can emerge. Note that this is not always the case and there are  exceptions. |
| Langton's Parameter | Fraction of all neighbourhood patterns, within the realm of a single rule, that don't map to quiescent state (quiescent state is hardcoded to 0, but can be changed in Power Query Editor).|



## Functionality

This template requires the user to enter parameters as per the following screen (it is highly encouraged to start with default values):

| <img src="README/parameters.PNG" /> | 
|:--:| 
| *First launch parameter screen* |

| Parameter | Meaning |
|:----------|:--------|
| MaxGen    | Number of generations of cellular automaton to compute for each rule. |
| NeighbourhoodSize | How many cells in one direction are considered to be neighbours of current cell. |
| PossibleStates | Number of states a cell can be in. | 
| RuleStart | First rule to compute. |
| RuleEnd   | Last rule to compute. Every rule between RuleStart and RuleEnd will be computed (susceptible to Langton's Parameter constraints). |
| Seed | Starting generation. |
| WorldLength | How many cells in one direction away from position 0 should be computed. |
| MinLangtonsParameter | Rules that exhibit Langton's Parameter lesser than this value won't be computed. |
| MaxLangtonsParameter | Rules that exhibit Langton's Parameter greater than this value won't be computed. |

After the initialization of the report one can fine tune the parameters in Power Query Editor whilst looking at the preview of Stats table. 


| <img src="README/stats.PNG" /> | 
|:--:| 
| *Stats table* |

| CountType | Meaning |
|:----------|:--------|
| LoadedRules | Number of rules that will be computed.|
| PossibleRules | Number of all rules possible given current values of NeighbourhoodSize and PossibleStates. |
| LoadedRows | Number of rows that will be loaded. This value can be used to approximate the time needed to load the data. |
| EdgeOfChaos | Explained in [Glossary](#glossary-of-terms). |
| Rest of the fields | Explained in [Functionality](#functionality). |

# Limitations

* Default values for MaxGen and WorldLength parameters are tailored to Power BI Scatter Chart limitations so that no more than 3000 points are possible within single world;
* Rule values are subject to Int64 size limit (which can be reached easily with just 4 states);
* The speed of calculations is a **MAJOR** problem since Power Query does not natively support access to previous/next rows needed to recognize pattern for the next state of the cell;

[^1]: world wrap and seed randomization are not supported
