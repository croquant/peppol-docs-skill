# EN16931 (TC434) Validation Rules - BR-* Rules

This document contains EN16931 business rules (BR-*) that apply to Peppol BIS Billing 3.0. These are the foundational European Standard rules that underpin all Peppol billing documents.

**Rule Severity:**
- Most BR-* rules have **fatal** severity
- BR-51 and most UBL-CR-* rules have **warning** severity

---

## Core Invoice Requirements (BR-01 to BR-20)

These rules mandate essential invoice components that MUST be present.

### Document Identifiers and Basic Information

| Rule ID | Description | Element | Severity |
|---------|-------------|---------|----------|
| BR-01 | An Invoice shall have a Specification identifier | `cbc:CustomizationID` | fatal |
| BR-02 | An Invoice shall have an Invoice number | `cbc:ID` | fatal |
| BR-03 | An Invoice shall have an Invoice issue date | `cbc:IssueDate` | fatal |
| BR-04 | An Invoice shall have an Invoice type code | `cbc:InvoiceTypeCode` or `cbc:CreditNoteTypeCode` | fatal |
| BR-05 | An Invoice shall have an Invoice currency code | `cbc:DocumentCurrencyCode` | fatal |

### Party Information

| Rule ID | Description | Element | Severity |
|---------|-------------|---------|----------|
| BR-06 | An Invoice shall contain the Seller name | `cac:AccountingSupplierParty/cac:Party/cac:PartyLegalEntity/cbc:RegistrationName` | fatal |
| BR-07 | An Invoice shall contain the Buyer name | `cac:AccountingCustomerParty/cac:Party/cac:PartyLegalEntity/cbc:RegistrationName` | fatal |
| BR-08 | An Invoice shall contain the Seller postal address | `cac:AccountingSupplierParty/cac:Party/cac:PostalAddress` | fatal |
| BR-09 | The Seller postal address shall contain a Seller country code | `cac:AccountingSupplierParty/.../cac:Country/cbc:IdentificationCode` | fatal |
| BR-10 | An Invoice shall contain the Buyer postal address | `cac:AccountingCustomerParty/cac:Party/cac:PostalAddress` | fatal |
| BR-11 | The Buyer postal address shall contain a Buyer country code | `cac:AccountingCustomerParty/.../cac:Country/cbc:IdentificationCode` | fatal |

### Financial Totals

| Rule ID | Description | Element | Severity |
|---------|-------------|---------|----------|
| BR-12 | An Invoice shall have the Sum of Invoice line net amount | `cac:LegalMonetaryTotal/cbc:LineExtensionAmount` | fatal |
| BR-13 | An Invoice shall have the Invoice total amount without VAT | `cac:LegalMonetaryTotal/cbc:TaxExclusiveAmount` | fatal |
| BR-14 | An Invoice shall have the Invoice total amount with VAT | `cac:LegalMonetaryTotal/cbc:TaxInclusiveAmount` | fatal |
| BR-15 | An Invoice shall have the Amount due for payment | `cac:LegalMonetaryTotal/cbc:PayableAmount` | fatal |

### Line Items and Conditional Requirements

| Rule ID | Description | Element | Severity |
|---------|-------------|---------|----------|
| BR-16 | An Invoice shall have at least one Invoice line | `cac:InvoiceLine` or `cac:CreditNoteLine` | fatal |
| BR-17 | The Payee name shall be provided if the Payee is different from the Seller | `cac:PayeeParty/cac:PartyName/cbc:Name` | fatal |
| BR-18 | The Seller tax representative name shall be provided if the Seller has a tax representative | `cac:TaxRepresentativeParty/cac:PartyName/cbc:Name` | fatal |
| BR-19 | The Seller tax representative postal address shall be provided if the Seller has a tax representative | `cac:TaxRepresentativeParty/cac:PostalAddress` | fatal |
| BR-20 | The Seller tax representative postal address shall contain a Tax representative country code if the Seller has a tax representative | `cac:TaxRepresentativeParty/.../cbc:IdentificationCode` | fatal |

---

## Line Item Rules (BR-21 to BR-30)

### Basic Line Requirements

| Rule ID | Description | Element | Severity |
|---------|-------------|---------|----------|
| BR-21 | Each Invoice line shall have an Invoice line identifier | `cac:InvoiceLine/cbc:ID` | fatal |
| BR-22 | Each Invoice line shall have an Invoiced quantity | `cac:InvoiceLine/cbc:InvoicedQuantity` | fatal |
| BR-23 | An Invoice line shall have an Invoiced quantity unit of measure code | `cac:InvoiceLine/cbc:InvoicedQuantity/@unitCode` | fatal |
| BR-24 | Each Invoice line shall have an Invoice line net amount | `cac:InvoiceLine/cbc:LineExtensionAmount` | fatal |
| BR-25 | Each Invoice line shall contain the Item name | `cac:InvoiceLine/cac:Item/cbc:Name` | fatal |
| BR-26 | Each Invoice line shall contain the Item net price | `cac:InvoiceLine/cac:Price/cbc:PriceAmount` | fatal |

### Price and Period Validation

| Rule ID | Description | Severity |
|---------|-------------|----------|
| BR-27 | The Item net price shall NOT be negative | fatal |
| BR-28 | The Item gross price shall NOT be negative | fatal |
| BR-29 | If both Invoice line period start date and Invoice line period end date are given, the Invoice line period end date shall be later or equal to the Invoice line period start date | fatal |
| BR-30 | If both Invoicing period start date and Invoicing period end date are given, the Invoicing period end date shall be later or equal to the Invoicing period start date | fatal |

---

## Allowances & Charges (BR-31 to BR-44)

### Document Level Allowances

| Rule ID | Description | Element | Severity |
|---------|-------------|---------|----------|
| BR-31 | Each Document level allowance shall have a Document level allowance amount | `cac:AllowanceCharge/cbc:Amount` | fatal |
| BR-32 | Each Document level allowance shall have a Document level allowance VAT category code | `cac:AllowanceCharge/cac:TaxCategory/cbc:ID` | fatal |
| BR-33 | Each Document level allowance shall have a Document level allowance reason | `cac:AllowanceCharge/cbc:AllowanceChargeReason` or `AllowanceChargeReasonCode` | fatal |

### Document Level Charges

| Rule ID | Description | Element | Severity |
|---------|-------------|---------|----------|
| BR-36 | Each Document level charge shall have a Document level charge amount | `cac:AllowanceCharge/cbc:Amount` | fatal |
| BR-37 | Each Document level charge shall have a Document level charge VAT category code | `cac:AllowanceCharge/cac:TaxCategory/cbc:ID` | fatal |
| BR-38 | Each Document level charge shall have a Document level charge reason | `cac:AllowanceCharge/cbc:AllowanceChargeReason` or `AllowanceChargeReasonCode` | fatal |

### Line Level Allowances and Charges

| Rule ID | Description | Element | Severity |
|---------|-------------|---------|----------|
| BR-41 | Each Invoice line allowance shall have an Invoice line allowance amount | `cac:InvoiceLine/cac:AllowanceCharge/cbc:Amount` | fatal |
| BR-42 | Each Invoice line allowance shall have an Invoice line allowance reason | `cac:InvoiceLine/cac:AllowanceCharge/cbc:AllowanceChargeReason` or code | fatal |
| BR-43 | Each Invoice line charge shall have an Invoice line charge amount | `cac:InvoiceLine/cac:AllowanceCharge/cbc:Amount` | fatal |
| BR-44 | Each Invoice line charge shall have an Invoice line charge reason | `cac:InvoiceLine/cac:AllowanceCharge/cbc:AllowanceChargeReason` or code | fatal |

---

## VAT Requirements (BR-45 to BR-48)

| Rule ID | Description | Element | Severity |
|---------|-------------|---------|----------|
| BR-45 | Each VAT breakdown shall have a VAT category taxable amount | `cac:TaxTotal/cac:TaxSubtotal/cbc:TaxableAmount` | fatal |
| BR-46 | Each VAT breakdown shall have a VAT category tax amount | `cac:TaxTotal/cac:TaxSubtotal/cbc:TaxAmount` | fatal |
| BR-47 | Each VAT breakdown shall be defined through a VAT category code | `cac:TaxTotal/cac:TaxSubtotal/cac:TaxCategory/cbc:ID` | fatal |
| BR-48 | Each VAT breakdown shall have a VAT category rate, except if the Invoice is not subject to VAT | `cac:TaxTotal/cac:TaxSubtotal/cac:TaxCategory/cbc:Percent` | fatal |

**Common VAT Category Codes:**
- **S**: Standard rate
- **Z**: Zero rated goods
- **E**: Exempt from tax
- **AE**: VAT Reverse Charge
- **K**: Intra-Community supply
- **G**: Free export item, tax not charged
- **O**: Services outside scope of tax
- **L**: Canary Islands general indirect tax
- **M**: Tax for production, services and importation in Ceuta and Melilla

---

## Payment & Documentation (BR-49 to BR-67)

### Payment Means

| Rule ID | Description | Element | Severity |
|---------|-------------|---------|----------|
| BR-49 | A Payment instruction shall specify the Payment means type code | `cac:PaymentMeans/cbc:PaymentMeansCode` | fatal |
| BR-50 | A Payment account identifier shall be present if Credit transfer information is provided | `cac:PaymentMeans/cac:PayeeFinancialAccount/cbc:ID` | fatal |
| BR-51 | The last 4 to 6 digits of the Payment card primary account number shall be present if Payment card information is provided | `cac:PaymentMeans/cac:CardAccount/cbc:PrimaryAccountNumberID` | **warning** |

**Common Payment Means Codes (UNCL 4461):**
- **1**: Instrument not defined
- **10**: In cash
- **30**: Credit transfer
- **31**: Debit transfer
- **42**: Payment to bank account
- **48**: Bank card
- **49**: Direct debit
- **57**: Standing agreement
- **58**: SEPA credit transfer
- **59**: SEPA direct debit

### Supporting Documents

| Rule ID | Description | Element | Severity |
|---------|-------------|---------|----------|
| BR-52 | Each Additional supporting document shall contain a Supporting document reference | `cac:AdditionalDocumentReference/cbc:ID` | fatal |

### Cardinality Constraints

| Rule ID | Description | Severity |
|---------|-------------|----------|
| BR-61 | If the Payment means type code means SEPA credit transfer, Local credit transfer or Non-SEPA international credit transfer, the Payment account identifier shall be present | fatal |
| BR-62 | The Seller electronic address shall have a Scheme identifier | fatal |
| BR-63 | The Buyer electronic address shall have a Scheme identifier | fatal |
| BR-64 | The Item classification identifier shall have a Scheme identifier | fatal |

---

## Specialized VAT Category Rules

### Reverse Charge (BR-AE-*)

| Rule ID | Description | Severity |
|---------|-------------|----------|
| BR-AE-01 | An Invoice that contains an Invoice line, Document level allowance or Document level charge where the VAT category code is "Reverse charge" shall contain the Seller VAT Identifier, the Seller tax registration identifier and/or the Seller tax representative VAT identifier | fatal |
| BR-AE-02 | An Invoice that contains an Invoice line where the Invoiced item VAT category code is "Reverse charge" shall contain the Buyer VAT identifier or the Buyer tax registration identifier | fatal |
| BR-AE-08 | In a VAT breakdown where the VAT category code is "Reverse charge" the VAT category taxable amount shall equal the sum of Invoice line net amounts minus the sum of Document level allowance amounts plus the sum of Document level charge amounts where the VAT category code is "Reverse charge" | fatal |
| BR-AE-09 | The VAT category tax amount in a VAT breakdown where the VAT category code is "Reverse charge" shall be 0 (zero) | fatal |
| BR-AE-10 | A VAT Breakdown with VAT Category code "Reverse charge" shall have a VAT exemption reason code or a VAT exemption reason text | fatal |

### Export (BR-G-*)

| Rule ID | Description | Severity |
|---------|-------------|----------|
| BR-G-01 | An Invoice that contains an Invoice line where the Invoiced item VAT category code is "Export outside the EU" shall contain the Seller VAT Identifier or the Seller tax representative VAT identifier | fatal |
| BR-G-08 | In a VAT breakdown where the VAT category code is "Export outside the EU" the VAT category taxable amount shall equal the sum of Invoice line net amounts minus the sum of Document level allowance amounts plus the sum of Document level charge amounts where the VAT category code is "Export outside the EU" | fatal |
| BR-G-09 | The VAT category tax amount in a VAT breakdown where the VAT category code is "Export outside the EU" shall be 0 (zero) | fatal |
| BR-G-10 | A VAT Breakdown with the VAT Category code "Export outside the EU" shall have a VAT exemption reason code or a VAT exemption reason text | fatal |

### Intra-Community Supply (BR-IC-*/BR-K-*)

| Rule ID | Description | Severity |
|---------|-------------|----------|
| BR-IC-01 | An Invoice that contains an Invoice line where the Invoiced item VAT category code is "Intra-Community supply" shall contain the Seller VAT Identifier or the Seller tax representative VAT identifier | fatal |
| BR-IC-02 | An Invoice that contains an Invoice line where the Invoiced item VAT category code is "Intra-Community supply" shall contain the Buyer VAT identifier | fatal |
| BR-IC-08 | In a VAT breakdown where the VAT category code is "Intra-Community supply" the VAT category taxable amount shall equal the sum of Invoice line net amounts minus the sum of Document level allowance amounts plus the sum of Document level charge amounts where the VAT category code is "Intra-Community supply" | fatal |
| BR-IC-09 | The VAT category tax amount in a VAT breakdown where the VAT category code is "Intra-Community supply" shall be 0 (zero) | fatal |
| BR-IC-10 | A VAT Breakdown with the VAT Category code "Intra-Community supply" shall have a VAT exemption reason code or a VAT exemption reason text | fatal |

### Exempt from Tax (BR-E-*)

| Rule ID | Description | Severity |
|---------|-------------|----------|
| BR-E-01 | An Invoice that contains an Invoice line where the Invoiced item VAT category code is "Exempt from VAT" shall contain the Seller VAT Identifier, the Seller tax registration identifier and/or the Seller tax representative VAT identifier | fatal |
| BR-E-08 | In a VAT breakdown where the VAT category code is "Exempt from VAT" the VAT category taxable amount shall equal the sum of Invoice line net amounts minus the sum of Document level allowance amounts plus the sum of Document level charge amounts where the VAT category code is "Exempt from VAT" | fatal |
| BR-E-09 | The VAT category tax amount in a VAT breakdown where the VAT category code is "Exempt from VAT" shall be 0 (zero) | fatal |
| BR-E-10 | A VAT Breakdown with the VAT Category code "Exempt from VAT" shall have a VAT exemption reason code or a VAT exemption reason text | fatal |

### Zero Rated (BR-Z-*)

| Rule ID | Description | Severity |
|---------|-------------|----------|
| BR-Z-01 | An Invoice that contains an Invoice line where the Invoiced item VAT category code is "Zero rated" shall contain the Seller VAT Identifier, the Seller tax registration identifier and/or the Seller tax representative VAT identifier | fatal |
| BR-Z-08 | In a VAT breakdown where the VAT category code is "Zero rated" the VAT category taxable amount shall equal the sum of Invoice line net amounts minus the sum of Document level allowance amounts plus the sum of Document level charge amounts where the VAT category code is "Zero rated" | fatal |
| BR-Z-09 | The VAT category tax amount in a VAT breakdown where the VAT category code is "Zero rated" shall be 0 (zero) | fatal |

### Standard Rate (BR-S-*)

| Rule ID | Description | Severity |
|---------|-------------|----------|
| BR-S-01 | An Invoice that contains an Invoice line where the Invoiced item VAT category code is "Standard rated" shall contain the Seller VAT Identifier or the Seller tax representative VAT identifier | fatal |
| BR-S-08 | For each different value of VAT category rate where the VAT category code is "Standard rated", the VAT category taxable amount in a VAT breakdown shall equal the sum of Invoice line net amounts plus the sum of document level charge amounts minus the sum of document level allowance amounts where the VAT category code is "Standard rated" and the VAT rate equals the VAT category rate | fatal |
| BR-S-09 | The VAT category tax amount in a VAT breakdown where the VAT category code is "Standard rated" shall equal the VAT category taxable amount multiplied by the VAT category rate | fatal |

### Other Specialized Categories

Similar patterns apply to:
- **BR-IGIC-\***: IGIC (Canary Islands)
- **BR-IPSI-\***: IPSI (Ceuta/Melilla)
- **BR-O-\***: Not subject to VAT
- **BR-L-\***: Canary Islands general indirect tax
- **BR-M-\***: Tax for production, services and importation

---

## Code List Compliance (BR-CL-*)

| Rule ID | Description | Code List | Severity |
|---------|-------------|-----------|----------|
| BR-CL-01 | Invoice type code shall be coded using a restriction of UNCL 1001 | UNCL 1001 | fatal |
| BR-CL-02 | Invoice currency code shall be coded using ISO 4217 | ISO 4217 | fatal |
| BR-CL-03 | Tax currency code shall be coded using ISO 4217 | ISO 4217 | fatal |
| BR-CL-04 | Country codes shall be coded using ISO 3166-1 | ISO 3166-1 alpha-2 | fatal |
| BR-CL-05 | Item classification identifier scheme identifier shall be coded using UNCL 7143 | UNCL 7143 | fatal |
| BR-CL-06 | Value added tax point date code shall be coded using UNTDID 2005 (see EN 16931-1:2017, Annex C) | UNTDID 2005 | fatal |
| BR-CL-09 | Payment means code shall be coded using UNCL 4461 | UNCL 4461 | fatal |
| BR-CL-10 | Unit of measure codes shall be coded according to UN/ECE Recommendation 20 with Recommendation 21 codes | UN/ECE Rec. 20 | fatal |
| BR-CL-11 | Invoiced item VAT category code shall be coded using UNCL 5305 | UNCL 5305 | fatal |
| BR-CL-13 | Invoice line allowance reason code shall be coded using UNCL 5189 | UNCL 5189 | fatal |
| BR-CL-14 | Invoice line charge reason code shall be coded using UNCL 7161 | UNCL 7161 | fatal |
| BR-CL-16 | Payment means payment channel code shall be coded using UNCL 4461 | UNCL 4461 | fatal |
| BR-CL-17 | Electronic address scheme identifier shall be coded using CEF EAS code list | CEF EAS | fatal |
| BR-CL-18 | Document level allowance reason code shall be coded using UNCL 5189 | UNCL 5189 | fatal |
| BR-CL-19 | Document level charge reason code shall be coded using UNCL 7161 | UNCL 7161 | fatal |
| BR-CL-20 | Invoice period description code shall be coded using UNCL 2005 | UNCL 2005 | fatal |
| BR-CL-21 | Invoiced object identifier scheme identifier shall be coded using ISO 6523 ICD | ISO 6523 ICD | fatal |
| BR-CL-23 | Item standard identifier shall use the scheme identifier attribute according to the code list | Various | fatal |
| BR-CL-24 | Item classification identifier shall use the scheme identifier attribute according to the code list | Various | fatal |
| BR-CL-25 | Invoice line Allowance reason code shall be coded using UNCL 5189 | UNCL 5189 | fatal |
| BR-CL-26 | Invoice line Charge reason code shall be coded using UNCL 7161 | UNCL 7161 | fatal |

---

## Consistency Rules (BR-CO-*)

### Mathematical Consistency

| Rule ID | Description | Severity |
|---------|-------------|----------|
| BR-CO-01 | Sum of Invoice line net amount shall equal the sum of the Invoice line net amounts | fatal |
| BR-CO-03 | Invoice total amount without VAT shall equal the sum of Invoice line net amounts minus the sum of Document level allowance amounts plus the sum of Document level charge amounts | fatal |
| BR-CO-04 | Invoice total VAT amount shall equal the sum of VAT category tax amounts | fatal |
| BR-CO-05 | Invoice total amount with VAT shall equal Invoice total amount without VAT plus Invoice total VAT amount | fatal |
| BR-CO-09 | The Paid amount shall be less or equal to the Invoice total amount with VAT | fatal |
| BR-CO-10 | Amount due for payment shall equal the Invoice total amount with VAT minus the Paid amount plus the Rounding amount | fatal |
| BR-CO-11 | Sum of allowances on document level shall be equal to the sum of document level allowance amounts | fatal |
| BR-CO-12 | Sum of charges on document level shall be equal to the sum of document level charge amounts | fatal |
| BR-CO-13 | Invoice line net amount shall equal (Invoiced quantity x (Item net price / Item price base quantity)) plus the sum of all Invoice line charges minus the sum of all Invoice line allowances at the Invoice line | fatal |
| BR-CO-14 | Invoice total VAT amount in accounting currency shall equal the sum of VAT category tax amount in accounting currency | fatal |
| BR-CO-15 | Invoice line net amount shall equal Invoice line quantity multiplied by the Invoice net price/base quantity reduced by the sum of the Invoice line allowance amounts and increased by the sum of the Invoice line charge amounts | fatal |
| BR-CO-16 | Amount due for payment shall be greater than or equal to zero | fatal |
| BR-CO-17 | VAT category tax amount shall equal the VAT category taxable amount multiplied by the VAT category rate | fatal |
| BR-CO-18 | An Invoice shall at least have one VAT breakdown group | fatal |
| BR-CO-25 | In case the Amount due for payment is positive, either the Payment due date or the Payment terms shall be present | fatal |
| BR-CO-26 | In order for the buyer to automatically identify a supplier, the Buyer electronic address shall be provided | fatal |

### VAT Identifier Requirements

| Rule ID | Description | Severity |
|---------|-------------|----------|
| BR-CO-08 | Value Added Tax point date shall not be later than the Invoice issue date | fatal |
| BR-CO-19 | If Seller tax representative VAT identifier is present, then the Seller tax representative name shall be present | fatal |
| BR-CO-20 | If Seller tax representative postal address is present, then the Seller tax representative name shall be present | fatal |
| BR-CO-21 | Each Document level allowance shall have a Document level allowance reason code or a Document level allowance reason | fatal |
| BR-CO-22 | Each Document level charge shall have a Document level charge reason code or a Document level charge reason | fatal |
| BR-CO-23 | Each Invoice line allowance shall have an Invoice line allowance reason code or an Invoice line allowance reason | fatal |
| BR-CO-24 | Each Invoice line charge shall have an Invoice line charge reason code or an Invoice line charge reason | fatal |

---

## Decimal Precision (BR-DEC-*)

Financial amounts are limited to 2 decimal places maximum:

| Rule ID | Description | Severity |
|---------|-------------|----------|
| BR-DEC-01 | The maximum number of decimals for Invoice line net amount is 2 | fatal |
| BR-DEC-02 | The maximum number of decimals for Invoice line allowance amount is 2 | fatal |
| BR-DEC-03 | The maximum number of decimals for Invoice line charge amount is 2 | fatal |
| BR-DEC-05 | The maximum number of decimals for Item net price is 2 | fatal |
| BR-DEC-08 | The maximum number of decimals for Document level allowance amount is 2 | fatal |
| BR-DEC-09 | The maximum number of decimals for Document level charge amount is 2 | fatal |
| BR-DEC-10 | The maximum number of decimals for Sum of Invoice line net amount is 2 | fatal |
| BR-DEC-11 | The maximum number of decimals for Sum of allowances on document level is 2 | fatal |
| BR-DEC-12 | The maximum number of decimals for Sum of charges on document level is 2 | fatal |
| BR-DEC-13 | The maximum number of decimals for Invoice total amount without VAT is 2 | fatal |
| BR-DEC-14 | The maximum number of decimals for Invoice total VAT amount is 2 | fatal |
| BR-DEC-15 | The maximum number of decimals for Invoice total amount with VAT is 2 | fatal |
| BR-DEC-16 | The maximum number of decimals for Paid amount is 2 | fatal |
| BR-DEC-17 | The maximum number of decimals for Rounding amount is 2 | fatal |
| BR-DEC-18 | The maximum number of decimals for Amount due for payment is 2 | fatal |
| BR-DEC-19 | The maximum number of decimals for VAT category taxable amount is 2 | fatal |
| BR-DEC-20 | The maximum number of decimals for VAT category tax amount is 2 | fatal |

---

## UBL Constraints (UBL-CR-*)

These are best practice warnings against including non-standard UBL extensions:

| Rule ID | Description | Severity |
|---------|-------------|----------|
| UBL-CR-001 | A UBL invoice should not include extensions | warning |
| UBL-CR-002 | A UBL invoice should not include additional information | warning |
| UBL-CR-003 | UBL normative namespace identifier shall be present | fatal |
| UBL-CR-004 | CustomizationID shall have a correct value | fatal |

Most UBL-CR-* rules have **warning** severity and recommend avoiding non-standard UBL elements.

---

## Summary

The EN16931 validation rules provide:
- **Mandatory data elements**: What must be present in every invoice
- **VAT handling**: Detailed rules for different VAT scenarios
- **Mathematical consistency**: Calculation validation
- **Code list compliance**: Standardized values
- **Decimal precision**: Financial amount formatting

All BR-* rules (except BR-51) have **fatal** severity, meaning non-compliance results in document rejection.
