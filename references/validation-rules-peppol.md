# Peppol-Specific Validation Rules (PEPPOL-* Rules)

This document contains all Peppol BIS Billing 3.0 specific validation rules. These rules are in addition to the EN16931 (BR-*) rules.

**Rule Severity Levels:**
- **fatal**: Must be fixed; document will be rejected
- **warning**: Should be reviewed; document may be accepted

---

## Common Format Rules (PEPPOL-COMMON-R*)

These rules validate country-specific identifier formats.

| Rule ID | Description | Severity | Notes |
|---------|-------------|----------|-------|
| PEPPOL-COMMON-R040 | GLN must have a valid format according to GS1 rules | fatal | Applies to Global Location Number identifiers |
| PEPPOL-COMMON-R041 | Norwegian organization number MUST be stated in the correct format | fatal | 9 digits |
| PEPPOL-COMMON-R042 | Danish organization number (CVR) MUST be stated in the correct format | fatal | 8 digits |
| PEPPOL-COMMON-R043 | Belgian enterprise number MUST be stated in the correct format | fatal | 10 digits (0000.000.000) |
| PEPPOL-COMMON-R044 | IPA Code (Codice Univoco Unità Organizzativa) must be stated in the correct format | warning | Italian recipient code, 6 alphanumeric characters |
| PEPPOL-COMMON-R045 | Tax Code (Codice Fiscale) must be stated in the correct format | warning | Italian tax code, 16 characters |
| PEPPOL-COMMON-R046 | Tax Code (Codice Fiscale) must be stated in the correct format | warning | Italian tax code validation |
| PEPPOL-COMMON-R047 | Italian VAT Code (Partita IVA) must be stated in the correct format | warning | 11 digits starting with country code IT |
| PEPPOL-COMMON-R049 | Swedish organization number MUST be stated in the correct format | fatal | 10 digits (NNNNNNNNNN) |
| PEPPOL-COMMON-R050 | Australian Business Number (ABN) MUST be stated in the correct format | fatal | 11 digits |

---

## EN16931 Compliance - Code List Rules (PEPPOL-EN16931-CL*)

These rules enforce the use of correct code lists.

| Rule ID | Description | Severity | Code List |
|---------|-------------|----------|-----------|
| PEPPOL-EN16931-CL001 | Mime code must be according to subset of IANA code list | fatal | IANA MIME types |
| PEPPOL-EN16931-CL002 | Reason code MUST be according to subset of UNCL 5189 D.16B | fatal | Allowance reason codes |
| PEPPOL-EN16931-CL003 | Reason code MUST be according to UNCL 7161 D.16B | fatal | Charge reason codes |
| PEPPOL-EN16931-CL006 | Invoice period description code must be according to UNCL 2005 D.16B | fatal | VAT date codes |
| PEPPOL-EN16931-CL007 | Currency code must be according to ISO 4217:2005 | fatal | Currency codes (EUR, USD, etc.) |
| PEPPOL-EN16931-CL008 | Electronic address identifier scheme must be from the codelist 'Electronic Address Identifier Scheme' | fatal | EAS code list (e.g., 0088 for GLN, 0192 for NO:ORGNR) |

**Common Electronic Address Schemes (EAS):**
- `0002`: System Information et Repertoire des Entreprise et des Etablissements (SIRENE)
- `0007`: Swedish Organization Number
- `0088`: Global Location Number (GLN)
- `0106`: Dutch Originator's Identification Number
- `0184`: Danish Ministry of the Interior and Health
- `0192`: Norwegian Organization Number (Brønnøysundregistrene)
- `0195`: Singapore Nationwide E-Invoice Framework
- `0201`: Freight Forwarder number
- `9956`: Belgian Crossroad Bank of Enterprises
- `9957`: French VAT number

---

## EN16931 Compliance - Format Rules (PEPPOL-EN16931-F*)

| Rule ID | Description | Severity | Format |
|---------|-------------|----------|--------|
| PEPPOL-EN16931-F001 | A date MUST be formatted YYYY-MM-DD | fatal | ISO 8601 date format |

**Examples:**
- ✅ Correct: `2024-01-15`
- ❌ Incorrect: `15/01/2024`, `01-15-2024`, `2024/01/15`

---

## EN16931 Compliance - Profile Rules (PEPPOL-EN16931-P*)

These rules enforce Peppol-specific profile requirements.

### Invoice/Credit Note Type Codes

| Rule ID | Description | Severity |
|---------|-------------|----------|
| PEPPOL-EN16931-P0100 | Invoice type code MUST be set according to the profile | fatal |
| PEPPOL-EN16931-P0101 | Credit note type code MUST be set according to the profile | fatal |
| PEPPOL-EN16931-P0112 | Invoice type code 326 or 384 are only allowed when both buyer and seller are German organizations | fatal |

**Allowed Invoice Type Codes:** 80, 82, 84, 130, 202, 204, 211, 295, 325, 326 (Germany only), 380, 383, 384 (Germany only), 386, 388, 389, 390, 393, 394, 395, 575, 623, 780, 935

**Allowed Credit Note Type Codes:** 81, 83, 261, 262, 296, 308, 381, 396, 420, 458, 532

### VAT Exemption Reason Code Mappings

These rules ensure correct tax category codes are used with specific VATEX exemption reasons:

| Rule ID | Description | Required Tax Category | Severity |
|---------|-------------|----------------------|----------|
| PEPPOL-EN16931-P0104 | Tax Category G MUST be used when exemption reason code is VATEX-EU-G | G (Export outside EU) | fatal |
| PEPPOL-EN16931-P0105 | Tax Category O MUST be used when exemption reason code is VATEX-EU-O | O (Services outside scope of tax) | fatal |
| PEPPOL-EN16931-P0106 | Tax Category K MUST be used when exemption reason code is VATEX-EU-IC | K (Intra-Community supply) | fatal |
| PEPPOL-EN16931-P0107 | Tax Category AE MUST be used when exemption reason code is VATEX-EU-AE | AE (Reverse charge) | fatal |
| PEPPOL-EN16931-P0108 | Tax Category E MUST be used when exemption reason code is VATEX-EU-D | E (Exempt from tax) | fatal |
| PEPPOL-EN16931-P0109 | Tax Category E MUST be used when exemption reason code is VATEX-EU-F | E (Exempt from tax) | fatal |
| PEPPOL-EN16931-P0110 | Tax Category E MUST be used when exemption reason code is VATEX-EU-I | E (Exempt from tax) | fatal |
| PEPPOL-EN16931-P0111 | Tax Category E MUST be used when exemption reason code is VATEX-EU-J | E (Exempt from tax) | fatal |

---

## EN16931 Compliance - Business Rules (PEPPOL-EN16931-R*)

### Core Requirements

| Rule ID | Description | Severity |
|---------|-------------|----------|
| PEPPOL-EN16931-R001 | Business process MUST be provided | fatal |
| PEPPOL-EN16931-R002 | No more than one note is allowed on document level, unless both the buyer and seller are German organizations | fatal |
| PEPPOL-EN16931-R003 | A buyer reference or purchase order reference MUST be provided | fatal |
| PEPPOL-EN16931-R004 | Specification identifier must equal 'urn:cen.eu:en16931:2017#compliant#urn:fdc:peppol.eu:2017:poacc:billing:3.0' | fatal |
| PEPPOL-EN16931-R007 | Business process MUST be in the format 'urn:fdc:peppol.eu:2017:poacc:billing:NN:1.0' | fatal |
| PEPPOL-EN16931-R008 | Document MUST not contain empty elements | fatal |
| PEPPOL-EN16931-R080 | Only one project reference is allowed on document level | fatal |

**Example ProfileID (Business Process):**
```xml
<cbc:ProfileID>urn:fdc:peppol.eu:2017:poacc:billing:01:1.0</cbc:ProfileID>
```

### Electronic Addresses

| Rule ID | Description | Severity | Element |
|---------|-------------|----------|---------|
| PEPPOL-EN16931-R010 | Buyer electronic address MUST be provided | fatal | `cac:AccountingCustomerParty/cac:Party/cbc:EndpointID` |
| PEPPOL-EN16931-R020 | Seller electronic address MUST be provided | fatal | `cac:AccountingSupplierParty/cac:Party/cbc:EndpointID` |

**Example:**
```xml
<cbc:EndpointID schemeID="0088">1234567890123</cbc:EndpointID>
```

### Currency Rules

| Rule ID | Description | Severity |
|---------|-------------|----------|
| PEPPOL-EN16931-R005 | VAT accounting currency code MUST be different from invoice currency code when provided | fatal |
| PEPPOL-EN16931-R051 | All currencyID attributes must match invoice currency code, except VAT in accounting currency | fatal |

### Allowance/Charge Rules

| Rule ID | Description | Severity |
|---------|-------------|----------|
| PEPPOL-EN16931-R040 | Allowance/charge amount must equal base amount * percentage/100 if both exist | fatal |
| PEPPOL-EN16931-R041 | Allowance/charge base amount MUST be provided when allowance/charge percentage is provided | fatal |
| PEPPOL-EN16931-R042 | Allowance/charge percentage MUST be provided when allowance/charge base amount is provided | fatal |
| PEPPOL-EN16931-R043 | Allowance/charge ChargeIndicator value MUST equal 'true' or 'false' | fatal |
| PEPPOL-EN16931-R044 | Charge on price level is NOT allowed. Only value 'false' allowed | fatal |

**Example Calculation:**
```xml
<cac:AllowanceCharge>
    <cbc:ChargeIndicator>false</cbc:ChargeIndicator>
    <cbc:MultiplierFactorNumeric>10</cbc:MultiplierFactorNumeric> <!-- 10% -->
    <cbc:Amount currencyID="EUR">10.00</cbc:Amount>
    <cbc:BaseAmount currencyID="EUR">100.00</cbc:BaseAmount> <!-- 100 * 10 / 100 = 10 -->
</cac:AllowanceCharge>
```

### Price Rules

| Rule ID | Description | Severity |
|---------|-------------|----------|
| PEPPOL-EN16931-R046 | Item net price MUST equal (Gross price - Allowance amount) when gross price is provided | fatal |
| PEPPOL-EN16931-R121 | Base quantity MUST be a positive number above zero | fatal |
| PEPPOL-EN16931-R130 | Unit code of price base quantity MUST be same as invoiced quantity | fatal |

### Tax Rules

| Rule ID | Description | Severity |
|---------|-------------|----------|
| PEPPOL-EN16931-R053 | Only one tax total with tax subtotals MUST be provided | fatal |
| PEPPOL-EN16931-R054 | Only one tax total without tax subtotals MUST be provided when tax currency code is provided | fatal |
| PEPPOL-EN16931-R055 | Invoice total VAT amount and Invoice total VAT amount in accounting currency MUST have the same operational sign | fatal |

### Payment Rules

| Rule ID | Description | Severity |
|---------|-------------|----------|
| PEPPOL-EN16931-R061 | Mandate reference MUST be provided for direct debit | fatal |

**Example:**
```xml
<cac:PaymentMeans>
    <cbc:PaymentMeansCode>49</cbc:PaymentMeansCode> <!-- Direct Debit -->
    <cac:PaymentMandate>
        <cbc:ID>MANDATE-123</cbc:ID> <!-- Required for direct debit -->
    </cac:PaymentMandate>
</cac:PaymentMeans>
```

### Line Item Rules

| Rule ID | Description | Severity |
|---------|-------------|----------|
| PEPPOL-EN16931-R100 | Only one invoiced object is allowed per line | fatal |
| PEPPOL-EN16931-R101 | Element Document reference can only be used for Invoice line object | fatal |
| PEPPOL-EN16931-R110 | Start date of line period MUST be within invoice period | fatal |
| PEPPOL-EN16931-R111 | End date of line period MUST be within invoice period | fatal |
| PEPPOL-EN16931-R120 | Invoice line net amount MUST equal (Invoiced quantity * (Item net price/item price base quantity) + Sum of invoice line charge amount - sum of invoice line allowance amount | fatal |

**Line Amount Calculation Example:**
```
Given:
- Invoiced quantity: 10 units
- Item net price: 15.00 EUR
- Item price base quantity: 1 unit
- Line charge: 5.00 EUR
- Line allowance: 3.00 EUR

Calculation:
Line Extension Amount = (10 * (15.00/1)) + 5.00 - 3.00 = 152.00 EUR
```

---

## Summary

**Total PEPPOL-specific rules: 40**
- Common format rules: 10
- Code list rules: 6
- Format rules: 1
- Profile rules: 9
- Business rules: 30

All rules except warnings (PEPPOL-COMMON-R044 through R047) have **fatal** severity, meaning non-compliance will result in document rejection.

---

## Schematron Validation

Peppol provides Schematron files for automated validation:
- Download from: https://docs.peppol.eu/poacc/billing/3.0/downloads/
- Files: PEPPOL-EN16931-UBL.sch

These files can be used with Schematron validators to automatically check compliance.
