# Consented Rewards Eligibility -- AP3 Demo Brief

**Working title:** Booking.com travel agent closes a $2,000 budget gap using partner rewards without exposing raw account data

---

## What This Demo Shows

A Booking.com AI travel agent helps a family of five book a five-night Hawaii trip. The best package is $2,000 over budget. Instead of asking the traveler to share loyalty credentials upfront, the agent asks for consent to run a privacy-preserving eligibility check across Marriott Bonvoy, United MileagePlus, and American Express. The check uses the Agent Privacy-Preserving Protocol to confirm that the traveler has applicable rewards -- without any partner revealing raw balances, account records, or business rules. The agent then recommends a revised package that fits the budget.

---

## The Scenario

- Traveler request: five-night Hawaii trip, two adults, three children, two hotel rooms, budget $10,000
- Initial package found: $12,000 (flights for five + two hotel rooms + fees)
- Budget gap: $2,000
- Trigger: agent surfaces consent request before touching any loyalty data

---

## Step-by-Step Flow

1. **Traveler prompt** -- "Plan a five-night Hawaii trip for a family of five under $10,000, two rooms."
2. **Agent finds package** -- $12,000. Flags the $2,000 gap.
3. **Consent request** -- Agent asks permission to check eligible rewards from Marriott, United, and Amex. Traveler clicks "Check rewards eligibility."
4. **AP3 initiates** -- A customer-approved purpose is created: "Evaluate whether eligible rewards can reduce this package from $12,000 to $10,000."
5. **PSI (Private Set Intersection)** -- Confirms the traveler has an account at each partner, without Booking.com seeing partner member lists or partners seeing Booking.com's user base.
6. **Threshold comparison** -- For Marriott and United: does this traveler have enough points or miles to cover the required portion of the package? Evaluated over private data. Output is an eligibility band, not a balance.
7. **Secure Function Evaluation** -- For Amex: which card benefits apply to this specific booking type? The eligibility function runs over private Amex inputs. Output is benefit flags only.
8. **Indicators returned** -- Booking.com receives: Marriott Free Night Award eligible, points sufficient for two additional room nights; United miles sufficient for award travel for two travelers; $200 Amex hotel credit applicable.
9. **Package recalculated** -- Original $12,000, rewards applied -$2,150, recommended total $9,850.
10. **Traveler confirms** -- "Proceed with this package." Actual redemption and account connection happen separately and are outside the scope of this demo.

---

## What AP3 Protects

| Private data | Held by | Never leaves | Protocol primitive |
|---|---|---|---|
| Points balance, Free Night Awards, stay history | Marriott Bonvoy | Marriott's system | Threshold Comparison |
| Miles balance, award availability | United MileagePlus | United's system | Threshold Comparison |
| Card benefits, Membership Rewards, transaction history | American Express | Amex's system | Secure Function Evaluation |
| Traveler identity across all three partners | All parties | Resolved inside Silence Compute only | Private Set Intersection |

---

## What Each Party Sees

**Traveler sees:** the budget gap, the consent request, which rewards were applied, revised package options, final total.

**Booking.com sees:** traveler request, consent, eligibility indicators (not raw balances), enough to rank package options.

**Partners see:** a customer-approved eligibility request, the scoped purpose, only what is needed to evaluate their specific function.

**Partners do not share:** raw balances, account numbers, transaction history, redemption rules, full account records.

---

## Product Boundaries

This demo shows:
- Consented, privacy-preserving eligibility checking across partner loyalty systems
- Planning-safe indicators sufficient for package recommendation
- Agent-to-agent coordination via the Agent Privacy-Preserving Protocol and Silence Compute

This demo does not show:
- Actual redemption or point spend (requires separate partner authorisation)
- Live integration with Marriott, United, or Amex systems
- A production-ready booking flow

A production MVP would require partner policy agreements, consent language review, audit logging, identity integration, and booking and redemption system integration.

---

## For Partner Review

The Agent Privacy-Preserving Protocol supports consented, privacy-preserving eligibility checks between agents. Silence Compute evaluates approved functions over private partner data. Booking.com receives only planning-safe indicators for package ranking. Raw loyalty records, balances, transaction history, and partner rules remain inside each partner boundary.

Final redemption, account connection, and payment require explicit traveler approval and partner fulfilment.
