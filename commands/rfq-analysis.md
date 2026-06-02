---
name: rfq-analysis
description: "Analyze a Request for Quotation document for freight forwarding. Extracts routes, volumes, service requirements, and special handling needs into a structured comparison format ready for the quoting team."
---

# /logistics-pm:rfq-analysis

Analyze an RFQ document and produce a structured breakdown for the quoting team.

## Arguments

`$ARGUMENTS` — The RFQ content (pasted text, uploaded file, or description of the request).

## Process

1. Read the `freight-domain-knowledge` skill for domain context.

2. Extract the following from the RFQ:

   **Route Information:**
   - Origin (port/city/country)
   - Destination (port/city/country)
   - Mode (ocean FCL, ocean LCL, air, multimodal)
   - Incoterms (if specified)

   **Cargo Details:**
   - Commodity description
   - Container type and quantity (if FCL)
   - Weight and volume (if LCL)
   - Special handling (hazmat, reefer, oversized, fragile)

   **Service Requirements:**
   - Frequency (one-time vs. contract with volume commitment)
   - Transit time expectations
   - Required documentation (COO, fumigation, inspection certificates)
   - Insurance requirements

   **Commercial Terms:**
   - Payment terms requested
   - Validity period needed
   - Any volume discounts or tiered pricing mentioned

3. Flag anything missing from the RFQ that the quoting team needs to clarify with the client before quoting.

4. If multiple routes or shipment types are included, produce a comparison table.

5. Estimate quote complexity (simple, moderate, complex) based on number of legs, special handling, and documentation requirements.

## Output Format

```
# RFQ Analysis: [Client Name / Reference]

## Route Summary
| # | Origin | Destination | Mode | Container | Incoterms |
|---|--------|-------------|------|-----------|-----------|
| 1 | [port] | [port]      | [mode] | [type x qty] | [term] |

## Cargo Details
- Commodity: [description]
- Special handling: [requirements or "None"]
- Weight/Volume: [details]

## Service Requirements
- Frequency: [one-time / contract]
- Transit expectation: [days or "not specified"]
- Documentation: [list]

## Missing Information
- [ ] [What needs to be clarified before quoting]

## Quote Complexity: [Simple / Moderate / Complex]
[One-sentence justification]
```
