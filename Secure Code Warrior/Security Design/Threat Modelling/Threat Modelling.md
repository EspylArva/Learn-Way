# Threat Modelling
## What is it?
A way to identify, communicate and understand security threats and mitigations.
Helps evaluate and prioritise threats to respond accordingly
## How to do it?
Different methods exist, such as [[STRIDE]] and [[Attack Trees]], but there is no absolute way to implement it.
There are however four points that should be covered:

| Topic | Description | Action | Description |
|-|-|-|-|
| Assets | What needs to be protected. Could be an app, a service, data... | Assessment | Description or model of the asset and its analysis |
| Vulnerabilities | Weaknesses, entry points that could be exploited to deal damage | | |
| Threats | Nature of damage that could occur in case of an attack or exploit | Threat Identification, Threat prioritization, and Remediation of threats | List of things that could go wrong, their priority compared to others, and countermeasures that could be applied to reduce the risk level |
| Threat Agents | Agent causing the damage. Could be insiders or outsiders. Threat agents can be oblivious of being such | Threat Agent Identification | List of agents who might be able to attack or leak vulnerabilities |

Threat modelling should be done ahead of project or at least as early as possible. It should be redone regularly, especially when the specification change. Asking questions on each topic (assets, vulnerabilities, threats, and agents) makes it easy to refresh the risk assessment