# Requirements to run

Ensure that the MPICH module is loaded. If it is not, the script will stop.
Ensure the g++ is installed.

Run this after downloading the attached script:
```
bash ./build.sh
```
This will generate the random numbers and run once.
To run the program again after this, run this command:
```
bash ./rerun.sh
```

# Changes to the Makefile:

```
OMPFLAG = 
CC = g++
MPI_CC = mpic++
CFLAGS = -Ofast
```

# Notes on build.sh file

In the build.sh file, one will find two ways to run the bitonic.cpp file. This due to my compute nodes not being accessible, and being unable to setup the cluster again after that.

I ran the command
```
mpirun ./bitonic 2>&1 | tee ./run.log
```
This game me a time of approximately 899ms which is what I sent in my run file. I ran this on the head node alone with the given optimization flags.

If my my compute nodes did not have  a Slurm connection error, I would have run:
```
salloc -n 4 -N 2 
prun mpirun ./bitonic 2>&1 | tee ./run.log
```
I asked a friend who also did the virtual cluster to run this code. The output of that is:
```
[test@smshost ~]$ bash build.sh 
mpich is installed.
fatal: destination path 'Bitonic' already exists and is not an empty directory.
mpic++ -Ofast  bitonic_mpi.cpp -o bitonic
Makefile has been updated:
MPI_CC set to mpic++
CFLAGS set to -Ofast
rm -vf generator
removed 'generator'
rm: cannot remove '*.csv': No such file or directory
g++ -g -Wall -fopenmp generator.cpp -o generator

-----------------------Starting Number Generation----------------------

Completed: Generated 1048576 random numbers

------------------------------------------------------------------------

salloc: Granted job allocation 29
[test@compute00 src]$ exit
salloc: Relinquishing job allocation 29
[prun] Master compute host = smshost
[prun] Resource manager = slurm
[prun] Launch cmd = mpirun ./bitonic (family=openmpi4)
Time taken: 276.085213 seconds
VALID BITONIC SEQUENCE
```

This would have resulted in better times, but I do belive that the optimization flags chosen are effective ones. The run of 276.085213 ms is the best run with my script, but I only got the message with the output two houts before the deadline and cannot ask the person for the run.log or take a screenshot.

# Notes on outcome

In my attempt to set up a virtual cluster for computing tasks, I made several efforts, totaling nine, to get it up and running. Unfortunately, success was elusive, achieved only once in the early stages of my endeavor.

On the third try, after multiple adjustments to configurations, the cluster finally came online. However, it wasn't smooth sailing. Unexpectedly, the nodes, essential for distributing tasks, encountered issues connecting to the Slurm scheduler. This left them idle, rendering the cluster ineffective.

In an effort to salvage the situation, I ran the Bitonic Sort program with optimization flags on the head node. While it did run successfully, it took 899 milliseconds to complete. Through this experience, I gained insights into the significance of optimization flags such as "-Ofast" and "mpic++" in enhancing program performance. These flags, when used appropriately, can significantly improve the efficiency of computational tasks.
Attempting to rectify the node connectivity issue, I tried to redo the project. Unfortunately, this led to the notorious permission error that proved troublesome to resolve, despite my efforts to troubleshoot it.

Despite the challenges encountered, this project provided valuable insights. It underscored the importance of understanding system variables when entering a shell environment and highlighted the intricate workings of components like Slurm and Warewolf in managing a cluster. Through troubleshooting, I gained a deeper understanding of the components necessary for a Slurm configuration file.

Although it lacks a run.log file, running the script on any virtual cluster with the necessary prerequisites (see above) should result in this time. I use the prun configuration in the build and run file rather than running with mpirun on the head node which got the time of 899ms.
