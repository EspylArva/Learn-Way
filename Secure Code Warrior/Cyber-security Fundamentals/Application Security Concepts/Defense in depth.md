# Defense in depth
## Context
Attack on system: target is directly accessible
## Danger
Attacker can access the target
## Counter measures
- Implement different layers to make the process complex
- Examples of layering:
	- Data validation enabled to protect injection attack
		- Client side
		- Server side
		- Read-only server ([[Least privilege]])
	- Data encrypted so stolen data are unusable
	- Network segmented, so intruder only has access to part of the network
- Most important steps of Defense in depth:
	- Data layer: access controls, encryption, backup/restore procedure
	- Application layer: authentification/authorization/auditing (AAA), secure coding, hardening
	- Host layer: hardening, authentification, patch management, antivirus
	- Internal network: network segmentation, IPsec, TLS, NAT
	- Perimeter layer: Firewall, TLS, [[Denial of Service|DoS]], prevention
	- Physical security: guards, locks, tracking devices, access control