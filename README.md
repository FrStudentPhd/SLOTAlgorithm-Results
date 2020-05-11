# SLOTAlgorithm-Results
This folders contains all the results presented for the submission to DSD2020. No disclosure with authors identities or their affiliation can be recovered from here.

There is one folder for each workload (from 6 to 15 tasks) and one additional with the overall.
Each folder contains (i) two csv files (one for SLOT and MILP, one for HEFT-NF and MILP) and (ii) the Cumulative Distribution Function (CDF) graph. The 'overall' folder contains the CDF only, because it is based on the concatenation of previous CSV files.


How to read csv files
1. The first table gives all the tested instances. Columns are:

- NAME -> unique name of the instance
- T -> number of tasks
- E -> number of edges
- MMIP -> optimal makespan found by MILP
- MSLOT -> makespan found by SLOT algorithm
- MHEFT-NF -> makespan found by HEFT-NF algorithm
- UMIP -> time taken by MILP in micro-seconds
- USLOT -> time taken by SLOT in micro-seconds
- UHEFTNF -> time taken by HEFT-NF in micro-seconds
- S boolean. True if the scheduling found by SLOT(HEFT-NF) is identical to the scheduling found by MILP
- M boolean. True if the makespan found by SLOT(HEFT-NF) is up to 1% different by the one found by MILP

2. The second table (present at the end of csv file) resumes the differences.
There is a line for each combination number of tasks/number of edges of the DAG.
Columns are: 
- T -> number of tasks
- E -> number of edges
- N -> total number of tested instances with such number of tasks and edges
- SchedDiff -> number of instances for which the scheduling found by SLOT(HEFT-NF) are different from the one found by MILP.
- SchedMkspDiff -> number of instances for which the makespans found by SLOT(HEFT-NF) is up to 1% different by the ones found by MILP

Other columns only refer to the instances for for which the makespans found by SLOT(HEFT-NF) is up to 1% different by the ones found by MILP. Values are expressed in terms of percentage from makespan found by MILP.
- MinMkspDiff -> the shorter difference between the makespans 
- MaxMkspDiff -> the larger difference between the makespans 
- AvgMkspDiff -> the more average difference between the makespans 
- StdMkspDiff -> the standard deviation difference between the makespans 

3. The last table (at the very end of csv file) resumes the execution times, in micro-seconds, of OUR implementations.
Columns are:
- T -> number of tasks
- E -> number of edges
- N -> total number of tested instances with such number of tasks and edges
- MinMipTime -> minimum execution time taken by MILP
- MaxMipTime -> maximum execution time taken by MILP
- AvgMipTime -> average execution time taken by MILP
- StdMipTime -> standard-deviations of MILP execution timing
- MinSlotTime -> minimum execution time taken by SLOT
- MaxSlotTime -> maximum execution time taken by SLOT
- AvgSlotTime -> average execution time taken by SLOT
- StdSlotTime -> standard-deviations of SLOT execution timing
- MinHeftNFTime -> minimum execution time taken by HEFT-NF
- MaxHeftNFTime -> maximum execution time taken by HEFT-NF
- AvgHeftNFTime -> average execution time taken by HEFT-NF
- StdHeftNFTime -> standard-deviations of HEFT-NF execution timing
