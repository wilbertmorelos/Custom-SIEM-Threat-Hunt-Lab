# Custom-SIEM-Threat-Hunt-Lab
# Custom SIEM and Threat Hunting Lab

## Objective
The goal of this project was to engineer a local Security Information and Event Management (SIEM) environment to ingest endpoint telemetry and simulate a real-world adversary attack. This lab demonstrates the ability to deploy infrastructure, parse raw telemetry, and hunt for specific Indicators of Compromise (IoCs).

## Tools & Technologies Used
* **Splunk Enterprise:** Log ingestion, parsing, and analysis.
* **Sysmon:** Advanced endpoint telemetry generation.
* **Atomic Red Team:** Adversary simulation and MITRE ATT&CK testing.
* **Windows 11 VM:** Target environment. 

## The Scenario
To test the detection capabilities of the SIEM, an adversary simulation was executed on the target endpoint. Specifically, **MITRE ATT&CK T1059.001 (PowerShell Execution)** was simulated using Atomic Red Team to bypass execution policies.

## Execution and Detection
1. **Infrastructure Setup:** Configured a Splunk Universal Forwarder and Sysmon to ship logs to the centralized SIEM. Diagnosed and resolved a network pipeline failure by modifying `outputs.conf` and validating TCP port 9997.
2. **Attack Simulation:** Executed the Atomic Red Team payload to trigger the PowerShell execution bypass. 
3. **Threat Hunting:** The raw Sysmon telemetry was ingested as XML. Wrote custom Splunk Processing Language (SPL) utilizing the `xmlkv` command to parse the raw text and extract the `CommandLine` and `ParentImage` fields.

*Insert Screenshot of your Splunk Table Here*

## Conclusion
By filtering out routine background processes, the exact malicious command line execution was isolated and identified. This project validated the effectiveness of continuous endpoint monitoring and custom log parsing in identifying living-off-the-land (LotL) techniques.
