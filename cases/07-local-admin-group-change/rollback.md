# Rollback / Lab Cleanup

## Objective
Return the lab to a safe post-simulation state after confirming unauthorized or suspicious local administrative group modification.

## Cleanup Actions
Recommended cleanup steps:
1. remove `ARATA\ops.user2` from the local `Administrators` group on `WinTest10`;
2. confirm that the account remains disabled until validation is complete;
3. reconnect the isolated host only after review is finished;
4. verify that privileged password resets were completed for all relevant administrative accounts;
5. retain screenshots and exported evidence in the case evidence folder.

## Validation After Cleanup
After cleanup, verify:
- `ARATA\ops.user2` is no longer a member of local `Administrators`;
- the workstation is back in the intended baseline state;
- no new privileged group modifications occurred during handling;
- no unintended configuration drift remains on `WinTest10`.

## Notes
Because this case involved confirmed privilege assignment, rollback must focus not only on artifact cleanup but also on restoring trust in privileged access. Administrative credential hygiene and membership validation are part of the cleanup process, not separate optional steps.