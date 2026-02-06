# Integration contracts

For cross-repo features, create a contract file in /contracts:

- contracts/CONTRACT-<feature>.md

The contract should include:
- endpoints + payloads
- query params
- auth/roles expectations
- edge cases

When implementing in another repo, paste the relevant contract section into the PR comment so the agent does not need cross-repo access.
