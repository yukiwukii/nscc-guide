Conventional wisdom says that if you want your job to stop queueing and start running, you should probably reduce the resources requested. This is false. Sometimes, you should **increase** the resources requested instead.

There are 6 main queues for GPU.

| Queue Name | Description                                                                   |
| ---------- | ----------------------------------------------------------------------------- |
| g1         | ngpus = 1, walltime = 02:00:01 hours to 24:00:00 hours                        |
| g2         | ngpus = 2 or 3, walltime = 02:00:01 hours to 24:00:00 hours                   |
| g3         | ngpus = 4  (1 node), walltime = 02:00:01 hours to 24:00:00 hours              |
| g4         | ngpus = 5 to 256 (2 to 64 nodes), walltime = 02:00:01 hours to 24:00:00 hours |
| glong      | ngpus = 1 to 64 (1 to 16 nodes), walltime = 24:00:01 hours to 120:00:00 hours |
| gdev       | ngpus = 1 to 4  (1 node), walltime = 00:00:01 hours to 02:00:00 hours         |

If your job is stuck at queueing, use the `qstat -s` command to see why it's stuck. More likely than not it is because you have reached the limit of jobs in **that queue**. So, just delete the job from the queue using `qdel`, and then submit again after increasing / decreasing the ngpus and walltime, such that it will go to **a different queue**.