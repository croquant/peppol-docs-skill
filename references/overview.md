# Peppol BIS Billing 3.0 Overview

## Documentation Structure

The Peppol BIS Billing 3.0 documentation is organized into five main categories:

### 1. Documentation
- Business Interoperability Specifications (BIS)
- BIS compliance
- Release notes

### 2. Syntax
- UBL Invoice
- UBL Credit Note
- Note: All element names are inherited from EN16931, though terminology uses "invoice" for both invoice and credit note documents

### 3. Rules
- EN16931 model bound to UBL (TC434 rules)
- Rules for Peppol BIS 3.0 Billing (PEPPOL-* rules)

### 4. Code Lists
Fourteen standardized code lists covering identifiers, schemes, and classifications

### 5. Downloads
- Schematron validation files (PEPPOL and TC434 rules)
- UBL stylesheet (XSLT)
- Example files (ZIP archive)

---

## Scope

The Peppol BIS addresses "clarifying requirements for ensuring interoperability and provides guidelines for the support and implementation of these requirements." It specifically covers invoice and credit note transactions, establishing a Core Invoice Usage Specification (CIUS) aligned with the European Standard EN 16931.

---

## Key Parties and Roles

The specification identifies two primary parties in billing transactions:

### Parties
- **Customer/Buyer**: The legal entity demanding products or services
- **Supplier/Seller**: The legal entity providing products or services

### Functional Roles
- **Creditor**: The party issuing invoices and claiming payment
- **Debtor**: The party receiving invoices and responsible for settlement

### Additional Optional Parties
- Payees (in factoring scenarios)
- Delivery parties
- Tax representatives

---

## Core Business Requirements

The specification organizes requirements across five functional areas:

### 1. Accounting
Document and line-level information enabling proper financial record-keeping and VAT compliance

### 2. Invoice Verification
Sufficient detail to authenticate transactions and trace related documentation (purchase orders, contracts, delivery records)

### 3. VAT Reporting
Information supporting correct VAT determination and reporting per EU Directive 2006/112/EC

### 4. Auditing
Identification of parties, products, values, quantities, and document linkages

### 5. Payment
Settlement details including amounts due, payment means, and SEPA-compliant bank transfer information

---

## General Invoicing Process

The workflow encompasses:

1. **Supplier issues and sends invoice** - Referencing orders and delivered goods/services
2. **Customer receives invoice** and either:
   - Approves and processes for payment
   - Completely rejects it
   - Disputes portions and requests credit notes

### Supported Invoicing Processes

The specification supports nine distinct invoicing processes, ranging from:
- Standard purchase order-based invoicing
- Pre-payment scenarios
- Spot payment scenarios
- Credit notes and negative invoices for corrections

---

## Specification Identifiers

### CustomizationID (Mandatory)
Default: `urn:cen.eu:en16931:2017#compliant#urn:fdc:peppol.eu:2017:poacc:billing:3.0`

This identifies that the document complies with both:
- EN16931 European Standard
- Peppol BIS Billing 3.0 specification

### ProfileID (Mandatory)
Default: `urn:fdc:peppol.eu:2017:poacc:billing:01:1.0`

This identifies the business process type.

---

## Key Compliance Points

1. **EN16931 Compliance**: The specification is a CIUS (Core Invoice Usage Specification) of the European Standard EN 16931
2. **VAT Directive**: Complies with EU Directive 2006/112/EC
3. **Interoperability**: Ensures cross-border electronic invoice exchange
4. **Validation**: Two-layer validation (EN16931 rules + Peppol-specific rules)
