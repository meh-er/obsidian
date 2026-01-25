---
tags:
  - OSSP
---
### Application scenario
Consider an application where the volume of data is not known beforehand

Example: Store info of the people you meet during office hour
- The number of people is not known 
- Each person may provide different amount of info

Best Solution:  Allocate memory at **runtime** as per **demand**
Advantages: Optimal memory consumption depending on the current state of the application.

##### Arrays in C: common mistakes
* Array size should normally be a constant
* 