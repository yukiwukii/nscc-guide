If you are new, don't read this. You will not use this. You should only consult this page when the situation calls for it.

Personally, I used this for `ollama`. I am running an interactive session to run the ollama server, and I need another entry point to that exact compute node to access my ollama server!

1. Find the job id of the running interactive job. `export PBS_JOBID=123456.pbs101`.
2. From the interactive job, take the GPU id (the x100c0... thing).
3. You can now ssh to the compute node using the GPU id with `ssh x100c0...`.