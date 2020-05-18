# SLOTAlgorithm-Results
This folders contains all the instances and the results presented for the submission to DSD2020. No disclosure with authors identities or their affiliation can be recovered from here.

We specify to the reader that, as it can be seen from the history of this git repository, we first committed a summary of our results. Secondly, as an addition, we committed all the files that contain the topology of our input graphs.

Following a brief explanation of each folder: 

Folder WORKLOADRESULTS

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


Folder TESTBENCH

It contains all the graph instances in json format.
This directory contains thousands of json files whose format is:

tests/xc7s25/tXX/eYYY/r0.1R0.5d10.0D50.0/ZZZ.app.json

where:
- 06 <= XX <= 15 is the number of tasks,
- 000 <= YYY is the number of internal edges in the DAG (edges except
source and sink incidents)
- 001 <= ZZZ <= 100 is the seed of the random generator used to generate
the application

app.json specifies the application using the following json fields:
- name -> the name of the instance according to the rules above mentioned
- task -> for each task, fields "resource" and "duration" are specified. "resource" field is an array which has lenght 3 in this benchmark (LEs, dsps, brams). "duration" is the task execution time expressed in milliseconds. Note that source and sink are dummy tasks from resource and duration point of view. 
- adjacency -> for each task a list that contains task's successors is given. Adjacency lists follow the order of tasks.

EXAMPLE

{ "name": "xc7s25 t06 e000 r0.1 R0.5 d10.0 D50.0 s001", "task": [ { "resource": [ 0, 0, 0 ], "duration": 0.0 }, { "resource": [ 6075, 21, 9 ], "duration": 39.848674824672422 }, { "resource": [ 4932, 13, 22 ], "duration": 30.936674559612236 }, { "resource": [ 9712, 30, 8 ], "duration": 23.740040935787903 }, { "resource": [ 8566, 17, 7 ], "duration": 16.253878259600562 }, { "resource": [ 0, 0, 0 ], "duration": 0.0 } ], "adjacency": [ [ 1, 2, 3, 4 ], [ 5 ], [ 5 ], [ 5 ], [ 5 ], [ ] ] }

In this example, there are 6 tasks.
Task 0 is the source, tasks 1, 2, 3, 4 depend from it and they are parallel. 
All tasks 1, 2, 3, 4 have a dependency to task 5, that is the sink. Task 3, for example, requires 9712 Logic Elements, 30 dsps and 8 bram blocks. It has a duration of 23.74 microseconds.

File "unusedGraphs.txt" contains a list of apps that are not taken into account in this analysis. We put a timer to MILP formulation. If such timer expires without the completion of MILP formulation, the application is discarded. This is to limit cases for which calculating an exact solution is too long.
