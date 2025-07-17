# Other Useful Slurm Commands

`scancel (job number)` : cancels a job; you can only cancel your own jobs.

`squeue` : shows the current Slurm queue and all jobs in it.

`squeue --me` : shows only your jobs in the current Slurm queue.

!!! note "How to read squeue"

    A job that is currently running will have a state (`ST`) code of `R`.
    The `NODELIST (REASON)` column will tell you what nodes the job is running
    on, or if it is not yet running, why it is waiting.
    If a job has something like `(Resources)` or `(Priority)` in that column,
    then it’s currently sitting in the queue waiting to be run.
    `(Resources)` means that the job has priority over other jobs in the queue
    and is just waiting on resources to become available, while `(Priority)`
    means that there are other jobs in the queue with a higher priority that
    must be run before that job will run.

`scontrol show job (job number)` : shows detailed job information.

## Submitting Your Script

Once your script is ready, you can submit it using:
```bash
sbatch (job script filename)
```

You will get an output message saying `Submitted batch job (job number)`, which
tells you that your job was successfully submitted.
