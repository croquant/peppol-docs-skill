# UBL Invoice Syntax Specification

## Root Element
**Element:** `ubl:Invoice`
**Namespace:** `urn:oasis:names:specification:ubl:schema:xsd:Invoice-2`

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
| `cbc:ID` | Invoice number | Must uniquely identify invoice per directive 2006/112/EC |
| `cbc:IssueDate` | Issue date | Format: YYYY-MM-DD |
| `cbc:InvoiceTypeCode` | Functional type | Example: 380 (commercial invoice) |
| `cbc:DocumentCurrencyCode` | Invoice currency | Example: EUR, USD (ISO 4217) |

### Parties

| Element | Purpose | Notes |
|---------|---------|-------|
| `cac:AccountingSupplierParty` | Seller information | Required group containing seller details |
| `cac:AccountingCustomerParty` | Buyer information | Required group containing buyer details |

### Financial Totals

| Element | Purpose | Notes |
|---------|---------|-------|
| `cac:TaxTotal` | Tax totals | 1-2 instances; two required if tax currency differs from document currency |
| `cac:LegalMonetaryTotal` | Document totals | Monetary summary (line extension, tax exclusive, payable amounts) |

### Line Items

| Element | Purpose | Notes |
|---------|---------|-------|
| `cac:InvoiceLine` | Line items | Minimum one line required (1..n) |

---

## Optional Elements

### Document-Level Optional Elements (0..1)

| Element | Purpose | Example/Notes |
|---------|---------|---------------|
| `cbc:DueDate` | Payment due date | Format: YYYY-MM-DD |
| `cbc:InvoicePeriod` | Billing period | Start and end dates |
| `cbc:Note` | Document-level note | Free text (max 1 note unless German B2B) |
| `cbc:TaxPointDate` | Tax point date | VAT accounting date |
| `cbc:TaxCurrencyCode` | Tax currency code | When different from document currency |
| `cbc:AccountingCost` | Accounting cost code | Buyer's accounting reference |
| `cbc:BuyerReference` | Buyer reference | Purchase order or contract reference |
| `cac:OrderReference` | Purchase order reference | Reference to order document |
| `cac:BillingReference` | Referenced invoice | For corrections or credit notes |
| `cac:ContractDocumentReference` | Contract reference | Reference to contract |
| `cac:DespatchDocumentReference` | Despatch advice reference | Delivery documentation |
| `cac:ReceiptDocumentReference` | Receipt advice reference | Receipt confirmation |
| `cac:OriginatorDocumentReference` | Originating document | Source document reference |
| `cac:PayeeParty` | Payee party | When different from seller (factoring) |
| `cac:TaxRepresentativeParty` | Tax representative | VAT representative details |
| `cac:Delivery` | Delivery information | Delivery details and location |
| `cac:PaymentTerms` | Payment terms | Payment conditions and discounts |
| `cac:ProjectReference` | Project reference | Project identification (max 1) |

### Repeatable Optional Elements (0..n)

| Element | Purpose | Example/Notes |
|---------|---------|---------------|
| `cac:AdditionalDocumentReference` | Supporting documents | Attachments, references, etc. |
| `cac:PaymentMeans` | Payment instructions | Bank account, payment card, etc. |
| `cac:AllowanceCharge` | Document-level adjustments | Discounts or charges |

---

## Party Structure (AccountingSupplierParty/AccountingCustomerParty)

Both supplier and customer party structures follow similar patterns:

### Mandatory Party Elements

```xml
<cac:Party>
    <cac:PartyName>
        <cbc:Name>Party legal name</cbc:Name> <!-- 1..1 -->
    </cac:PartyName>
    <cac:PostalAddress>
        <cac:Country>
            <cbc:IdentificationCode>Country code</cbc:IdentificationCode> <!-- 1..1 ISO 3166-1 -->
        </cac:Country>
    </cac:PostalAddress>
    <cac:PartyLegalEntity>
        <cbc:RegistrationName>Legal registration name</cbc:RegistrationName> <!-- 1..1 -->
    </cac:PartyLegalEntity>
</cac:Party>
```

### Optional Party Elements

- `cbc:EndpointID` - Electronic address (0..1, but MUST be provided per PEPPOL-EN16931-R010/R020)
- `cac:PartyIdentification/cbc:ID` - Party identifier (0..n)
- `cac:PostalAddress` - Full address details (street, city, postal code)
- `cac:PartyTaxScheme` - VAT identification (0..n)
- `cac:Contact` - Contact information (0..1)

---

## Tax Total Structure

```xml
<cac:TaxTotal>
    <cbc:TaxAmount currencyID="EUR">25.00</cbc:TaxAmount> <!-- 1..1 -->
    <cac:TaxSubtotal> <!-- 1..n -->
        <cbc:TaxableAmount currencyID="EUR">100.00</cbc:TaxableAmount> <!-- 1..1 -->
        <cbc:TaxAmount currencyID="EUR">25.00</cbc:TaxAmount> <!-- 1..1 -->
        <cac:TaxCategory>
            <cbc:ID>S</cbc:ID> <!-- 1..1 (S=Standard, Z=Zero, E=Exempt, etc.) -->
            <cbc:Percent>25.00</cbc:Percent> <!-- 0..1, required for most categories -->
            <cac:TaxScheme>
                <cbc:ID>VAT</cbc:ID> <!-- 1..1 -->
            </cac:TaxScheme>
        </cac:TaxCategory>
    </cac:TaxSubtotal>
</cac:TaxTotal>
```

---

## Legal Monetary Total Structure

```xml
<cac:LegalMonetaryTotal>
    <cbc:LineExtensionAmount currencyID="EUR">100.00</cbc:LineExtensionAmount> <!-- 1..1 -->
    <cbc:TaxExclusiveAmount currencyID="EUR">100.00</cbc:TaxExclusiveAmount> <!-- 1..1 -->
    <cbc:TaxInclusiveAmount currencyID="EUR">125.00</cbc:TaxInclusiveAmount> <!-- 1..1 -->
    <cbc:AllowanceTotalAmount currencyID="EUR">0.00</cbc:AllowanceTotalAmount> <!-- 0..1 -->
    <cbc:ChargeTotalAmount currencyID="EUR">0.00</cbc:ChargeTotalAmount> <!-- 0..1 -->
    <cbc:PrepaidAmount currencyID="EUR">0.00</cbc:PrepaidAmount> <!-- 0..1 -->
    <cbc:PayableRoundingAmount currencyID="EUR">0.00</cbc:PayableRoundingAmount> <!-- 0..1 -->
    <cbc:PayableAmount currencyID="EUR">125.00</cbc:PayableAmount> <!-- 1..1 -->
</cac:LegalMonetaryTotal>
```

---

## Invoice Line Structure

```xml
<cac:InvoiceLine>
    <cbc:ID>1</cbc:ID> <!-- 1..1 Line identifier -->
    <cbc:Note>Line note</cbc:Note> <!-- 0..1 -->
    <cbc:InvoicedQuantity unitCode="C62">10</cbc:InvoicedQuantity> <!-- 1..1 -->
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
</cac:InvoiceLine>
```

---

## Common Invoice Type Codes (UNCL 1001 subset)

| Code | Description |
|------|-------------|
| 380 | Commercial invoice |
| 381 | Credit note |
| 384 | Corrected invoice |
| 389 | Self-billed invoice |
| 326 | Partial invoice |
| 751 | Invoice information for accounting purposes |

---

## Common Unit Codes (Subset of UN/ECE Recommendation 20)

| Code | Description |
|------|-------------|
| C62 | One (piece) |
| DAY | Day |
| HUR | Hour |
| KGM | Kilogram |
| LTR | Litre |
| MTQ | Cubic meter |
| MTR | Meter |
| TNE | Tonne (metric ton) |
| XPP | Portion/Piece |

For a complete list, refer to UN/ECE Recommendation 20.
