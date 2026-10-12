# Explaining failures and fixes

## Explain the distinction the failure depends on

Before describing the bug, establish the facts the reader needs to understand it. For example, an identity mismatch only makes sense once the reader knows that the agent and its owner have separate document permissions.

## Use one concrete scenario

Name who changes what, whose permissions or state each code path checks, and what fails. Follow that scenario from the triggering change through the relevant paths to the observable consequence. Explain the reverse direction only when it adds a different consequence.

## Translate internal values into behavior

Introduce an internal value by explaining what selecting it does. For example, introduce `agentOwner` as “access documents using the installed agent owner's permissions.” Then reuse ordinary words such as “owner” and “agent”; retain the identifier where it helps the reader locate or apply the change.

## Keep implementation caveats beside the proposal

Describe a suggested change as a proposal until the relevant behavior has been tested. Put untested status and incomplete coverage next to the suggested diff or proposal. State which behavior remains unverified or uncovered there, so the main explanation stays focused on the failure.

## Example

This fictional scenario illustrates the explanation's structure.

Too compressed:

> `agentOwner` passes validation, but retrieval still uses the agent identity.

Explanatory:

> An installed agent and its owner have separate document permissions. The owner can read a document that the agent cannot. An editor sets document access to `agentOwner`, meaning “access documents using the installed agent owner's permissions.” Validation checks the owner's permissions and accepts the document, but retrieval checks the agent's permissions and rejects the read. The request therefore passes validation and then fails when it tries to retrieve the document.

The explanation establishes the permission distinction, follows one change through both checks, and names the observable failure.
