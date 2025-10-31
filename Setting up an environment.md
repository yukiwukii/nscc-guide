In the terminal (be it via VSCode or otherwise), your go-to environment manager will be conda. You need to first activate it.
```bash
module load miniforge3
```
You should see (base) before your username. This means conda is activated.
Then, you can create your conda environment as per normal.
```bash
conda create -n my_env python=3.11
conda activate my_env # To activate
conda deactivate # To deactivate
```