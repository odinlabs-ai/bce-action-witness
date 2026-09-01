# Witness record

## Scope

This record distinguishes two claims:

1. **External-repository execution:** the generated BCE Action runs in this repository through an
   immutable commit. GitHub Actions run URLs provide the evidence.
2. **Independent-human usability:** not established by the creator-maintained runs below. A future
   contributor must add their own signed-off observation without being coached through the commands.

## Candidate under test

- BCE Action and Git dependency: `blueprint-conformance/bce@5d8a3d96b184ad47d6cdec235f80cde1fb1e9a42`
- Blueprint: `no-direct-http-client@0.1.0`
- Posture: advisory, proposed, unratified

## Creator-maintained external Action runs

The sequence begins with a clean source change, then plants a direct `axios` import, then removes it.
Run URLs and observed outcomes are appended only after GitHub has executed them.

| Stage | Commit | GitHub Actions evidence | Observed result |
|---|---|---|---|
| clean | `cab5e06449adc34e80600f949ec26a553ba9e6d0` | [run 33496925176](https://github.com/odinlabs-ai/bce-action-witness/actions/runs/33496925176) | Action downloaded the immutable BCE commit, built its own engine on Node 22, and reported score 100 / pass |
| planted drift | `12a082745bc6c15b4ce78c806463a279216d02aa` | [run 33497018340](https://github.com/odinlabs-ai/bce-action-witness/actions/runs/33497018340) | score 60; `forbidden-dependency-axios` at `src/billing.extension.ts#L1`; visibly RED but non-blocking under committed advisory posture |
| corrected | `d7012ee87eefd0fa57adb20ae9cac26ae9cc2e49` | [run 33497122787](https://github.com/odinlabs-ai/bce-action-witness/actions/runs/33497122787) | same Action and blueprint returned to score 100 / pass |

These runs establish external-repository execution and RED/GREEN discrimination. They do not
establish independent-human usability.

## Independent contributor protocol

Without private guidance from the maintainer:

1. Fork or clone this repository on Node 22.
2. Follow `README.md` using only committed instructions.
3. Open a pull request that plants `import axios from 'axios'` in `src/billing.extension.ts`.
4. Record whether the generated Action names the violated contract and source anchor.
5. Remove the drift and record whether the same Action returns to a clean grade.
6. Add a short, candid note here: confusing steps, hidden prerequisites, and whether BCE helped.

Do not claim independence if a maintainer supplied missing commands interactively.
