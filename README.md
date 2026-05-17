# Windows-Linux-Scripting
This lab demonstrates network health monitoring through OS-level scripting on both Windows and Linux platforms. The goal is to create automated scripts that check network configuration and connectivity, saving the results to a log file.

Objectives:

- Create network diagnostic scripts for Windows (Batch) and Linux (Bash)
- Capture IP configuration details
- Perform network connectivity tests
- Save diagnostic results to log files
- Understand cross-platform scripting differences

Technologies Used

Windows: Batch Scripting (.bat)
Linux: Bash Scripting (.sh)
Commands: ipconfig, ping (Windows) | ip, ping (Linux)


Part 1: Linux Setup
Initial Setup
The lab begins by setting up the Linux environment with necessary configuration files.
The setup copies essential bash configuration files:

.bashrc - Bash shell configuration
.bash_profile - Login shell configuration
.inputrc - Input configuration
.profile - Profile settings


Part 2: Windows Network Health Check Script
Script: network_check.bat

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

Host Name: Ethan
Node Type: Hybrid
IPv4 Address: 10.0.0.13
Default Gateway: 10.0.0.1
Physical Address (MAC): 10-FF-E0-B8-39-A5
DNS Servers and DHCP information

Key Features of Windows Script

Creates a tempinfo directory for log storage
Uses ipconfig /all to capture complete network configuration
Pings loopback address (127.0.0.1) to verify TCP/IP stack
Timestamps the log with generation date and time
Pauses at the end to allow user to review output

Part 3: Linux Network Health Check Script
Script: network_check.sh
Script Contents
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

Linux network health log showing:

Multiple network adapters (Ethernet and Ethernet 3)
IPv4 addresses (10.0.0.13 and 192.168.56.1)
IPv6 addresses
Default gateway information
Loopback ping test results with 0% packet loss



Key Features of Linux Script

Uses shebang (#!/bin/bash) to specify bash interpreter
Uses mkdir -p to create directory (no error if exists)
Leverages $(date) command substitution for timestamp
Uses ping -c 4 to limit ping count (prevents infinite loop)
Outputs network configuration using ipconfig command


