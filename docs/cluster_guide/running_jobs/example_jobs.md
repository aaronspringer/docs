# Example submission scripts

The final component of an sbatch script is the set of commands that will be run
after the slurm parameters are parsed.
These can be any shell command, e.g., loading modules, setting environment
variables, or calling executables.
Let's say you've created an [MPI executable](../../software/c.md); you could
use the following script to submit this job to the scheduler requesting 48 cores
on a single CPU node:

```bash title="hello_world_slurm.sh"
#!/bin/bash
#SBATCH -J HELLOWORLD    # job name
#SBATCH -o log_slurm.o%j # output and error file name (%j expands to jobID)
#SBATCH -n 48            # total number of tasks requested
#SBATCH -N 1             # number of nodes you want to run on
#SBATCH -p bsudfq        # queue (partition)
#SBATCH -t 00:05:00      # run time (hh:mm:ss) - 5 minutes in this example

# (optional) Print some debugging information
echo "Date              = $(date)"
echo "Hostname          = $(hostname -s)"
echo "Working Directory = $(pwd)"
echo ""
echo "Number of Nodes Allocated  = $SLURM_JOB_NUM_NODES"
echo "Number of Tasks Allocated  = $SLURM_NTASKS"
echo ""

# Run the program
module load borah-base openmpi/4.1.3/gcc/12.1.0
mpirun -n 48 ./hello_world
```

As another example, here’s a job script requesting a GPU node and then running
`nvidia-smi` to see information about the GPU:

```bash title="gpu_slurm.sh"
#!/bin/bash
#SBATCH -J NVIDIASMI        # job name
#SBATCH -o log_slurm.o%j    # output and error file name (%j expands to jobID)
#SBATCH -c 1                # cpus per task
#SBATCH -N 1                # number of nodes you want to run on
#SBATCH --gres=gpu:1        # request a gpu
#SBATCH -p gpu              # queue (partition)
#SBATCH -t 00:05:00         # run time (hh:mm:ss)

# (optional) Print some debugging information
echo "Date              = $(date)"
echo "Hostname          = $(hostname -s)"
echo "Working Directory = $(pwd)"
echo ""
echo "Number of Nodes Allocated  = $SLURM_JOB_NUM_NODES"
echo "Number of Tasks Allocated  = $SLURM_NTASKS"
echo "GPU Allocated              = $SLURM_JOB_GPUS"
echo ""
nvidia-smi
```

These commands will differ from job to job.
If you need any help setting up a submission script, please don't hesitate to
email us at ResearchComputing@boisestate.edu--we're happy to help!

Once your script is ready, you can submit it using
```
sbatch (job script filename)
```
You will get an output message saying `Submitted batch job (job number)`, which
tells you that your job was successfully submitted.