# Investigation Notes

## Initial Observation

While reviewing the authentication log, I noticed that the `jlee` account had a large number of failed authentication attempts.

## Authentication Failures

- User: `jlee`
- Source IP: `185.77.12.44`
- Failed attempts: 18
- First failed attempt: 9:55:00 AM
- Last failed attempt: 10:01:14 AM

## Successful Authentication

A successful authentication for `jlee` from `185.77.12.44` occurred at 10:02:10 AM.

This was 56 seconds after the final failed authentication attempt.

## Baseline Comparison

Previous successful authentication activity for `jlee` originated from `10.10.20.15`.

The suspicious activity originated from a different source IP: `185.77.12.44`.

## Assessment

The repeated failed authentication attempts followed by a successful authentication from the same unusual source IP are consistent with possible brute-force activity.

The available authentication data alone does not confirm that the account was compromised.

## Further Investigation

Additional investigation should determine:

- Whether the account owner recognizes the successful login.
- What activity occurred after the successful authentication.
- Whether other systems recorded activity associated with the source IP.
- Whether additional accounts experienced similar authentication attempts.
