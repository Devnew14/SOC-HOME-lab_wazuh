# SOC Home Lab — Wazuh SIEM

![Project status](https://img.shields.io/badge/status-in%20progress-orange)
![Focus](https://img.shields.io/badge/focus-SOC%20%7C%20Blue%20Team-blue)
![Platform](https://img.shields.io/badge/platform-Linux-lightgrey)

## Overview

This project aims to build a small Security Operations Center (SOC) home lab using Wazuh, an open-source security monitoring platform.

The objective is to understand how security events are collected, monitored, analyzed, and investigated in a controlled laboratory environment.

The project focuses on practical SOC analyst skills, including log analysis, authentication monitoring, alert investigation, detection validation, and incident reporting.

**Project status:** In progress. Implementation and test results will be documented as the lab evolves.

## Objectives

- Deploy and understand a Wazuh monitoring environment.
- Connect a monitored Linux endpoint to the platform.
- Collect and inspect security logs.
- Investigate repeated authentication failures.
- Validate detection behavior using controlled test events.
- Document alerts, false positives, and detection limitations.
- Produce a structured incident report.
- Practice technical documentation and reproducible investigations.

## Technologies and Languages

| Technology | Purpose |
|---|---|
| Wazuh | Security monitoring, log analysis, and alerting |
| Linux / Ubuntu | Laboratory environment and endpoint |
| Bash | Linux administration and command-line operations |
| YAML | Configuration files where applicable |
| Markdown | Technical documentation and incident reports |
| JSON | Structured sample events and test data |
| Python | Optional log generation and test automation |
| Git / GitHub | Version control and project documentation |

Additional technologies may be introduced when required by the project.

## Planned Architecture

The initial laboratory will use a Wazuh server and a monitored Linux endpoint.

```text
+--------------------------+
| Linux Endpoint           |
|                          |
| System and auth logs     |
+------------+-------------+
             |
             | Log collection
             v
+--------------------------+
| Wazuh Agent              |
|                          |
| Monitors configured logs |
+------------+-------------+
             |
             | Secure communication
             v
+--------------------------+
| Wazuh Server             |
|                          |
| Analysis and alerting     |
+------------+-------------+
             |
             v
+--------------------------+
| Wazuh Dashboard          |
|                          |
| Search, alerts, analysis |
+--------------------------+
```

This is the planned logical architecture. The actual deployment, network configuration, and communication settings will be documented after implementation.

## Laboratory Environment

Initial environment:

- A computer running Windows or Linux.
- A Linux virtual machine for the laboratory.
- Wazuh server and dashboard.
- A Wazuh agent installed on the monitored endpoint.
- A dedicated, isolated laboratory network where appropriate.

The required CPU, memory, disk space, and supported operating system versions will be determined using the official Wazuh documentation before installation.

## Implementation Roadmap

### Phase 1 — Environment Setup

- [ ] Review the Wazuh architecture.
- [ ] Check the host computer's available resources.
- [ ] Create the laboratory virtual machine.
- [ ] Install and configure Wazuh using the official documentation.
- [ ] Verify that the dashboard is accessible.
- [ ] Document the installation process.

### Phase 2 — Endpoint Monitoring

- [ ] Install and register the Wazuh agent.
- [ ] Verify agent connectivity.
- [ ] Identify the authentication logs collected by the endpoint.
- [ ] Inspect events in the dashboard.
- [ ] Document the log collection flow.

### Phase 3 — Authentication Detection

- [ ] Establish a baseline of normal authentication activity.
- [ ] Generate controlled authentication failures in the laboratory.
- [ ] Identify the corresponding events.
- [ ] Determine which detection rule generates an alert.
- [ ] Record the rule identifier, severity, and event details.
- [ ] Evaluate whether the alert is useful and sufficiently specific.

### Phase 4 — Detection Validation

- [ ] Define test cases and expected outcomes.
- [ ] Compare normal and suspicious authentication activity.
- [ ] Check whether expected alerts are generated.
- [ ] Investigate missing alerts and unexpected alerts.
- [ ] Document false positives and detection limitations.
- [ ] Consider improvements where justified by the tests.

### Phase 5 — Incident Investigation

- [ ] Select a controlled laboratory scenario.
- [ ] Build a timeline of relevant events.
- [ ] Identify the affected account and endpoint.
- [ ] Separate confirmed facts from hypotheses.
- [ ] Assess the potential impact.
- [ ] Recommend containment and remediation measures.
- [ ] Produce an incident report.

### Phase 6 — Documentation and Review

- [ ] Complete the architecture documentation.
- [ ] Add sanitized screenshots.
- [ ] Document the commands and configuration required to reproduce the lab.
- [ ] Explain the technical decisions.
- [ ] Record known limitations.
- [ ] Define future improvements.

## Detection Scenario: Repeated Authentication Failures

### Objective

Investigate repeated failed authentication attempts on a monitored Linux endpoint.

### Scenario

A user account receives multiple failed login attempts within a short period.

The activity could result from a mistyped password, a misconfigured service, or a suspicious attempt to gain access.

Repeated failures alone do not prove that an attack has occurred.

### Investigation Procedure

1. Identify the relevant authentication events.
2. Check timestamps, account names, source information when available, and event outcomes.
3. Correlate the events with Wazuh alerts.
4. Review the detection rule and its conditions.
5. Determine whether the activity can be explained by legitimate behavior.
6. Document the evidence and remaining uncertainty.
7. Recommend proportionate next steps.

### Expected Evidence

The investigation should aim to produce:

- Relevant event samples.
- The associated alert and rule information.
- A short event timeline.
- An assessment of the evidence.
- A record of detection limitations.
- A proposed response plan.

Results will be added after the scenario has been executed and validated.

## Incident Report Template

Each investigated scenario should include the following sections:

1. **Incident summary:** What was observed?
2. **Scope:** Which systems and accounts were involved?
3. **Timeline:** What happened, and when?
4. **Evidence:** Which logs and alerts support the findings?
5. **Assessment:** What is confirmed, suspected, or unknown?
6. **Impact:** What could be affected?
7. **Response:** Which containment or remediation actions are recommended?
8. **Lessons learned:** What could be improved?
9. **Detection improvements:** How could monitoring be made more effective?

## Security and Ethical Scope

All tests must remain within systems I own or have explicit permission to test.

- No unauthorized access attempts.
- No testing against public systems or third-party infrastructure.
- No real credentials, secrets, or personal data in the repository.
- No publication of private IP details, tokens, or sensitive screenshots.
- Use synthetic events when real logs are unnecessary.
- Document the scope and authorization of laboratory activities.

## Repository Structure

```text
soc-home-lab-wazuh/
├── README.md
├── .gitignore
├── docs/
│   ├── architecture.md
│   ├── installation.md
│   ├── detection.md
│   └── incident-report.md
├── config/
│   └── agent/
├── tests/
│   └── sample-events.json
├── scripts/
│   └── README.md
└── screenshots/
    └── README.md
```

Only files that are relevant and safe to publish will be added. Empty directories can be created as the corresponding phases begin.

## Learning Outcomes

By completing this project, I aim to develop practical skills in:

- Linux system administration.
- Security event collection and interpretation.
- SIEM concepts and alert investigation.
- Authentication monitoring.
- Detection validation and false-positive analysis.
- Incident documentation.
- Technical communication.
- Reproducible laboratory setup.

## Limitations

This is a personal laboratory and not a production SOC.

Its results will depend on the monitored systems, enabled log sources, configuration, detection rules, and test scenarios.

A successful test does not demonstrate that all attacks can be detected. Detection coverage and false-positive behavior must be evaluated within a defined scope.

## Future Improvements

Possible extensions include:

- Monitoring a Windows endpoint.
- Creating and validating custom Wazuh detection rules.
- Adding Sigma rules and explaining their compatibility or conversion where applicable.
- Mapping relevant detections to MITRE ATT&CK.
- Automating repeatable tests with Python.
- Developing additional incident scenarios.
- Comparing detection behavior across different log sources.

Extensions will be prioritized according to their learning value and the time available.

## References

- [Wazuh Documentation](https://documentation.wazuh.com/current/)
- [Wazuh Getting Started](https://documentation.wazuh.com/current/getting-started/)
- [Sigma Specification](https://github.com/SigmaHQ/sigma-specification)
- [MITRE ATT&CK](https://attack.mitre.org/)

---

**Author:** Your GitHub username

**Project type:** Cybersecurity home lab / Blue Team

**Status:** In progress
