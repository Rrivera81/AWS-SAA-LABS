# Lab 04 — ENI, Elastic IP, and Placement Groups

Region: us-east-2

## What I built
Tested public IP behavior across stop/start, attached a secondary ENI,
attempted a cross-AZ ENI attach to confirm the AZ boundary, and launched
an instance into a cluster placement group.

## Part 1 — Elastic IP vs auto-assigned public IP
Launched a t2.micro and recorded the auto-assigned public IPv4.

| | Public IPv4 |
|---|---|
| At launch | 18.191.217.28 |
| After stop/start | 18.217.132.39 |
| After associating an Elastic IP | 18.216.158.72 |
| After stop/start with EIP attached | 18.216.158.72 |

**Result:** the auto-assigned public IP changed on restart. The Elastic IP
did not.

**Why it matters:** if a partner allow-lists your IP on their firewall, an
auto-assigned public IP breaks the allow-list every time the instance stops.
An Elastic IP is static and survives stop/start.

**Cost note:** an Elastic IP that is not attached to a running instance is
billed. Released it at teardown.

## Part 2 — Secondary ENI and the AZ boundary
Created an ENI in the same AZ (us-east-2c) as the instance and attached it as a
secondary interface. Then created an ENI in a different AZ (us-east-2b) and tried to
attach it to the same instance.

**Result:** The instance did not appear in the attach target list at all —
AWS filtered out instances outside the ENI's AZ, so the attach is not even
offered.

**Takeaway:** an ENI is bound to the Availability Zone it was created in.
It can be detached and reattached to a different instance, but only within
that same AZ. Cross-AZ failover requires a different mechanism — a load
balancer, or remapping an Elastic IP to a standby instance.

## Part 3 — Cluster placement group
Created a cluster placement group and launched an instance into it.

- **Cluster** — instances packed close together in a single AZ. Lowest
  latency, highest throughput. Shared failure domain. Use for HPC and
  tightly coupled workloads.
- **Spread** — each instance on distinct hardware. Max 7 per AZ. Use for a
  small number of critical instances.
- **Partition** — instances divided into partitions on separate racks. Use
  for large distributed systems (HDFS, Kafka, Cassandra).

## Core Four — IAM rebuild (from memory)
- Rep 1 (Jul 25): 2:01
- Rep 2 (Jul 26): 1:03
- Rep 3 (Jul 28): 00:38.33

## Practice test 01 — 15/20 (75%)
First cumulative test covering IAM + EC2 fundamentals + EC2 SA-level.

Three of five misses were topics I had already drilled and scored well on
days earlier — Dedicated Host vs Instance, Credentials Report vs Access
Advisor, and least privilege. That is decay, not a knowledge gap, and it is
why the cumulative tests exist. Added a fast recall drill to the daily
warm-up.

## Teardown
Terminated instances, released the Elastic IP, deleted the ENIs and the
placement group. Verified us-east-1 and us-east-2 show no running resources.
