Generic SSH connection library supporting arbitrary jump chains with per-hop authentication (keys, keyboard-interactive 2FA, GSSAPI/Kerberos) and strict hostkey validation.Built on Paramiko, structured around transport orchestration and pluggable auth strategies.

Targets bastions, HPC and locked-down enterprise environments.

<!-- good idea Yes, but only if you scope it to “reliable hop chain + auth plugins + hostkey policy” and do not chase full OpenSSH feature parity.
Main risk: edge cases (per-hop auth quirks, ProxyCommand variants, agent forwarding, hostkey UX) dominate time; value is highest for bastion-heavy/HPC automation. -->

This library provides a generic, programmatic way to establish arbitrary SSH connections through any number of jump hosts, with explicit control over transports, channels, authentication and host key validation. It is built on Paramiko and models SSH as a sequence of hops, each with its own transport lifecycle, rather than as a command-line workflow.

Connections can be defined either by resolving an existing `ssh_config` entry or by supplying an explicit hop specification list. Each hop can independently select its authentication strategy, including SSH keys, keyboard-interactive 2FA and (optionally) GSSAPI/Kerberos, while enforcing strict per-hop host key validation. The same orchestration logic applies regardless of input source.

The API exposes transports and channels as first-class objects, allowing users to choose between single-transport multi-channel designs or fully isolated multi-transport chains. The goal is not OpenSSH feature parity, but a reliable, composable foundation for automating complex SSH workflows in bastion-heavy, enterprise and HPC environments.

Possible features: X11 forwarding support (requesting X11 on a channel and managing X11 auth/display plumbing when a local X server is available). Also SSH agent integration (authenticate via the local agent, and optionally support agent forwarding across jump hops). 

Very vaguely possible feature: ProxyCommand-style connectors, where a user-defined local command provides a bidirectional byte stream that is wrapped into a Paramiko Transport . Limited ProxyCommand support, allowing a user-defined local command to provide a stream that is wrapped into a Paramiko Transport. Scope would be best-effort only, without guaranteeing full OpenSSH compatibility or helper availability. Any implementation is constrained to "command that behaves like a raw TCP pipe", not the full OpenSSH universe.
