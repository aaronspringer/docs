# Timing, Output, and Naming

The scheduler relies on the submission script to estimate how long a job
will take. You can set a time limit for your job with the following line:
```bash
#SBATCH -t DD-HH:MM:SS
```
For example, one day and twenty hours would be `1-20:00:00`, twelve hours and
fifty minutes would be `12:50:00`, and a half hour would be `00:30:00`.
This time limit is a hard stop for your job, and when it is reached, your job
will be terminated regardless of whether your script has finished.
Ideally, you want to choose a time limit that is just longer than you expect
your job to run. If no time limit is specified, a default of twelve hours will be set.

You can update the job's time limit by running:
```bash
scontrol update job JOBID timelimit=NEWTIMELIMIT
```
where `JOBID` is the job id of the job you want to update and `NEWTIMELIMIT` is
the new time limit.

!!! note "Updating time limits"

    You will only be able to increase the time limit of a job that is still
    queued. Once a job is running, you will only be able to _decrease_ the
    time limit.

    If you need more time on a currently running job, please email us at
    researchcomputing@boisestate.edu.

If you want to change the name of the file where the script output is logged,
you can use the following line:
```bash
#SBATCH -o (output file name)
```
This will redirect any terminal output that the job produces to a file in the
current working directory with the name you specify; if this parameter is
omitted, the output is logged to a text file named `slurm-(job number).out`.

If you want to give your job a unique name to identify it in the `squeue`
output, you can do so by adding the following line to your script:
```bash
#SBATCH -J (job name)
```

Finally, if you want to make sure that your job has exclusive access to an
entire node--regardless of how many resources it is using--you can add the
following line to your submission script:
```bash
#SBATCH --exclusive
```
This will claim the entire compute node (and all its resources) for just your
job, stopping other jobs from running on the node. This is useful if you’re
actually utilizing all 48 cores (on Borah) and/or a significant portion of the
node’s memory, but it can make the job take a little longer to get through
the queue.
