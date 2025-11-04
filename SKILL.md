---
name: peppol-docs
description: This skill should be used when working with Peppol BIS Billing 3.0 specifications, validating UBL Invoice or Credit Note documents against Peppol compliance rules, understanding Peppol requirements, or debugging Peppol validation errors. Use this skill for questions about Peppol billing compliance, UBL syntax, mandatory fields, VAT handling, validation rules (PEPPOL-* and BR-* rules), or code lists used in Peppol documents.
---

# Peppol BIS Billing 3.0 Documentation

## Overview

Provide comprehensive knowledge of the Peppol BIS (Business Interoperability Specifications) Billing 3.0 standard for electronic invoicing and credit notes. Enable validation, debugging, and implementation of Peppol-compliant UBL documents.

**Scope:**
- Peppol BIS Billing 3.0 specification (compliant with EN16931 European Standard)
- UBL Invoice and Credit Note syntax
- Validation rules (PEPPOL-* and BR-* rules)
- Code lists and standardized values
- VAT compliance and tax handling

## When to Use This Skill

Invoke this skill when:
- Validating UBL Invoice or Credit Note documents for Peppol compliance
- Understanding Peppol billing requirements and specifications
- Debugging Peppol validation errors (e.g., "PEPPOL-EN16931-R003 failed")
- Implementing Peppol-compliant billing document generation
- Questions about mandatory fields, optional elements, or cardinality
- Understanding VAT category handling and tax calculations
- Working with Peppol code lists (currency codes, country codes, payment means, etc.)
- Verifying party identification and electronic address requirements

## Reference Documentation

This skill includes comprehensive reference files organized by topic. Load these files as needed to answer specific questions:

### Core Specification Files

**`references/overview.md`**
- Peppol BIS Billing 3.0 scope and purpose
- Key parties and roles
- Core business requirements (Accounting, VAT Reporting, Payment, etc.)
- General invoicing processes
- Specification identifiers (CustomizationID, ProfileID)

**Use when:** Understanding the overall Peppol framework, business requirements, or specification structure.

### UBL Syntax Files

**`references/ubl-invoice-syntax.md`**
- Complete UBL Invoice structure and namespaces
- Mandatory vs. optional elements with cardinality
- Party structures (Supplier, Customer, Payee, Tax Representative)
- Tax Total and Legal Monetary Total structures
- Invoice Line structure and item details
- Common type codes and unit codes

**`references/ubl-creditnote-syntax.md`**
- Complete UBL Credit Note structure
- Differences from Invoice (root element, type codes, line elements)
- Billing Reference structure
- Credit note use cases and scenarios

**Use when:** Understanding document structure, element requirements, XML structure, or implementing UBL document generation.

### Validation Rules Files

**`references/validation-rules-peppol.md`**
- PEPPOL-COMMON-R* rules (country-specific identifier formats)
- PEPPOL-EN16931-CL* rules (code list compliance)
- PEPPOL-EN16931-F* rules (date formatting)
- PEPPOL-EN16931-P* rules (profile requirements, type codes, VAT exemption mappings)
- PEPPOL-EN16931-R* rules (business logic, electronic addresses, currencies, allowances/charges, payments, line items)
- 40 total Peppol-specific rules with severity levels (fatal/warning)

**`references/validation-rules-en16931.md`**
- BR-* rules (EN16931 European Standard business rules)
- Core invoice requirements (BR-01 to BR-20)
- Line item rules (BR-21 to BR-30)
- Allowances & charges (BR-31 to BR-44)
- VAT requirements (BR-45 to BR-48)
- Specialized VAT category rules (BR-AE, BR-G, BR-IC, BR-E, BR-Z, BR-S, etc.)
- Code list compliance (BR-CL-*)
- Consistency rules (BR-CO-*)
- Decimal precision rules (BR-DEC-*)

**Use when:** Debugging validation errors, understanding specific rule requirements, or implementing validation logic.

### Code Lists File

**`references/code-lists.md`**
- Currency codes (ISO 4217)
- Country codes (ISO 3166-1 Alpha-2)
- Electronic Address Scheme (EAS) codes
- VAT category codes (UNCL 5305)
- Invoice and Credit Note type codes (UNCL 1001)
- Payment means codes (UNCL 4461)
- Allowance and charge reason codes (UNCL 5189, 7161)
- VAT exemption reason codes (VATEX)
- Unit of measure codes (UN/ECE Recommendation 20)
- MIME type codes
- Item classification codes (UNCL 7143)

**Use when:** Looking up valid code values, understanding code meanings, or validating code list compliance.

## Common Usage Patterns

### Pattern 1: Debugging Validation Errors

When encountering a Peppol validation error:

1. Identify the rule ID (e.g., "PEPPOL-EN16931-R003", "BR-CO-04")
2. Search the appropriate validation rules file:
   - PEPPOL-* rules → `references/validation-rules-peppol.md`
   - BR-* rules → `references/validation-rules-en16931.md`
3. Understand the rule requirement and fix the document accordingly

**Example workflow:**
```
Error: "PEPPOL-EN16931-R003: A buyer reference or purchase order reference MUST be provided"

Steps:
1. Read references/validation-rules-peppol.md
2. Find PEPPOL-EN16931-R003 in "Business Rules" section
3. Understand: Either cbc:BuyerReference or cac:OrderReference/cbc:ID must be present
4. Add the missing element to the UBL document
```

### Pattern 2: Understanding Document Structure

When implementing UBL document generation:

1. Read the appropriate syntax file:
   - For invoices → `references/ubl-invoice-syntax.md`
   - For credit notes → `references/ubl-creditnote-syntax.md`
2. Review mandatory elements (1..1 cardinality)
3. Understand party structures, tax totals, and line items
4. Implement document generation with proper structure

### Pattern 3: Validating Code Values

When working with codes (type codes, VAT categories, payment means, etc.):

1. Read `references/code-lists.md`
2. Find the relevant code list section
3. Verify the code value is in the allowed list
4. Understand the code's meaning and usage context

### Pattern 4: Understanding VAT Requirements

When handling VAT scenarios:

1. Identify the VAT category (S, Z, E, AE, K, G, O, L, M)
2. Read `references/code-lists.md` for VAT category descriptions
3. Read `references/validation-rules-en16931.md` for category-specific BR-* rules
4. Check if VAT rate is required, if exemption reason is needed, etc.
5. Verify party VAT identifiers are present when required

## Key Compliance Points

### Mandatory Specification Identifiers

Every Peppol invoice/credit note MUST have:

```xml
<cbc:CustomizationID>urn:cen.eu:en16931:2017#compliant#urn:fdc:peppol.eu:2017:poacc:billing:3.0</cbc:CustomizationID>
<cbc:ProfileID>urn:fdc:peppol.eu:2017:poacc:billing:01:1.0</cbc:ProfileID>
```

### Electronic Addresses

Both seller and buyer MUST have electronic addresses with scheme identifiers:

```xml
<!-- Seller -->
<cac:AccountingSupplierParty>
    <cac:Party>
        <cbc:EndpointID schemeID="0192">987654321</cbc:EndpointID>
        ...
    </cac:Party>
</cac:AccountingSupplierParty>

<!-- Buyer -->
<cac:AccountingCustomerParty>
    <cac:Party>
        <cbc:EndpointID schemeID="0088">1234567890123</cbc:EndpointID>
        ...
    </cac:Party>
</cac:AccountingCustomerParty>
```

### Buyer Reference Requirement

Either buyer reference OR purchase order reference MUST be provided (PEPPOL-EN16931-R003):

```xml
<!-- Option 1: Buyer Reference -->
<cbc:BuyerReference>BUYER-REF-123</cbc:BuyerReference>

<!-- Option 2: Order Reference -->
<cac:OrderReference>
    <cbc:ID>ORDER-123</cbc:ID>
</cac:OrderReference>
```

### Date Formatting

All dates MUST use YYYY-MM-DD format (PEPPOL-EN16931-F001):

```xml
<cbc:IssueDate>2024-01-15</cbc:IssueDate>
<cbc:DueDate>2024-02-15</cbc:DueDate>
```

### Document-Level Notes

Only ONE note allowed at document level (unless both parties are German organizations - PEPPOL-EN16931-R002):

```xml
<cbc:Note>Invoice note text here</cbc:Note>
<!-- Only one allowed! -->
```

## Working with This Skill

### Search Strategies

When searching for specific information in reference files:

**For validation rules:**
```bash
# Search for specific rule ID
grep "PEPPOL-EN16931-R003" references/validation-rules-peppol.md
grep "BR-CO-04" references/validation-rules-en16931.md

# Search for topic
grep -i "electronic address" references/validation-rules-peppol.md
grep -i "vat category" references/validation-rules-en16931.md
```

**For syntax elements:**
```bash
# Find specific element
grep "cbc:BuyerReference" references/ubl-invoice-syntax.md
grep "cac:TaxTotal" references/ubl-invoice-syntax.md
```

**For code lists:**
```bash
# Find specific codes
grep "0192" references/code-lists.md  # Norwegian organization number
grep "Payment means" references/code-lists.md
grep "VATEX" references/code-lists.md
```

### Progressive Loading

Load reference files progressively based on the question:

1. **General questions** → Start with `references/overview.md`
2. **Syntax/structure questions** → Load syntax files
3. **Validation errors** → Load specific validation rules file
4. **Code lookup** → Load `references/code-lists.md`

Avoid loading all files at once; load only what's needed for the specific question.

## Common Questions and Reference Mapping

| Question Type | Primary Reference File |
|---------------|------------------------|
| "What is Peppol BIS Billing?" | overview.md |
| "What are the mandatory fields for an invoice?" | ubl-invoice-syntax.md |
| "How do I structure a credit note?" | ubl-creditnote-syntax.md |
| "What does PEPPOL-EN16931-R003 mean?" | validation-rules-peppol.md |
| "What does BR-CO-04 require?" | validation-rules-en16931.md |
| "What VAT category codes are allowed?" | code-lists.md |
| "What payment means codes exist?" | code-lists.md |
| "What is EAS code 0192?" | code-lists.md |
| "How should VAT reverse charge be handled?" | validation-rules-en16931.md (BR-AE rules) |
| "What's the format for Norwegian org numbers?" | validation-rules-peppol.md (PEPPOL-COMMON-R041) |

## Additional Resources

**Official Peppol Documentation:**
- Full specification: https://docs.peppol.eu/poacc/billing/3.0/
- Schematron validation files: https://docs.peppol.eu/poacc/billing/3.0/downloads/
- Example files: Available in specification downloads

**Standards Referenced:**
- EN16931: European Standard for electronic invoicing
- UBL 2.1: Universal Business Language
- ISO 4217: Currency codes
- ISO 3166-1: Country codes
- UN/CEFACT code lists: UNCL 1001, 4461, 5189, 5305, 7161, etc.

## Notes

- All PEPPOL-* rules have **fatal** severity (except PEPPOL-COMMON-R044 through R047 which are warnings)
- All BR-* rules have **fatal** severity (except BR-51 which is a warning)
- Currency amounts limited to 2 decimal places (BR-DEC-* rules)
- Empty elements not allowed (PEPPOL-EN16931-R008)
- The specification supports both invoices and credit notes with nearly identical structures
