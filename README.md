# Windows-Linux-Scripting

This lab demonstrates network health monitoring through OS-level scripting on both Windows and Linux platforms. The goal is to create automated scripts that check network configuration and connectivity.

## 📋 Objectives

- Create network diagnostic scripts for Windows (Batch) and Linux (Bash)
- Capture IP configuration details
- Perform network connectivity tests
- Save diagnostic results to log files
- Understand cross-platform scripting differences

## 🛠️ Technologies Used

| Component | Technology |
|-----------|-----------|
| **Windows** | Batch Scripting (.bat) |
| **Linux** | Bash Scripting (.sh) |
| **Windows Commands** | `ipconfig`, `ping` |
| **Linux Commands** | `ip`, `ping` |

---

## Part 1: Linux Setup

### Initial Setup

The lab begins by setting up the Linux environment with necessary configuration files. The setup copies essential bash configuration files:

- `.bashrc` - Bash shell configuration
- `.bash_profile` - Login shell configuration
- `.inputrc` - Input configuration
- `.profile` - Profile settings

---

## Part 2: Windows Network Health Check Script

### Script: `network_check.bat`

```batch
mkdir tempinfo

echo ========================================== > tempinfo\myIPhealth.txt
echo     WINDOWS NETWORK CARD HEALTH LOG     >> tempinfo\myIPhealth.txt
echo     Generated on: %date% %time%         >> tempinfo\myIPhealth.txt
echo ========================================== >> tempinfo\myIPhealth.txt
echo. >> tempinfo\myIPhealth.txt

ipconfig /all >> tempinfo\myIPhealth.txt

echo. >> tempinfo\myIPhealth.txt
echo ========================================== >> tempinfo\myIPhealth.txt
echo     LOOPBACK NETWORK CARD PING CHECK    >> tempinfo\myIPhealth.txt
echo ========================================== >> tempinfo\myIPhealth.txt
echo. >> tempinfo\myIPhealth.txt

ping 127.0.0.1 -n 4 >> tempinfo\myIPhealth.txt

echo Script Execution Complete. Results saved in: tempinfo\myIPhealth.txt
pause
```

### Sample Output

```
Host Name: Ethan
Node Type: Hybrid
IPv4 Address: 10.0.0.13
Default Gateway: 10.0.0.1
Physical Address (MAC): 10-FF-E0-B8-39-A5
DNS Servers and DHCP information
```
<img width="1261" height="969" alt="Screenshot 2026-05-16 203347" src="https://github.com/user-attachments/assets/109c8390-4ee0-4e49-ae7c-c2a1b9c7c5b9" />

### Key Features

✅ Creates a `tempinfo` directory for log storage  
✅ Uses `ipconfig /all` to capture complete network configuration  
✅ Pings loopback address (127.0.0.1) to verify TCP/IP stack  
✅ Timestamps the log with generation date and time  
✅ Pauses at the end to allow user to review output  

---

## Part 3: Linux Network Health Check Script

### Script: `network_check.sh`

```bash
#!/bin/bash

mkdir -p tempinfo

echo "==========================================" > tempinfo/myIPhealth.txt
echo "     LINUX NETWORK CARD HEALTH LOG     " >> tempinfo/myIPhealth.txt
echo "     Generated on: $(date)            " >> tempinfo/myIPhealth.txt
echo "==========================================" >> tempinfo/myIPhealth.txt
echo "" >> tempinfo/myIPhealth.txt

ipconfig >> tempinfo/myIPhealth.txt

# Note: '-c 4' limits the ping to 4 packets, preventing an infinite loop
echo "" >> tempinfo/myIPhealth.txt
echo "==========================================" >> tempinfo/myIPhealth.txt
echo "     LOOPBACK NETWORK CARD PING CHECK  " >> tempinfo/myIPhealth.txt
echo "==========================================" >> tempinfo/myIPhealth.txt
echo "" >> tempinfo/myIPhealth.txt

ping -c 4 127.0.0.1 >> tempinfo/myIPhealth.txt

echo "Script Execution Complete. Results saved in: tempinfo/myIPhealth.txt"
```
<img width="571" height="366" alt="Screenshot 2026-05-16 222929" src="https://github.com/user-attachments/assets/b366d357-e2ab-44c8-bdb4-88535dab3dd8" />
### Sample Output
<img width="1577" height="922" alt="Screenshot 2026-05-16 222738" src="https://github.com/user-attachments/assets/b8f9ff29-ed6a-428d-bead-ed528e73bfc0" />

The Linux network health log shows:

- Multiple network adapters (Ethernet and Ethernet 3)
- IPv4 addresses (10.0.0.13 and 192.168.56.1)
- IPv6 addresses
- Default gateway information
- Loopback ping test results with 0% packet loss

### Key Features

✅ Uses shebang (`#!/bin/bash`) to specify bash interpreter  
✅ Uses `mkdir -p` to create directory (no error if exists)  
✅ Leverages `$(date)` command substitution for timestamp  
✅ Uses `ping -c 4` to limit ping count (prevents infinite loop)  
✅ Outputs network configuration using `ipconfig` command  

---

## 📝 Summary

Both scripts provide comprehensive network diagnostics for their respective platforms, capturing essential network information and connectivity status. The key difference is the command syntax and shell-specific features.

---

## Technical Comparison: Windows vs Linux

| Feature | Windows (.bat) | Linux (.sh) |
|---------|---|---|
| **Script Extension** | .bat | .sh |
| **Interpreter Declaration** | Not required | #!/bin/bash |
| **Directory Creation** | mkdir tempinfo | mkdir -p tempinfo |
| **Date/Time** | %date% %time% | $(date) |
| **IP Configuration** | ipconfig /all | ipconfig or ip addr |
| **Ping Limit** | -n 4 | -c 4 |
| **Output Redirection** | > and >> | > and >> |
| **New Line** | echo. | echo "" |
| **User Pause** | pause | Not typically used |

---

## Key Learning Outcomes

- **Cross-Platform Scripting**: Understanding syntax differences between Windows Batch and Linux Bash
- **Network Diagnostics**: Using built-in OS tools to check network health
- **File I/O**: Redirecting command output to files for logging
- **Script Automation**: Creating reusable scripts for system administration tasks

---

## Best Practices

✅ Always limit ping packets to prevent infinite loops  
✅ Add timestamps to logs for troubleshooting  
✅ Use meaningful file names and directory structures
