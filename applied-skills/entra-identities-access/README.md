# Microsoft Applied Skills  
## Get started with identities and access using Microsoft Entra

Documentation and technical notes derived from completing the Microsoft Applied Skills assessment focused on identity and access management using Microsoft Entra ID.

This repository captures architectural concepts, evaluation logic, and identity engineering takeaways learned through hands-on validation, without exposing assessment material or implementation-specific configurations.

---

## Assessment Overview

This Applied Skills assessment evaluated practical identity and access management operations within Microsoft Entra ID.

The primary focus was understanding how Conditional Access functions as a real-time decision engine and how identity signals—such as user context, device posture, location, and risk—combine to determine access outcomes during authentication.

The environment reflected realistic enterprise identity scenarios, emphasizing reasoning, validation, and interpretation rather than isolated configuration tasks.

---

## Assessment Objectives

The assessment validated the ability to:

- Understand Conditional Access as a policy-based access control framework
- Evaluate policy behavior under varied authentication conditions
- Analyze how identity signals influence access decisions
- Validate access logic prior to enforcement
- Interpret Conditional Access outcomes using structured testing tools
- Apply risk-aware identity security principles

---

## Conditional Access Evaluation Framework

Conditional Access in Microsoft Entra operates as a dynamic identity policy engine.

During authentication, multiple contextual signals are collected and evaluated to determine whether access should be allowed, restricted, or challenged.

Key signal categories include:

- Identity context (user or group assignment)
- Application context (cloud resources)
- Client context (browser or application type)
- Device context (platform or compliance posture)
- Network context (location-based indicators)
- Risk context (sign-in and identity risk)

Access decisions are derived from the combined evaluation of these signals rather than a single condition.

---

## Policy Evaluation Logic (Conceptual)

Conditional Access policies are evaluated independently against the authentication context.

The evaluation process follows these core principles:

- Each policy is assessed individually
- Policy relevance is determined first by assignment scope
- All configured conditions must be satisfied for applicability
- Multiple policies may apply simultaneously
- Policies outside assignment scope are excluded immediately

There is no sequential “first-match” logic.  
Applicable policies collectively influence the final access decision.

---

## Policy State Considerations

Conditional Access policies may operate in different enforcement states.

### Enforced Policies

- Actively apply access controls
- Directly affect authentication outcomes
- Used for production security enforcement

### Report-Only Policies

- Fully evaluated during sign-in
- Do not block or enforce access
- Provide visibility into potential enforcement behavior
- Commonly used to validate policy impact prior to rollout

Report-only mode enables safe testing of access controls without user disruption.

---

## Role of What If Analysis

The What If tool in Microsoft Entra ID provides deterministic simulation of authentication scenarios.

This allows administrators to:

- Safely test sign-in conditions
- Validate policy applicability
- Understand why policies apply or do not apply
- Identify assignment or condition mismatches
- Evaluate enforcement impact before deployment

Structured simulation significantly reduces uncertainty during identity troubleshooting and policy design.

---

## Operational Observations

Key behaviors reinforced through evaluation include:

- Conditional Access policies are evaluated independently
- Assignment scope acts as the primary gating factor
- Conditions are evaluated only after assignment inclusion
- Report-only policies provide full evaluation visibility
- Multiple policies can influence a single authentication event

These behaviors highlight the need for strong identity governance as environments scale.

---

## Lessons Learned / Identity Engineering Takeaways

### Identity Is the Modern Security Perimeter

Security enforcement has shifted from network-centric controls to identity-centric decision making.

Microsoft Entra evaluates access dynamically using real-time context rather than static allow or deny rules.

Conditional Access functions as the central enforcement layer of modern Zero Trust architectures.

---

### Policy Assignment Determines Relevance First

Policy evaluation begins with assignment scope.

If a user or group is not included in a policy assignment, the policy is excluded entirely—regardless of matching conditions.

This reinforces the importance of:

- Precise user and group targeting
- Avoiding unnecessary broad assignments
- Clearly documenting policy intent
- Maintaining ownership and governance

Mis-scoped assignments are a common source of both overblocking and security gaps.

---

### Report-Only Mode Is an Engineering Safeguard

Report-only mode is a critical identity engineering control.

It enables teams to:

- Validate policy logic safely
- Observe potential enforcement behavior
- Detect overlap or conflicts early
- Prevent accidental user lockouts
- Support controlled rollout strategies

Effective identity design relies on measured validation rather than immediate enforcement.

---

### Deterministic Testing Reduces Risk

Simulation-based testing using tools such as What If analysis enables predictable access outcomes.

This approach:

- Reduces troubleshooting time
- Improves confidence in enforcement decisions
- Supports structured change management
- Strengthens overall identity maturity

Identity logic should be tested with the same rigor as infrastructure or application changes.

---

### Governance Is Essential at Scale

As Conditional Access environments grow, complexity increases rapidly.

Without documentation and governance, organizations risk:

- Policy sprawl
- Redundant enforcement
- Conflicting access requirements
- Reduced troubleshooting clarity
- Long-term operational drift

Identity governance must evolve alongside policy creation to maintain clarity and control.

---

## Summary

This Applied Skills assessment reinforced that strong identity security is achieved through deliberate engineering practices rather than configuration alone.

Effective identity posture depends on:

- Clear policy intent
- Precise assignment scoping
- Structured validation
- Controlled enforcement
- Ongoing governance

Microsoft Entra Conditional Access provides powerful capabilities, but those capabilities must be designed, tested, and governed thoughtfully to balance security and operational stability.
