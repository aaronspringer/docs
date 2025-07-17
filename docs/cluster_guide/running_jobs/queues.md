# Queues

The queue (or partition) parameter tells the scheduler which queue the job
should be submitted to and is specified as follows:
```
#SBATCH -p (partition name)
```
You can view the queues available to you from the command line using `sinfo`.
The following table provides information about the queues on Borah:

!!! warning

    “Preemptable” means that jobs submitted to this queue can be stopped and
    requeued if a higher priority job needs the resources. If the software you
    are using makes use of checkpointing, i.e., writing out intermediate data so
    the job doesn't need to restart from the beginning, you can make the best
    use of these queues.


| Queue    | Node Type | Max Nodes/User | Time limit (days) | Preemptable? | Total nodes |
| :---     | :---      | :---           | :---              | :---         | :---        |
| bsudfq   | CPU       | 8              | 28                | No           | 38          |
| bigmem   | CPU (768 GB of RAM)| 1     | 7                 | No           | 1           |
| short    | CPU       | no limit       | 7                 | Yes          | 39          |
| gpu              | GPU | 2            | 7                 | No           | 6           |
| gpu-l40          | GPU | 1            | 7                 | No           | 2           |
| gpu-p100         | GPU | no limit     | 7                 | No           | 1           |
| gpu-v100         | GPU | 2            | 7                 | No           | 4           |
| shortgpu         | GPU | no limit     | 7                 | Yes          | 9           |
| shortgpu-a30     | GPU | no limit     | 7                 | Yes          | 1           |
| shortgpu-l40     | GPU | no limit     | 7                 | Yes          | 2           |
| shortgpu-p100    | GPU | no limit     | 7                 | Yes          | 1           |
| shortgpu-rtx8000 | GPU | no limit     | 7                 | Yes          | 1           |
| shortgpu-v100    | GPU | no limit     | 7                 | Yes          | 4           |


!!! info "Borah hardware specifications"

    The default queue on Borah is `bsudfq`. Each node in this queue has 48 CPU
    cores and 192GB of memory. See
    [Borah's Specifications](hpc_resources#specifications) for more information.

!!! note "Note about the gpu and shortgpu queues"

    The `gpu` and `shortgpu` partitions have heterogeneous node configurations; the
    `gpu` queue contains nodes with V100 (2/node) and L40 (4/node) GPUs with 48
    and 64 CPU cores, respectively. The `shortgpu` queue contains, in addition to
    the nodes in the `gpu` queue, nodes with A30 (2/node), P100 (2/node), and
    RTX8000 (8/node) GPUs with 64, 28, and 48 CPU cores, respectively.

The above table provides information about the specifications of nodes in
the available queues, but you can also see these resources from the
command-line using sinfo.
The following example queries the node name, CPU cores, memory, and resources
of all the nodes in the `shortgpu` queue:
```bash
sinfo -p shortgpu -o "%n %c %m %G"
```