# Attack-Chain-Step-by-Step
Pass-the-Hash via WinRM (Lab Exercise)
# Pass-the-Hash via WinRM (Lab Exercise)

This repo documents a controlled red team lab exercise demonstrating:

- Offline extraction of local NTLM hashes from Windows registry hives (SAM + SYSTEM)
- Pass-the-Hash authentication over WinRM (no password cracking)
- Remote PowerShell session establishment
- Controlled proof of access and cleanup
- Defensive detection and mitigation notes

## Scope / Ethics
This was performed in a **local lab environment** on systems I own and have permission to test.  
No brute forcing, no malware, no destructive actions.

## Attack Chain Summary
1. Export SAM + SYSTEM hives from Windows (admin context)
2. Extract NTLM hashes offline using Impacket `secretsdump`
3. Enable WinRM (lab-only) and validate remote access
4. Authenticate via Pass-the-Hash using Evil-WinRM
5. Verify access with non-destructive commands
6. Clean up and restore secure posture (disable WinRM)

## Why this matters
This technique demonstrates how credential material (NTLM hashes) can be abused to gain remote access without knowing a plaintext password. In enterprise environments, this risk grows when:
- Local admin passwords are reused across endpoints
- NTLM is broadly enabled
- WinRM is exposed and not monitored

## Artifacts
- Full write-up: `docs/pass-the-hash-winrm.md`
- Sanitized command log: `logs/commands_sanitized.md`
- Defensive guidance: `defensive/detection_and_mitigation.md`

## Interview-ready explanation
> “I demonstrated credential compromise by extracting NTLM hashes from the Windows SAM database using SYSTEM-level access. I then successfully performed pass-the-hash authentication over WinRM, achieving remote administrative command execution without knowing or cracking the user’s password. This showed how credential reuse and NTLM trust can enable lateral movement and full system compromise with minimal noise.”
