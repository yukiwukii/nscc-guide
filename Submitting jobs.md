In a nutshell, how NSCC work is similar to a mafia organization:
1. You have a **job** that needs to be run.
2. You need to write some details about the job, in the **job file**.
3. After writing the job file, you need to queue for a worker.
4. You pass the job file to the worker, who will do the dirty job for you.
5. While the worker is running the job, you can check on their progress.
6. Once they are done, they will report back the result of the job, whether it is successful or not, along with the detailed logs.

**Note:** For your AI job to run fast, you need GPU. However, the GPU is only available once you submit the job (in the **compute node**). The place you spawn when you login to NSCC is the **login node**. There is *no* GPU there. So, don't run your scripts with `python my_script.py`! Always write a job file and submit it.
## Basics of a Job File
The job file is written in shell script. You may choose either `.pbs` or `.sh` extension.
```bash
touch job.pbs # Create a job file
nano job.pbs # If you are using terminal to edit files, for whatever reason
# If you are using VSCode, find the job.sh file on the directory panel
```
On top of the `job.pbs` file, you need to enter the details.
```bash
#!/bin/bash

#PBS -q normal
#PBS -j oe
#PBS -l select=1:ncpus=16:ngpus=4
#PBS -l walltime=20:00:00
#PBS -N my_first_nscc_job
#PBS -P personal-<nscc_username>
```
Details:
- `-q` determines which queue you want to use. Just use normal.
- `-j oe` combines the output and the error files into one file.
- `-l select=1:ncpus=16:ngpus=4` requests 16-core CPU and 4-core GPU. This is **important**!! You need to request for GPU. If not, your AI job will run **very slowly**.
- `-l walltime=20:00:00` your job will exit after 20 hours, if it has not completed.
- `-N` setup your job name. This can be anything, but it should be descriptive.
- `-P` put it as personal-nscc_username i.e. personal_nady0006

Below the details (in the same job file!), you need to activate your environment + specify which script to run.
```bash
module load miniforge3 # Activate conda
module activate my_env # Activate venv
cd my_folder # (Optional) Move to a different folder
python my_script # Run the script
```

Finally, once you are done, `qsub job.pbs` will submit your job to the queue.
## Checking your Jobs
To check how your jobs are doing, use the `qstat` command. You will get a table of your running jobs.
> [!NOTE] **Help!** qstat does not return anything.
> Your job is either finished, or died. Check your job submission history using `qstat -H`.

The `s` header on the table stands for status. There are a few status your job may have:
- `q` queueing.
- `r` running. This is good. It's processing.
- `e` exiting. Either finished, or died.

>[!NOTE] **Help!** My job is eternally queueing.
>You need to increase/decrease the ngpu requested and/or the walltime. Use `qstat -s` command to see why your job is queueing. See [Min-maxing the queue](/Min-maxing%20the%20queue.md) for how to game the system.
## Checking the Results of your Jobs
The results of the job is `<job_name>.o<job_id>`.

In here, you can find all the output of your script (the one that would be outputted to the terminal otherwise). **Important Note:** You must wait until the job finishes / dies to see the output. If you need to see the output immediately (to monitor the progress or something), you can create an [interactive job](/Running%20jupyter-notebooks.md) instead.
## Deleting your Jobs
To delete the jobs, find the job_id with `qstat`, and delete it by running `qdel <job_id>`.