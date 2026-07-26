# Lab 02 — IAM Policies

## What I built
A custom IAM policy allowing s3:GetObject on one bucket, then added an
explicit Deny on the same resource to prove the evaluation rule.

## The policy
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowRead",
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::DEMO/*"
    },
    {
      "Sid": "DenyRead",
      "Effect": "Deny",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::DEMO/*"
    }
  ]
}
```

## What each part does
- **Effect** — Allow or Deny
- **Action** — the API call (s3:GetObject = read an object)
- **Resource** — the ARN it applies to. The `/*` scopes it to objects
  inside the bucket, not the bucket itself.

## What I tested
With both Allow and Deny on the same object, read access failed.
Confirmed: explicit deny always overrides explicit allow.

## What broke
Got a JSON syntax error adding the Deny statement — I was typing it in
the wrong place. Fixed it with the "Add new statement" button, which
scaffolds each statement as its own {} object inside the Statement [ ]
array, comma-separated.

## Core Four — IAM rebuild (from memory)
- Rep 1 (Jul 25): 2:01.41 — user, group, attach policy, add user to group
