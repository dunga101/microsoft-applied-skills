# Microsoft Applied Skills  
## Get started with identities and access using Microsoft Entra

Documentation and technical notes for the Microsoft Applied Skills assessment focused on identity and access management using Microsoft Entra ID.

---

## Assessment Overview

This Applied Skills assessment evaluated hands-on identity and access management operations within Microsoft Entra ID.  
The focus was on understanding how Conditional Access policies are evaluated during authentication and how risk-based signals influence access decisions.

The assessment environment simulated real-world enterprise scenarios involving user sign-ins, device platforms, network locations, and identity risk.

## Assessment Objectives

- Evaluate Conditional Access policy behavior under different sign-in conditions
- Use What If analysis to determine policy applicability and order of evaluation
- Understand the impact of report-only versus enforced policies
- Configure and validate named locations for access control logic
- Review authentication methods, MFA, and Self-Service Password Reset configuration
- Interpret sign-in risk signals and their effect on access decisions
## Conditional Access Policy Evaluation

This assessment focused on understanding how Microsoft Entra evaluates Conditional Access policies during user authentication and how multiple identity signals combine to determine final access outcomes.

Policy behavior was analyzed using the **What If** tool (Microsoft Entra ID P2), which simulates real sign-in attempts and provides detailed visibility into policy applicability, evaluation results, and access decisions.

---

### Evaluation Method

A simulated sign-in scenario was configured with the following attributes:

- **User:** Diego Siciliani  
- **Application:** Microsoft Exchange Online  
- **Client type:** Browser  
- **Device platform:** Android  
- **Network location:** United States  
- **IP address:** 131.107.#.##  
- **Sign-in risk level:** High  

This scenario was designed to represent a realistic external sign-in attempt involving elevated identity risk.

---

## Policy Evaluation Logic (Conceptual Summary)

Conditional Access policies are evaluated independently during sign-in based on assignment scope and configured conditions.

The evaluation process follows these principles:

- Each policy is assessed individually against the sign-in context.
- Policies apply only when the user or group assignment is in scope.
- All configured conditions (such as device platform, application, location, or risk) must be satisfied for a policy to be considered applicable.
- Policies that are not assigned to the signing-in identity are excluded from evaluation.
- Multiple policies can apply simultaneously during a single authentication attempt.

### Policy State Considerations

- **Enforced policies** actively apply access controls and directly affect sign-in outcomes.
- **Report-only policies** do not block or enforce access but provide visibility into how enforcement would behave if enabled.
- Report-only mode is commonly used to validate policy impact before production rollout.

### Evaluation Outcome Interpretation

During sign-in analysis:

- Applicable policies contribute to the final access decision.
- Non-applicable policies are ignored without impact.
- Visibility from report-only policies helps identify unintended access restrictions, overlap, or conflicts.

This evaluation model allows identity engineers to validate security posture while minimizing disruption to end users.

---

### Key Observations

- Conditional Access policies are evaluated **independently**, not in sequence.
- A policy applies only when **all assignment and condition criteria are satisfied**.
- Policies in **report-only mode** are fully evaluated but do not enforce access controls.
- The What If tool clearly identifies **why a policy does or does not apply**, eliminating uncertainty during troubleshooting.
- User assignment is a primary gating factor — policies not scoped to the signing-in user are excluded immediately.

---

### Operational Insight

This evaluation reinforced the importance of validating Conditional Access behavior through structured testing rather than assumption.

Using What If analysis enables administrators to:

- Safely test high-risk sign-in scenarios without affecting production users
- Validate policy scope prior to enforcement
- Identify overlapping or redundant Conditional Access policies
- Reduce the risk of unintended access blocks during rollout

This approach supports controlled security posture improvements while maintaining operational stability.
## Lessons Learned / Identity Engineering Takeaways

This assessment reinforced several critical principles that govern effective identity and access management in enterprise environments.

---

### Identity Is the Primary Security Control Plane

Modern security decisions are no longer enforced solely at the network perimeter. Identity now serves as the central enforcement point where user context, device posture, location, and risk signals converge.

Conditional Access operates as a real-time policy engine that evaluates identity signals dynamically rather than relying on static allow or deny rules.

---

### Policy Assignment Determines Relevance Before Conditions Are Evaluated

Conditional Access evaluation begins with **policy assignment scope**.

If a user is not included in the policy assignment, the policy is excluded immediately—regardless of how well other conditions match the sign-in scenario. This reinforces the importance of:

- Precise user and group targeting
- Avoiding overly broad “All users” assignments without justification
- Clearly documenting policy ownership and intent

Mis-scoped assignments are a common root cause of both overblocking and security gaps.

---

### Report-Only Mode Is a Critical Engineering Control

Report-only mode is not merely a testing feature—it is an essential identity engineering safeguard.

Using report-only policies enables administrators to:

- Observe policy behavior without user impact
- Validate condition logic against real sign-in patterns
- Identify unintended enforcement scenarios early
- Safely evaluate complex access models involving multiple signals

Effective identity design relies on measured rollout rather than immediate enforcement.

---

### What If Analysis Enables Deterministic Troubleshooting

The What If tool provides deterministic visibility into Conditional Access behavior by clearly identifying:

- Which policies apply
- Which policies do not apply
- The specific reason each decision was made

This eliminates guesswork and significantly reduces troubleshooting time compared to reviewing raw sign-in logs alone.

Structured simulation should always precede enforcement changes.

---

### Overlapping Policies Increase Complexity and Require Governance

When multiple Conditional Access policies target similar users or applications, complexity increases rapidly.

Without documentation and periodic review, organizations risk:

- Redundant policy enforcement
- Conflicting access requirements
- Reduced troubleshooting clarity
- Operational drift over time

Identity governance is as important as policy creation
