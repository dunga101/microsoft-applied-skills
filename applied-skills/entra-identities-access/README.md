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
- **IP address:** 131.107.1.10  
- **Sign-in risk level:** High  

This scenario was designed to represent a realistic external sign-in attempt involving elevated identity risk.

---

### Policy Evaluation Results

Conditional Access policies were evaluated independently based on assignment scope and configured conditions.

#### Policies that applied

- **Policy2**  
  - Assigned directly to Diego Siciliani  
  - Policy state: Enforced  
  - Applied successfully because user assignment conditions were met  

- **Policy3**  
  - Assigned to all users  
  - Policy state: Report-only  
  - Evaluated for visibility and impact analysis  

- **Policy4**  
  - Assigned to all users  
  - Policy state: Report-only  
  - Evaluated to observe potential enforcement behavior  

#### Policies that did not apply

- **Policy1**  
  - Assigned to a different user (Alex Wilber)  
  - Excluded from evaluation due to user assignment mismatch  

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
