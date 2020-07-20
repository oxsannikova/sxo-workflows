# sxo-acsc-advisory-workflow

## Overview

> Full description of this project is covered in this [blog post](https://blogs.cisco.com/security/unleashing-securex).

Recently certain Australian government owned entities and companies have been targeted by a sophisticated state-based actor. The Australian Cyber Security Centre (ACSC) has titled these events as “Copy-Paste Compromises” and have published a summary with links to detailed TTPs (tactics, techniques, procedures). 
This SecureX orchestration workflow is an automated way to help understand the impact of the threat in your environment. Are these observables suspicious or malicious? Have we seen these observables? Which endpoints have the malicious files or have connected to the domain/URL? What can I do about it right now?

If you are not in Australia, don’t walk away just yet! The title ‘Copy-Paste Compromises’ is derived from the actor’s heavy use of proof of concept exploit code, web shells and other tools copied almost identically from open source. So you may see some of these in your environment even if you are not being specifically targeted by this campaign. Also you can replace the example above with any other malware/cyber campaign. Typically you will find blogs from Cisco (TALOS) or other vendors or community posts, detailing the TTPs and more importantly the IOCs. In other situations, you might receive IOCs over a threat feed or simply scrape them from a webpage/blog/post. Irrespective with minor tweaks the below process should still work for any of those sources as well.

SecureX orchestrator enables you to create automated workflow that can be modified for any IOC source, including the TALOS Blog RSS Feed, however in this case we are going to use the ACSC provided [IOC csv file](https://www.cyber.gov.au/sites/default/files/2020-06/ACSC-Advisory-2020-008-Copy-Paste-Compromises-Indicators-of-Compromise.csv).

Workflow Block-scheme:

![](/assets/playbook_flow.png)

[Workflow Setup Instructions](acsc_workflow.md)

Copyright (c) 2020 Cisco Systems, Inc. and/or its affiliates.
