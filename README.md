Generic SSH connection library supporting arbitrary jump chains with per-hop authentication (keys, keyboard-interactive 2FA, GSSAPI/Kerberos) and strict hostkey validation.
Built on Paramiko, structured around transport orchestration and pluggable auth strategies, not SSH CLI emulation.
Targets bastions, HPC and locked-down enterprise environments.

<!-- good idea Yes, but only if you scope it to “reliable hop chain + auth plugins + hostkey policy” and do not chase full OpenSSH feature parity.
Main risk: edge cases (per-hop auth quirks, ProxyCommand variants, agent forwarding, hostkey UX) dominate time; value is highest for bastion-heavy/HPC automation. -->
