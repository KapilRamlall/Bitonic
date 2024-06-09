
# Requirements to run

Ensure that the MPICH module is loaded. If it is not, the script will stop.
Ensure the g++ is installed.

Run this after downloading the attached script:
```
bash ./build.sh
```

Changes to the Makefile:


```
OMPFLAG = 
CC = g++
MPI_CC = mpic++
CFLAGS = -Ofast
```

# Notes on outcome

In my attempt to set up a virtual cluster for computing tasks, I made several efforts, totaling nine, to get it up and running. Unfortunately, success was elusive, achieved only once in the early stages of my endeavor.

On the third try, after multiple adjustments to configurations, the cluster finally came online. However, it wasn't smooth sailing. Unexpectedly, the nodes, essential for distributing tasks, encountered issues connecting to the Slurm scheduler. This left them idle, rendering the cluster ineffective.

In an effort to salvage the situation, I ran the Bitonic Sort program with optimization flags on the head node. While it did run successfully, it took 899 milliseconds to complete. Through this experience, I gained insights into the significance of optimization flags such as "-Ofast" and "mpic++" in enhancing program performance. These flags, when used appropriately, can significantly improve the efficiency of computational tasks.
Attempting to rectify the node connectivity issue, I tried to redo the project. Unfortunately, this led to a permission error that proved troublesome to resolve, despite my efforts to troubleshoot it.

Despite the challenges encountered, this project provided valuable insights. It underscored the importance of understanding system variables when entering a shell environment and highlighted the intricate workings of components like Slurm and Warewolf in managing a cluster. Through troubleshooting, I gained a deeper understanding of the components necessary for a Slurm configuration file.
