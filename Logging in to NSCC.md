## 1. Account Creation
 First thing first, you need to create an account for NSCC. Link is [here](https://user.nscc.sg/saml/index.php).
- Note that you must be a student in one of the following institutions: NUS, NTU, ASTAR, SUTD, TCOMS, SMU, SIT, SP, TP and RP.

Then, you need to set a new password. Keep this password safe. You'd need to change your password every 90 days, but NSCC will send you a reminder 9 days before it expires. Take note your username too. Look at "Your NSCC is account is **username**".
## 2. VPN Setup
You need to be connected to your institution's network to access NSCC. For NTU students, this is NTUSECURE. If you are outside, you can download a VPN. 
- NTU users can download it [here](gate-student.ntu.edu.sg). 
- If you are from other institutions other than NUS, NTU, SUTD, or A-STAR, you need to download NSCC VPN. Detailed steps are in page 8 of [this document](https://help.nscc.sg/wp-content/uploads/2024/05/NSCC-Introductory-Workshop-Practical-ASPIRE2A.pdf). 

**SPECIAL FOR NTU STUDENTS:** Email hpcsupport@ntu.edu.sg requesting for HPCC jumphost access. Give them your NSCC username. 
- If you are working in a lab, you should ask other lab members if the lab has a jumphost set up. If so, you can instead use the lab's jumphost.
- You only need a jumphost if you want to access NSCC outside of campus!
## 3. Logging In with Terminal
**FOR STUDENTS OUT OF CAMPUS:** Make sure you are on VPN.
**SPECIAL FOR NTU STUDENTS:** Access your jumphost first.
```bash
# ACCESSING JUMPHOST
ssh -X your_ntu_username@172.21.26.100 # If you are using HPCC jumphost
# Enter your NTU password.

ssh -X jumphost_username@jumphost_ip # If you are using lab's personal jumphost
# Enter lab's jumphost password
```

**FOR EVERYONE**:
```bash
ssh nscc_username@aspire2antu.nscc.sg # For NTU
ssh nscc_username@aspire2a.nus.edu.sg # For NUS
ssh nscc_username@aspire2a.a-star.edu.sg # For A-STAR
ssh nscc_username@aspire2a.sutd.edu.sg # For SUTD
ssh nscc_username@aspire2a.nscc.sg # For everyone else

# Enter your NSCC password.
```

> [!TIP]
> You can combine the jumphost + NSCC access into a one-liner.
> `ssh -J jumphost_username@jumphost_ip nscc_username@aspire2antu.nscc.sg`

If you are successful, you will see **Welcome to NSCC Aspire2A System**. It can take a while to load, so be patient!

## 4. Integration with VSCode
The best way to write and edit code on NSCC is using vim. However, if you are not a `:wq` enthuasist (like me), your next best option is VSCode.

1. You first need to download the Remote-SSH extension on VSCode.
2. Using the command panel (command + shift + P), open `Remote-SSH: Open SSH Configuration File`.
3. Create a config file under `Users/` directory.
4. Paste this in: 
```bash
Host my_nscc
  HostName aspire2antu.nscc.sg
  ProxyJump jumphost_username@jumphost_ip
  User nscc_username
```
5. Using the command panel again, open `Remote-SSH: Connect to Host`. Click `my_nscc`, enter jumphost password, enter NSCC password.
6. Wait until VSCode finishes downloading the server into your NSCC account. This can take quite a while.
	- If NSCC decides to die, this is very normal. Keep trying until it works.
	- If it still doesn't work, look at tunnelling.

If you are successful, congratulations! You don't have to log in via terminal (Step 3) anymore. From now on, whenever you want to access NSCC, you just need to do step 4.5 (Pressing `Remote-SSH: Connect to Host`).

>[!Tip]
> If you like GUI, you can access NSCC using the VSCode sidebar. Find the `Remote Explorer` extension. `my_nscc` should be under the SSH dropdown. You can just press the $\rightarrow$ icon to connect to NSCC in the current window.
