Rust-Hydra
Project Summary

Rust-Hydra is a high-performance, Rust-based authentication testing framework inspired by Hydra, redesigned with a modern, streaming, fault-tolerant architecture.
It is built specifically for educational use, CTFs, and authorized lab environments, prioritising correctness, observability, and resumability over raw speed.

Rather than re-implementing fragile protocol stacks, Rust-Hydra uses a modular protocol abstraction and delegates complex authentication logic to proven external tooling where appropriate (e.g. smbclient, evil-winrm), while maintaining full control over concurrency, progress tracking, and state.

Key Capabilities
Asynchronous, concurrent authentication attempts (Tokio)
Modular protocol architecture via a unified Protocol trait
Streaming wordlists (constant RAM usage)
Crash-safe resume & restore
Accurate progress bars with ETA
Stop-on-success support
Protocol autodetection (scheme, port, probe)
Domain-aware Windows authentication
Safe defaults for lockout-prone services
Designed for realistic red-team lab workflows

This project is intended only for CTFs, labs, and explicitly authorized penetration testing.
⚠️ DO NOT USE AGAINST SYSTEMS YOU DO NOT OWN OR HAVE EXPLICIT PERMISSION TO TEST

Features

HTTP form authentication testing
SSH authentication
FTP authentication
SMB (NTLM) authentication
WinRM (HTTP / HTTPS) authentication
Streaming wordlists (no full in-memory loading)
Resume / restore after interruption
Progress bar with ETA
Async multi-threaded engine

Hydra-style workflow and CLI concepts

🛠 Supported Protocols
Protocol	Status
HTTP Forms	✅
SSH	✅
FTP	✅
SMB (NTLM)	✅
WinRM (HTTP/HTTPS)	✅


📦 Installation
git clone https://github.com/kerravon99/rust-hydra.git
cd rust-hydra
cargo build --release

Usage Examples
HTTP Form Authentication
./target/release/rust-hydra http http://10.10.10.10/login \
  -L users.txt \
  -P passwords.txt \
  --user-field username \
  --pass-field password \
  --fail "Invalid login"

SSH
./target/release/rust-hydra ssh 10.10.10.10 \
  -L users.txt \
  -P passwords.txt

SMB (NTLM)
./target/release/rust-hydra auto 10.10.10.5 \
  -L users.txt \
  -P passwords.txt \
  --domain ACME \
  -t 1

WinRM
./target/release/rust-hydra winrm 10.10.10.10 \
  -L users.txt \
  -P passwords.txt \
  --domain CORP \
  --ssl \
  -t 1

Autodetection
./target/release/rust-hydra auto 10.10.10.10 \
  -L users.txt \
  -P passwords.txt

♻️ Resume / Restore

You can safely interrupt execution with Ctrl+C.
Progress is saved automatically.

Resume with:
./target/release/rust-hydra ... --resume

Works across:
Crashes
Network interruptions
Long-running wordlists

🛣 Future Development Goals
Short-Term
Mysql protocol module
Per-protocol attempt delays (--delay)
Output file logging (-o, JSON/CSV)
Improved error classification (network vs auth failure)
Lockout-aware backoff

Medium-Term
SMB post-auth validation (share enumeration)
WinRM post-auth command verification
Credential reuse detection
Per-user attempt limits

Long-Term
Kerberos-aware authentication modes
LDAP / Active Directory support
Credential spraying mode
Distributed execution (multi-node)
Plugin SDK for third-party protocols
Blue-team simulation / detection testing mode

⚖️ Legal & Ethical Disclaimer
Authorized Use Only

Rust-Hydra is intended solely for lawful security testing, including:
TryHackMe CTFs
Hack The Box labs
Your own systems
Explicitly authorized penetration tests
Any use against systems you do not own or have written authorization to test is illegal.

No Warranty
This software is provided “as is”, without warranty of any kind.
The authors assume no liability for misuse, damage, account lockouts, or legal consequences.

User Responsibility
By using this tool, you acknowledge that:
You have proper authorization for all targets

Authentication attacks may trigger:
Account lockouts
Logging and alerts
Service disruption

You accept full responsibility for compliance with applicable laws
Final Warning

If you do not have permission — do not use this tool.
Authorization is not implied. Silence is not consent.
