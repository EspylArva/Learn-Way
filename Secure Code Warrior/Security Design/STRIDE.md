# STRIDE
## What is it?
STRIDE is a way to [[Threat Modelling|model threats]]. It has been designed by Microsoft and is still considered one of the most comprehensive way to identify threats.
It is used at every application development stage: from design to development, testing and security proofing.

Each letter of STRIDE represent a topic of threat modelling: 
| Letter | Threat | Description | Desired Property | 
|-|-|-|-|
| S | Spoofing | Impersonation of someone or something | Authentification |
| T | Tampering | Modification of data or code by an attacker | Integrity |
| R | Repudiation | Claim that an action has not been commited | Non-repudiation |
| I | Information Disclosure | Leak of confidential data to those that should not be permitted |Confidentiality |
| D | [[Denial of Service]] | Degradation or denial of a service  | Availability |
| E | Elevation of Privilege | Gain of capabilities that were not granted nor supposed to be granted | Authorization |

## How to do it?
To use STRIDE, we ask ourselves "How could someone \<insert threat from STRIDE> our \<insert product>?". For example, "How could someone spoof our app?". STRIDE can also be applied to parts of the system: for example, "how could someone [[Denial of Service|DoS]] the communication layer of the system?"

## Alternatives
STRIDE is only one of the many ways to [[Threat Modelling|model threats]]. Although it is deemed very comprehensive, it could still be paired with other methodologies.
