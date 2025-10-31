This is optional! You don't even have to care about this if you don't use NSCC regularly!

Are you tired of turning on VPN, opening Microsoft Authenticator, putting in the jumphost password, and then putting in the NSCC password... and doing this everytime if your laptop (accidentally) sleeps? SSH tunnelling is here to save your day.

It's super easy to setup, and very useful! Once you logged into NSCC:
1. `tmux new-session -s tunnel`
2. Once in the tmux session, run 
```bash
curl -Lk 'https://code.visualstudio.com/sha/download?build=stable&os=cli-alpine-x64' --output vscode_cli.tar.gz
tar -xf vscode_cli.tar.gz
./code tunnel --accept-server-license-terms
```
3. Choose the GitHub option
4. Open the link in your local browser, connect it with your GitHub
5. Name your machine `nscc`
6. On the control panel, press "Remote-Tunnels: Connect to Tunnel" -> GitHub -> Login to GitHub -> `nscc`

Tada! Now, whenever you want to login, you can just do step 6, without needing to connect to VPN or inputting password, etc etc.