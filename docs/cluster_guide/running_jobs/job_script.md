#Job Submission Script

In order to know how many resources you should request for your job, it helps to
understand a little about the different resources.

!!! info "Node vs. CPU vs. task"

    A **node** is a computer or server within the cluster, e.g., the login node
    or a compute node like cpu101.
    When we talk about the node we are talking about the entire machine; this
    encompasses the memory, network card, CPU(s), GPU(s), hard drive, etc.

    A **CPU**, generally, is the processing unit of a computer, but slurm kind
    of fudges this definition to be the sockets, cores, or threads of a CPU.
    [This Slurm resource](https://slurm.schedmd.com/cpu_management.html) provides
    more information.

    A **task** is a part of a job parallelized using a distributed memory model,
    e.g., using MPI.
    For an overview of shared and distributed memory models, please check out
    [Cornell Virtual Workshop: Memory Access](https://cvw.cac.cornell.edu/parallel/memory-access/index).

If you are not sure how many resources to request, in general,  we recommend
requesting 1 node, 1 task, and a full node's worth of cores working on that
task. For the default queue on Borah, this request would look like this:

```
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=48
```

If you are using a distributed memory framework, e.g., MPI, you may want to use
more tasks with one or more core(s) per task.
This can also distribute your job across multiple nodes by setting the nodes
count to greater than one and the tasks count to greater than the number of cores
per node.
We recommend scaling multi-node jobs in increments of the number of cores per
node; e.g., request a number of cores that can be evenly divided by the number
of cores per node ($n_{cores/node} \times N$).

In addtion to nodes and cores, you can also request that your job run on a GPU.
To request a GPU, add the following to your submission script:
```
#SBATCH --gres=gpu:(number of GPUs requested)
```