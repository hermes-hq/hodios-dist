<context>
Cloud cost advice is usually a generic list ("use spot", "rightsize", "buy reservations") with no link to the actual bill. Real savings come from reading where the money goes, which is often not compute: NAT gateway processing, cross-zone and internet egress, log ingestion, idle environments, forgotten snapshots and over-provisioned database storage. Every recommendation must trace back to a line of the bill and carry an honest risk.
</context>

<task>
Find savings in this bill:
[BILL_EXPORT]

1. Identify the provider and the bill's currency. Group spend by service and usage type; list the items that make up 80% of the total and the month-over-month trend.
2. Look for savings in four groups:
   - Waste: unattached volumes and IPs, old snapshots and images, idle load balancers, non-production environments running all week, unused provisioned capacity.
   - Rightsizing: instances, databases and containers whose utilisation is low. Recommend this only when utilisation data supports it; otherwise mark it "verify utilisation first".
   - Pricing: commitments (savings plans, committed use, reservations) sized to the steady baseline only; spot or preemptible capacity for fault-tolerant stateless work; storage tiers and lifecycle rules.
   - Architecture: data transfer paths, NAT gateway traffic that could use private endpoints, log and metric volume, chatty cross-zone traffic, over-replication.
3. For each saving, estimate the monthly amount with the arithmetic from the bill lines, and rate effort (S/M/L) and risk (low/medium/high, with what could break).
4. Rank by monthly saving adjusted for effort and risk. Separate reversible quick wins from commitments that lock in spend.
</task>

<constraints>
- Every number must come from the export or be marked as an estimate with its assumption. Do not invent usage figures.
- Never recommend deleting data, snapshots or backups without first checking retention, legal hold and restore needs; say so on those items.
- Size commitments to the lowest steady usage, not the average, and say what the lock-in period is.
- Quote amounts in the bill's currency, written as the currency code followed by the number (for example "USD 1,200").
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Spend summary
Total, trend, and a table of the top cost lines with their share.
## Ranked savings
A table: rank, change, monthly saving, effort, risk, reversible (yes/no).
## Details
One short subsection per saving: evidence from the bill, the exact action, what could break, how to verify the saving next month.
## Do not touch
Items that look wasteful but are not, and why.
## Data needed
What extra data (utilisation, tags, traffic) would sharpen the estimates.
</output_format>
