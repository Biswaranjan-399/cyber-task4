# Task 4 - Firewall Configuration and Testing

## 📌 Objective
Configure and test basic firewall rules to allow or block traffic on Windows Firewall or UFW (Linux).

## 🛠 Tools Used
- *Windows Firewall* (on Windows 10/11)
- *PowerShell* (for testing connectivity)
- *Command Prompt / netsh* (optional)
- *UFW (Uncomplicated Firewall)* (on Linux, optional)

## 📂 Deliverables
- Screenshots of firewall rules added/removed
- Commands or steps used
- Summary of how firewall filters traffic


## 🔹 Steps Performed

### 1. Checked Current Firewall Rules
On Windows:
powershell
netsh advfirewall firewall show rule name=all


### 2. Blocked Inbound Traffic on Port 23 (Telnet)
Added a firewall rule to block Telnet (port 23):
netsh advfirewall firewall add rule name="Block Telnet" dir=in action=block protocol=TCP localport=23


### 3. Tested Rule
Attempted to connect to port 23 locally using PowerShell:
Test-NetConnection -ComputerName 127.0.0.1 -Port 23
Result showed that the connection was blocked.


### 4. Removed Test Rule
Restored the original state by removing the Telnet block rule:
netsh advfirewall firewall delete rule name="Block Telnet"