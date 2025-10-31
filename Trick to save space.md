There are two types of storage in NSCC:
1. Home directory (asp2a-home) -> Max: 50GB
2. Scratch -> Max: 100TB, basically unlimited
You can check your current usage using `myquota` command.

Actually, the 50GB limit is **very** restrictive. You should only use your home directory for important files, like key experimental results, etc. For the rest, you should put it under scratch. Accessing scratch: `cd ~/scratch`.

>[!Caution]
>The `scratch` directory is meant to be temporary, and NSCC may delete your files at any given moment without prior notice! However, it has yet to happen to me. So please be careful and always have a backup on Git.

When you run out of disk quota, you will be **unable to access NSCC via VSCode**. You can investigate which file is taking up space by running `du -h --max-depth=1`. Move this file into scratch.

## What if the biggest file is my conda environment?
This is normal. Sometimes one environment can take up >30 GB of space (damn you PyTorch!). So there's a very nice trick to deal with this.
1. Create `envs` folder under `~/scratch`
2. Create a symlink. `ln -s ~/scratch/envs/<env_name> ~/.conda/envs/<env_name>` (make sure it's always the full path).
Now, you can still access the environment using `conda activate <env_name>` without needing to specify the super long path everytime!

## What if the biggest file is my HuggingFace stuff?
You can set up your default directory for huggingface to scratch.
Put this under your job file (.pbs or .sh):
```bash
export HF_HUB_CACHE=/home/users/ntu/nscc_username/scratch
export HF_HOME=/home/users/ntu/nscc_username/scratch
```
Don't forget to substitute `nscc_username` to your username.