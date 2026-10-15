# Follow precedent

Existing patterns govern implementation choices unless an explicit task requirement or applicable documented repository rule overrides them. Prefer consistency over your preferred design. Apply this contract to plans, implementation, tests, and proposed review fixes.

## 1. Establish precedent before editing

Find the closest existing implementation with the same responsibility. Read its callers and tests to understand its contract. Compare another established example when available. Cite the relevant paths and symbols before proposing or implementing changes. Code introduced by the change under consideration is not independent precedent.

Done when each substantive choice has an existing source reference, or the searched locations and absence of applicable precedent are recorded. For a gap, disclose the proposed approach under step 3 before implementing it.

## 2. Confirm that the precedent applies

Match architectural responsibility, trust boundaries, and lifecycle. A similar name or shared API is insufficient. Prefer applicable local patterns over examples from unrelated subsystems. If examples conflict, explain which fits this task and why. If the conflict remains unresolved, surface it before choosing and continue independent work.

Done when each cited example fits the affected contract and every conflict is resolved with evidence or surfaced as a blocking question for the affected work.

## 3. Disclose necessary deviations before implementing

For each proposed deviation, state:

- The existing pattern, with a source reference, or the recorded search gap.
- The task requirement or concrete failure it cannot accommodate.
- The smallest necessary departure.
- The resulting behavior and compatibility consequences.

Elegance, hypothetical future needs, and personal preferences do not establish necessity. If the task already authorizes the departure, cite that authorization and proceed within its scope. Otherwise, obtain direction before implementing the affected portion. Continue independent work.

Done when every departure is disclosed and tied to necessity, and implementation proceeds only within existing authorization or newly obtained direction.

## 4. Adapt the existing implementation

Reuse its helpers, types, defaults, and division of responsibilities. Preserve its error propagation and ordering guarantees. Treat new abstractions, configuration mechanisms, retries, fallbacks, and side effects as design deviations subject to step 3. Keep unrelated cleanup outside the change.

Done when every substantive implementation choice follows the cited pattern or an explicitly authorized deviation.

## 5. Follow existing validation ownership

Trace where inputs become trusted before adding checks. Reuse the established schemas and validation boundary. For every additional check, identify the contract it enforces and explain why existing validation is insufficient. Treat new limits, formats, rejection rules, and repeated validation as behavior changes subject to step 3. If precedent leaves a concrete correctness or security gap, disclose that gap explicitly.

Done when each added check has a justified contract and owner, and every resulting behavior change has passed step 3.

## 6. Verify through established tests and commands

Extend the closest existing tests using their fixtures and conventions. Derive expected behavior from task requirements and existing contracts. A test written for a newly invented rule does not establish that the rule is required. If verification needs a new harness or procedure, apply step 3.

Done when the tests follow applicable precedent, their expectations trace to requirements or existing contracts, and established verification commands pass or their limits are reported.

## 7. Audit the complete diff against precedent

Account for every substantive difference from the cited examples. Remove differences that lack a requirement or an authorized deviation. When review identifies a pattern violation, inspect the complete change for other instances of the same mistake.

Finish only when every substantive choice follows cited precedent or has an explicitly authorized deviation. Unresolved choices and inspection limits remain explicit blockers to claiming full conformance.
