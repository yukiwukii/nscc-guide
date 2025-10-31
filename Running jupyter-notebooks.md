There are two things you need:
1. A terminal multiplexer, like `tmux` or `screen`
2. An interactive job
## Terminal Multiplexer
Have you ever been in a situation where you are running a script, and you cannot close your laptop because it would stop the program? A terminal multiplexer solves this! Basically, you can create a terminal session that will **never close**. 

I personally use `tmux`, and it comes pre-installed with your NSCC account.
```bash
tmux new-session -s my_session # Create a new terminal
tmux ls # List of running terminals
tmux a -t my_session # Enter my_session terminal
tmux kill-session -t my_session # Delete the my_session terminal
```
Once you are on a `tmux` session, you can exit the session by pressing control (not command!) + B. Check this tmux cheatsheet for other controls. TODO: Add the cheatsheet.
## Interactive Session
Submitting the job file using `qstat`, you will only see the output after the job is done. However, if you need to monitor the progress, you can submit an interactive session instead. Just change `qstat <job_file>` to `qstat -I <job_file>`. In the mafia analogy, this is equivalent of you doing the dirty job yourself, instead of asking for a worker.

After your job finishes queueing, you will enter the compute node! This is where the GPU lives! In here, you don't need to submit the job, you can just run the python file directly, just like a personal computer. 

However, for some whatever reason, once you enter the interactive session, they won't run the submitted job automatically. You have to run it again with `./<job_file>`.
## Detailed Steps
1. [[Setting up an environment|Create your environment]]
	- In addition to the above, you need to install `ipykernel` with `conda install ipykernel` with your environment activated.
	- You need to also install jupyter notebook using `pip install notebook`, if you haven't.
2. Create a tmux session with `tmux new-session -s jupyter`
3. Inside the jupyter notebook, you need to run an interactive session.
	- You can run any job file, just make sure that the wall-time and the GPU requested is sufficient for your jupyter notebook.
4. In the interactive session, you need to re-activate your environment and `cd` to your directory.
5. Run `jupyter-notebook --no-browser --ip=[0.0.0.0](https://0.0.0.0/) --port 8888`
6. After a while, you will get something like `http://x1000c0s7b0n1:8888/tree?token=...`. The x100c0... thing is your GPU id. Copy paste this **entire** link, including the token.
7. Open your jupyter notebook on VSCode. Press the "Change Kernel" on the top right corner. Press "Select other kernel" -> "Existing Jupyter Server". Copy paste the link from step (6).
8. Done! Check if cuda can be seen with `import torch` and `print(torch.cuda.is_available())`. Pray that the output is `True`.







