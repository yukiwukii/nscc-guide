The easiest way to transfer files is via GitHub. Just create a GitHub repository, and upload all of your files. Then,
```bash
git clone <repository_link>

# Download to NSCC
git pull # Make sure you always pull first to prevent merging issues

# Upload from NSCC
git add <filepath> # To add to stage
git commit -m 'add commit message here' # To commit
git push # Push to remote repository
```

## Alternative: Use SCP
If you have too many files and/or lazy to use git, you can use SCP instead! 
```bash
# From your local terminal (Don't login to NSCC)
## NSCC -> local machine
scp nscc_username@aspire2antu.nscc.sg:<nscc_path> <local_path>
## Local machine -> NSCC
scp <local_path> nscc_username@aspire2antu.nscc.sg:<nscc_path>
```
If you have a large file that will take ages to upload / download, use `tmux`! Read more about `tmux` [here](/Running%20jupyter-notebooks.md).

There are some apps that provide a nice GUI for SCP. On MacBook, you can check out [CyberDuck](https://cyberduck.io/download/). On Windows, I have heard things about Windows-SCP, but I never tried it.

## Alternative to the alternative: Drag & Drop
If you have intergrated with VSCode, you can actually just drag and drop your files from Finder / file manager to the directory list in the VSCode window. It's actually quite intuitive.
>[!Caution]
>This method is **not recommended** if your files are **huge**! This will kill your VSCode server and you may lose progress, or cause some phantom files to appear. Basically don't do this if your files are >100MB.
