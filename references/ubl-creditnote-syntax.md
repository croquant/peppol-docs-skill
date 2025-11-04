# UBL Credit Note Syntax Specification

## Root Element
**Element:** `ubl:CreditNote`
**Namespace:** `urn:oasis:names:specification:ubl:schema:xsd:CreditNote-2`

---

## Important Note

The Peppol specification uses "invoice" terminology for both invoice and credit note documents. All element names are inherited from EN16931. The main differences between Invoice and CreditNote are:
- Root element (`ubl:Invoice` vs `ubl:CreditNote`)
- Type code element (`cbc:InvoiceTypeCode` vs `cbc:CreditNoteTypeCode`)
- Line element (`cac:InvoiceLine` vs `cac:CreditNoteLine`)

**The structure, mandatory/optional elements, and business rules are otherwise identical.**

---

## Cardinality Reference

- **1..1**: Exactly one required
- **1..n**: One or more required
- **1..2**: One to two required
- **0..1**: Zero or one optional
- **0..n**: Zero or more optional

---

## Mandatory Elements (1..1 cardinality)

### Specification and Process Identifiers

| Element | Purpose | Notes |
|---------|---------|-------|
| `cbc:CustomizationID` | Specification identifier | Default: `urn:cen.eu:en16931:2017#compliant#urn:fdc:peppol.eu:2017:poacc:billing:3.0` |
| `cbc:ProfileID` | Business process type | Default: `urn:fdc:peppol.eu:2017:poacc:billing:01:1.0` |

### Document Identification

| Element | Purpose | Notes |
|---------|---------|-------|
| `cbc:ID` | Credit note number | Must uniquely identify credit note within seller's records |
| `cbc:IssueDate` | Issue date | Format: YYYY-MM-DD |
| `cbc:CreditNoteTypeCode` | Functional type | Example: 381 (credit note) |
| `cbc:DocumentCurrencyCode` | Document currency | Single currency for all amounts (e.g., EUR, USD - ISO 4217) |

### Parties

| Element | Purpose | Notes |
|---------|---------|-------|
| `cac:AccountingSupplierParty` | Seller information | Required group containing seller details |
| `cac:AccountingCustomerParty` | Buyer information | Required group containing buyer details |

### Financial Totals

| Element | Purpose | Notes |
|---------|---------|-------|
| `cac:TaxTotal` | Tax totals | 1-2 instances; two required if tax currency differs from document currency |
| `cac:LegalMonetaryTotal` | Document totals | Monetary summary |

### Line Items

| Element | Purpose | Notes |
|---------|---------|-------|
| `cac:CreditNoteLine` | Line items | Minimum one line required (1..n) |

---

## Optional Elements

### Document-Level Optional Elements (0..1)

| Element | Purpose | Example/Notes |
|---------|---------|---------------|
| `cbc:DueDate` | Payment due date | Format: YYYY-MM-DD |
| `cbc:TaxPointDate` | Tax point date | VAT accounting date |
| `cbc:Note` | Document-level note | Free text (max 1 note unless German B2B) |
| `cbc:TaxCurrencyCode` | Tax currency code | When different from document currency |
| `cbc:AccountingCost` | Accounting cost code | Buyer's accounting reference |
| `cbc:BuyerReference` | Buyer reference | Purchase order or contract reference |
| `cac:InvoicePeriod` | Billing period | Start and end dates |
| `cac:OrderReference` | Purchase order reference | Reference to order document |
| `cac:ContractDocumentReference` | Contract reference | Reference to contract |
| `cac:DespatchDocumentReference` | Despatch advice reference | Delivery documentation |
| `cac:ReceiptDocumentReference` | Receipt advice reference | Receipt confirmation |
| `cac:OriginatorDocumentReference` | Originating document | Source document reference |
| `cac:PayeeParty` | Payee party | When different from seller (factoring) |
| `cac:TaxRepresentativeParty` | Tax representative | VAT representative details |
| `cac:Delivery` | Delivery information | Delivery details and location |
| `cac:PaymentTerms` | Payment terms | Payment conditions |

### Repeatable Optional Elements (0..n)

| Element | Purpose | Example/Notes |
|---------|---------|---------------|
| `cac:BillingReference` | Referenced invoice | Reference to original invoice being credited |
| `cac:AdditionalDocumentReference` | Supporting documents | Attachments, references, etc. |
| `cac:PaymentMeans` | Payment instructions | Bank account, payment card, etc. |
| `cac:AllowanceCharge` | Document-level adjustments | Discounts or charges |

---

## Common Credit Note Type Codes (UNCL 1001 subset)

| Code | Description |
|------|-------------|
| 381 | Credit note |
| 396 | Factored credit note |
| 532 | Forwarder's credit note |

---

## Billing Reference Structure

Credit notes typically reference the original invoice(s) being credited:

```xml
<cac:BillingReference>
    <cac:InvoiceDocumentReference>
        <cbc:ID>INV-2024-001</cbc:ID> <!-- 1..1 Original invoice number -->
        <cbc:IssueDate>2024-01-15</cbc:IssueDate> <!-- 0..1 Original invoice date -->
    </cac:InvoiceDocumentReference>
</cac:BillingReference>
```

---

## Credit Note Line Structure

```xml
<cac:CreditNoteLine>
    <cbc:ID>1</cbc:ID> <!-- 1..1 Line identifier -->
    <cbc:Note>Line note</cbc:Note> <!-- 0..1 -->
    <cbc:CreditedQuantity unitCode="C62">10</cbc:CreditedQuantity> <!-- 1..1 -->
    <cbc:LineExtensionAmount currencyID="EUR">100.00</cbc:LineExtensionAmount> <!-- 1..1 -->
    <cbc:AccountingCost>Project 123</cbc:AccountingCost> <!-- 0..1 -->

    <cac:InvoicePeriod> <!-- 0..1 -->
        <cbc:StartDate>2024-01-01</cbc:StartDate> <!-- 0..1 -->
        <cbc:EndDate>2024-01-31</cbc:EndDate> <!-- 0..1 -->
    </cac:InvoicePeriod>

    <cac:OrderLineReference> <!-- 0..1 -->
        <cbc:LineID>1</cbc:LineID> <!-- 1..1 -->
    </cac:OrderLineReference>

    <cac:DocumentReference> <!-- 0..n -->
        <cbc:ID>DOC123</cbc:ID> <!-- 1..1 -->
        <cbc:DocumentTypeCode>130</cbc:DocumentTypeCode> <!-- 0..1 -->
    </cac:DocumentReference>

    <cac:AllowanceCharge> <!-- 0..n -->
        <cbc:ChargeIndicator>false</cbc:ChargeIndicator> <!-- 1..1 -->
        <cbc:AllowanceChargeReasonCode>95</cbc:AllowanceChargeReasonCode> <!-- 0..1 -->
        <cbc:AllowanceChargeReason>Discount</cbc:AllowanceChargeReason> <!-- 0..1 -->
        <cbc:MultiplierFactorNumeric>10</cbc:MultiplierFactorNumeric> <!-- 0..1 -->
        <cbc:Amount currencyID="EUR">10.00</cbc:Amount> <!-- 1..1 -->
        <cbc:BaseAmount currencyID="EUR">100.00</cbc:BaseAmount> <!-- 0..1 -->
    </cac:AllowanceCharge>

    <cac:Item> <!-- 1..1 -->
        <cbc:Description>Item description</cbc:Description> <!-- 0..1 -->
        <cbc:Name>Item name</cbc:Name> <!-- 1..1 -->
        <cac:BuyersItemIdentification> <!-- 0..1 -->
            <cbc:ID>BUYER-SKU</cbc:ID> <!-- 1..1 -->
        </cac:BuyersItemIdentification>
        <cac:SellersItemIdentification> <!-- 0..1 -->
            <cbc:ID>SELLER-SKU</cbc:ID> <!-- 1..1 -->
        </cac:SellersItemIdentification>
        <cac:StandardItemIdentification> <!-- 0..1 -->
            <cbc:ID schemeID="0160">1234567890123</cbc:ID> <!-- 1..1 -->
        </cac:StandardItemIdentification>
        <cac:OriginCountry> <!-- 0..1 -->
            <cbc:IdentificationCode>DE</cbc:IdentificationCode> <!-- 1..1 -->
        </cac:OriginCountry>
        <cac:CommodityClassification> <!-- 0..n -->
            <cbc:ItemClassificationCode listID="STI">12345678</cbc:ItemClassificationCode> <!-- 1..1 -->
        </cac:CommodityClassification>
        <cac:ClassifiedTaxCategory> <!-- 1..1 -->
            <cbc:ID>S</cbc:ID> <!-- 1..1 -->
            <cbc:Percent>25.00</cbc:Percent> <!-- 0..1 -->
            <cac:TaxScheme>
                <cbc:ID>VAT</cbc:ID> <!-- 1..1 -->
            </cac:TaxScheme>
        </cac:ClassifiedTaxCategory>
        <cac:AdditionalItemProperty> <!-- 0..n -->
            <cbc:Name>Property name</cbc:Name> <!-- 1..1 -->
            <cbc:Value>Property value</cbc:Value> <!-- 1..1 -->
        </cac:AdditionalItemProperty>
    </cac:Item>

    <cac:Price> <!-- 1..1 -->
        <cbc:PriceAmount currencyID="EUR">10.00</cbc:PriceAmount> <!-- 1..1 -->
        <cbc:BaseQuantity unitCode="C62">1</cbc:BaseQuantity> <!-- 0..1 -->
        <cac:AllowanceCharge> <!-- 0..1 (price discount only) -->
            <cbc:ChargeIndicator>false</cbc:ChargeIndicator> <!-- 1..1 -->
            <cbc:Amount currencyID="EUR">2.00</cbc:Amount> <!-- 1..1 -->
            <cbc:BaseAmount currencyID="EUR">12.00</cbc:BaseAmount> <!-- 0..1 -->
        </cac:AllowanceCharge>
    </cac:Price>
</cac:CreditNoteLine>
```

---

## Party, Tax Total, and Legal Monetary Total Structures

These structures are **identical to the Invoice specification**. Please refer to `ubl-invoice-syntax.md` for:
- Party structure (AccountingSupplierParty/AccountingCustomerParty)
- Tax Total structure
- Legal Monetary Total structure

The only difference is that in credit notes, values typically represent amounts being credited back to the buyer.

---

## Credit Note Use Cases

Credit notes are used in several scenarios:

1. **Full or partial cancellation** of an original invoice
2. **Corrections** to previously issued invoices
3. **Returns** of goods or cancelled services
4. **Price adjustments** after invoice issuance
5. **Billing disputes** resolution

### Negative Invoices vs Credit Notes

Both negative invoices (invoice with negative amounts) and credit notes can be used to correct billing. The choice depends on:
- Local regulations and practices
- Buyer/seller agreement
- Accounting system capabilities

The Peppol specification supports both approaches.
