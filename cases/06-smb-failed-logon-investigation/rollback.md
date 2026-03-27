# Rollback / Lab Cleanup

## Objective
Return the lab to its pre-simulation state after generating repeated failed SMB authentication attempts.

## Cleanup Actions
Recommended cleanup steps:
1. verify that no test account is locked out;
2. unlock affected lab accounts if required;
3. confirm that no successful session was created on `WinTest10`;
4. retain exported screenshots and logs in the evidence folder;
5. clear only temporary lab artifacts if any were created outside normal logging.

## Validation After Cleanup
After cleanup, verify:
- `WinTest10` remains operational;
- the shared folder used during testing is still in the expected state;
- the two test accounts are usable for future lab cases;
- no unintended configuration changes were introduced.

## Notes
Because this case intentionally generated failed authentication events only, rollback is minimal. The primary task is to confirm there was no successful access and no lasting side effect on the host or the domain accounts used in the simulation.