# Firewall Task Report

*Tool:* Windows Defender Firewall (Windows 11)  
*Objective:* Add a rule to block inbound traffic on port 23 (Telnet) and demonstrate the effect.

## Steps performed
1. Started a temporary TCP listener on port *23* (for testing):
   - Command used (Admin PowerShell):
     
     $listener = [System.Net.Sockets.TcpListener]::new([System.Net.IPAddress]::Any,23)
     $listener.Start()
     
2. Verified port open:
   - Test-NetConnection -ComputerName 127.0.0.1 -Port 23  
   - Result: TcpTestSucceeded : True
   - Screenshot: screenshots/listener_before_test.png

3. Created inbound Block rule (Windows Defender Firewall):
   - GUI: Inbound Rules → New Rule → Port → TCP → Specific Port 2323 → Block the connection → Name: Block_Telnet_Test 
   - OR PowerShell:
     
     New-NetFirewallRule -DisplayName "Block_Telnet_Test" -Direction Inbound -LocalPort 23 -Protocol TCP -Action Block -Profile Any
     
   - Screenshot: screenshots/rule_list_block.png

4. Verified the rule applied:
   - Test-NetConnection -ComputerName 127.0.0.1 -Port 23  
   - Result: TcpTestSucceeded : False  
   - Screenshot: screenshots/listener_after_block.png

5. Clean up:
   - Removed firewall rule:
     
     Remove-NetFirewallRule -DisplayName "Block_Telnet_Test"
     
   - Stopped listener:
     
     $listener.Stop()
     $listener = $null
     
   - Screenshot: screenshots/rule_deleted.png

## Observations
- The firewall block prevented new inbound TCP connections to the test port when the rule was active.
- Note: If testing on 127.0.0.1 does not reflect firewall blocking on some systems, use the machine LAN IP or test from another device on the same network.

## Conclusion & Recommendations
- Firewalls can quickly block unwanted services (e.g., Telnet) and reduce attack surface.
- For real systems: block unused ports, only allow necessary services, enforce least privilege, and maintain regular firewall rule audits.