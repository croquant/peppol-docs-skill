# Peppol BIS Billing 3.0 Code Lists

This document contains standardized code lists used in Peppol billing documents. These code lists ensure interoperability and compliance with international standards.

---

## Currency Codes (ISO 4217)

**Standard:** ISO 4217:2005
**Element:** `cbc:DocumentCurrencyCode`, `cbc:TaxCurrencyCode`
**Usage:** All monetary amounts must use valid ISO 4217 currency codes

### Common Currency Codes

| Code | Currency |
|------|----------|
| EUR | Euro |
| USD | United States Dollar |
| GBP | Pound Sterling |
| SEK | Swedish Krona |
| NOK | Norwegian Krone |
| DKK | Danish Krone |
| CHF | Swiss Franc |
| JPY | Yen |
| AUD | Australian Dollar |
| CAD | Canadian Dollar |
| PLN | Zloty |
| CZK | Czech Koruna |
| HUF | Forint |
| RON | Romanian Leu |

For a complete list, refer to ISO 4217.

---

## Country Codes (ISO 3166-1 Alpha-2)

**Standard:** ISO 3166-1:Alpha2
**Element:** `cac:Country/cbc:IdentificationCode`
**Usage:** Country identification in addresses and party information

### EU/EEA Country Codes

| Code | Country |
|------|---------|
| AT | Austria |
| BE | Belgium |
| BG | Bulgaria |
| HR | Croatia |
| CY | Cyprus |
| CZ | Czech Republic |
| DK | Denmark |
| EE | Estonia |
| FI | Finland |
| FR | France |
| DE | Germany |
| GR | Greece |
| HU | Hungary |
| IE | Ireland |
| IT | Italy |
| LV | Latvia |
| LT | Lithuania |
| LU | Luxembourg |
| MT | Malta |
| NL | Netherlands |
| PL | Poland |
| PT | Portugal |
| RO | Romania |
| SK | Slovakia |
| SI | Slovenia |
| ES | Spain |
| SE | Sweden |
| IS | Iceland |
| LI | Liechtenstein |
| NO | Norway |

### Other Common Country Codes

| Code | Country |
|------|---------|
| GB | United Kingdom |
| US | United States |
| CH | Switzerland |
| CA | Canada |
| AU | Australia |
| JP | Japan |
| CN | China |
| IN | India |
| BR | Brazil |

For a complete list, refer to ISO 3166-1.

---

## Electronic Address Scheme (EAS)

**Standard:** CEF EAS (Connecting Europe Facility - Electronic Address Scheme)
**Element:** `cbc:EndpointID/@schemeID`
**Usage:** Identifies the scheme used for electronic addresses

### Common EAS Codes

| Code | Scheme | Description |
|------|--------|-------------|
| 0002 | FR:SIRENE | System Information et Repertoire des Entreprise et des Etablissements (France) |
| 0007 | SE:ORGNR | Swedish Organization Number |
| 0088 | GLN | Global Location Number (GS1) |
| 0096 | DK:P | Danish Chamber of Commerce Scheme (EDIRA compliant) |
| 0106 | NL:OIN | Dutch Originator's Identification Number |
| 0130 | IT:SIA | SIA Object Identifiers |
| 0135 | IT:SECETI | SECETI Object Identifiers |
| 0142 | IT:CODDEST | Codice Destinatario (IT) |
| 0184 | DK:DIGST | DIGSTORG |
| 0188 | JP:SST | Corporate Number of The Social Security and Tax Number System (Japan) |
| 0190 | NL:OINO | Dutch Originator's Identification Number for Organizations |
| 0192 | NO:ORGNR | Norwegian Organization Number (Brønnøysundregistrene) |
| 0195 | SG:UEN | Singapore Nationwide E-Invoice Framework |
| 0198 | PEPPOL | Peppol participant identifier |
| 0201 | IS:KTNR | Icelandic freight forwarder identifier |
| 0204 | NO:VAT | Norwegian VAT number |
| 0208 | BE:EN | Belgian eNotary identifier |
| 9901 | DK:CPR | Danish Ministry of the Interior and Health |
| 9902 | DK:CVR | Danish Commerce and Companies Agency |
| 9906 | IT:IPA | Indice delle Pubbliche Amministrazioni (IPA) |
| 9907 | IT:CF | Tax Code (Codice Fiscale) |
| 9910 | IT:VAT | Italian VAT number |
| 9913 | FR:VAT | French VAT number |
| 9914 | BE:VAT | Belgian VAT number |
| 9915 | NL:VAT | Dutch VAT number |
| 9918 | DE:VAT | German VAT number |
| 9919 | NO:VAT | Norwegian VAT number |
| 9920 | SE:VAT | Swedish VAT number |
| 9922 | DK:VAT | Danish VAT number |
| 9925 | GB:VAT | United Kingdom VAT number |
| 9933 | ES:VAT | Spanish VAT number |
| 9956 | BE:CBE | Belgian Crossroad Bank of Enterprises |
| 9957 | FR:VAT | French VAT number |

**Example:**
```xml
<cbc:EndpointID schemeID="0192">987654321</cbc:EndpointID> <!-- Norwegian Organization Number -->
```

---

## VAT Category Codes (UNCL 5305 Subset)

**Standard:** UN/CEFACT Code List 5305 (Duty or tax or fee category code)
**Element:** `cac:TaxCategory/cbc:ID`
**Usage:** VAT category classification

| Code | Description | Rate Required |
|------|-------------|---------------|
| S | Standard rate | Yes |
| Z | Zero rated goods | Yes (0%) |
| E | Exempt from tax | No |
| AE | VAT Reverse Charge | No |
| K | VAT exempt for EEA intra-community supply of goods and services | No |
| G | Free export item, tax not charged | No |
| O | Services outside scope of tax | No |
| L | Canary Islands general indirect tax | Yes |
| M | Tax for production, services and importation in Ceuta and Melilla | Yes |
| B | Transferred (VAT) | Yes |

**Example:**
```xml
<cac:ClassifiedTaxCategory>
    <cbc:ID>S</cbc:ID>
    <cbc:Percent>25.00</cbc:Percent>
    <cac:TaxScheme>
        <cbc:ID>VAT</cbc:ID>
    </cac:TaxScheme>
</cac:ClassifiedTaxCategory>
```

---

## Invoice Type Codes (UNCL 1001 Subset)

**Standard:** UN/CEFACT Code List 1001
**Element:** `cbc:InvoiceTypeCode`
**Usage:** Classification of invoice functional type

### Allowed Invoice Type Codes

| Code | Description |
|------|-------------|
| 80 | Debit note related to goods or services |
| 82 | Metered services invoice |
| 84 | Debit note related to financial adjustments |
| 130 | Invoicing data sheet |
| 202 | Direct payment valuation |
| 204 | Provisional payment valuation |
| 211 | Interim application for payment |
| 295 | Quantity valuation |
| 325 | Proforma invoice |
| 326 | Partial invoice (German organizations only) |
| 380 | Commercial invoice |
| 383 | Debit note |
| 384 | Corrected invoice (German organizations only) |
| 386 | Prepayment invoice |
| 388 | Tax invoice |
| 389 | Self-billed invoice |
| 390 | Delcredere invoice |
| 393 | Factored invoice |
| 394 | Lease invoice |
| 395 | Consignment invoice |
| 575 | Insurer's invoice |
| 623 | Forwarder's invoice |
| 780 | Freight invoice |
| 935 | Customs invoice |

**Note:** Type codes 326 and 384 are only allowed when both buyer and seller are German organizations (PEPPOL-EN16931-P0112).

---

## Credit Note Type Codes (UNCL 1001 Subset)

**Standard:** UN/CEFACT Code List 1001
**Element:** `cbc:CreditNoteTypeCode`
**Usage:** Classification of credit note functional type

| Code | Description |
|------|-------------|
| 81 | Credit note related to goods or services |
| 83 | Credit note related to financial adjustments |
| 261 | Self billed credit note |
| 262 | Consolidated credit note - goods and services |
| 296 | Quantity valuation request |
| 308 | Delcredere credit note |
| 381 | Credit note |
| 396 | Factored credit note |
| 420 | Optical Character Reading (OCR) payment credit note |
| 458 | Debit note related to services |
| 532 | Forwarder's credit note |

---

## Payment Means Codes (UNCL 4461)

**Standard:** UN/CEFACT Code List 4461
**Element:** `cbc:PaymentMeansCode`
**Usage:** Specifies the payment method

| Code | Description |
|------|-------------|
| 1 | Instrument not defined |
| 2 | Automated clearing house credit |
| 3 | Automated clearing house debit |
| 4 | ACH demand debit reversal |
| 5 | ACH demand credit reversal |
| 6 | ACH demand credit |
| 7 | ACH demand debit |
| 10 | In cash |
| 20 | Cheque |
| 21 | Banker's draft |
| 23 | Certified banker's draft |
| 30 | Credit transfer |
| 31 | Debit transfer |
| 42 | Payment to bank account |
| 48 | Bank card |
| 49 | Direct debit |
| 50 | Payment by postgiro |
| 54 | Urgent commercial payment |
| 55 | Urgent Treasury Payment |
| 57 | Standing agreement |
| 58 | SEPA credit transfer |
| 59 | SEPA direct debit |
| 60 | Promissory note |
| 68 | Online payment service |
| 97 | Clearing between partners |

**Note:** When using payment means code 49 (Direct debit), mandate reference MUST be provided (PEPPOL-EN16931-R061).

---

## Allowance Reason Codes (UNCL 5189 Subset)

**Standard:** UN/CEFACT Code List 5189 D.16B
**Element:** `cac:AllowanceCharge/cbc:AllowanceChargeReasonCode` (when ChargeIndicator=false)
**Usage:** Reason for document or line level allowances (discounts)

| Code | Description |
|------|-------------|
| 41 | Bonus for works ahead of schedule |
| 42 | Other bonus |
| 60 | Manufacturer's consumer discount |
| 62 | Due to military status |
| 63 | Due to work accident |
| 64 | Special agreement |
| 65 | Production error discount |
| 66 | New outlet discount |
| 67 | Sample discount |
| 68 | End-of-range discount |
| 70 | Incoterm discount |
| 71 | Point of sales threshold allowance |
| 88 | Material surcharge/deduction |
| 95 | Discount |
| 100 | Special rebate |
| 102 | Fixed long term |
| 103 | Temporary |
| 104 | Standard |
| 105 | Yearly turnover |

---

## Charge Reason Codes (UNCL 7161)

**Standard:** UN/CEFACT Code List 7161 D.16B
**Element:** `cac:AllowanceCharge/cbc:AllowanceChargeReasonCode` (when ChargeIndicator=true)
**Usage:** Reason for document or line level charges

| Code | Description |
|------|-------------|
| AA | Advertising |
| AAA | Telecommunication |
| AAC | Technical modification |
| AAD | Job-order production |
| AAE | Outlying area |
| AAF | Sourcing |
| AAH | Rework |
| AAI | Slotting |
| AAS | Acceptance |
| AAT | Rush delivery |
| AAV | Special construction |
| AAY | Airport facilities |
| AAZ | Concession |
| ABA | Compulsory storage |
| ABB | Fuel removal |
| ABC | Into plane |
| ABD | Overtime |
| ABF | Tooling |
| ABK | Miscellaneous |
| ABL | Additional packaging |
| ABN | Dunnage |
| ABR | Containerisation |
| ABS | Carton packing |
| ABT | Hessian wrapped |
| ABU | Polyethylene wrap packing |
| ACF | Miscellaneous treatment |
| ACG | Enamelling treatment |
| ACH | Heat treatment |
| ACI | Plating treatment |
| ACJ | Painting |
| ACK | Polishing |
| ACL | Priming |
| ACM | Preservation treatment |
| ACS | Fitting |
| ADC | Defective packing |
| ADE | Distressed cargo |
| ADJ | Charge for claim |
| ADK | Charge for damage |
| ADL | Charge for loss |
| ADM | Charge for detention |
| ADN | Delivery charge |
| ADO | Documentation charge |
| ADP | Drayage charge |
| ADQ | Equipment charge |
| ADR | Exchange rate guarantee |
| ADT | Expedition fee |
| ADW | Ferry charge |
| ADY | Freight charge |
| ADZ | Fuel charge |
| AEA | Haulage charge |
| AEB | Hoisting charge |
| AEC | Loading charge |
| AED | Lashing charge |
| AEF | Palletizing charge |
| AEH | Pickup charge |
| AEI | Repacking charge |
| AEJ | Handling charge |
| AEK | Repair charge |
| AEL | Inland transport charge |
| AEM | Shipping and handling |
| AEN | Shelter charge |
| AEO | Special handling |
| AEP | Special tooling charge |
| AES | Storage charge |
| AET | Testing |
| AEU | Transportation - third party |
| AEV | Transportation by vendor |
| AEW | Drop yard |
| AEX | Warehousing charge |
| AEY | Combine all same day shipment |
| AEZ | Split pick-up |
| FC | Freight service |
| FH | Filling/handling |
| FI | Financing |
| GAA | Cleaning charge |
| HAA | Breakage |
| HD | Handling charge |
| HH | Hoisting and hauling |
| IAA | Installation |
| IAB | Installation and warranty |
| ID | Industrial promotion |
| IF | Inspection |
| IR | Installation and training |
| IS | Invoicing |
| KO | Contact information |
| L1 | Advance payment |
| LA | Labelling |
| LAA | Labour |
| LAB | Repair and return |
| LF | Legalisation fee |
| MAE | Mounting |
| MI | Mail invoice |
| ML | Mail invoice to each location |
| NAA | Non-returnable containers |
| OA | Outside labour |
| PA | Invoice with shipment |
| PAA | Phosphatizing (steel treatment) |
| PC | Packing |
| PL | Palletizing |
| RAB | Re-delivery |
| RAC | Restocking charge |
| RAD | Re-labelling |
| RAF | Re-furbishing |
| RE | Re-exchange |
| RF | Refurbishing |
| RH | Repositioning charge |
| RV | Reservation charge |
| SA | Salvaging |
| SAA | Shipping and handling |
| SAD | Special packaging |
| SAE | Stamping |
| SAI | Consignee unload |
| SG | Shrink-wrap |
| SH | Special handling |
| SM | Special finish |
| SU | Set-up |
| TAB | Tank renting |
| TAC | Testing |
| TT | Transportation - third party |
| TV | Transportation by vendor |
| V1 | Drop yard |
| V2 | Drop dock |
| WH | Warehousing |
| XAA | Combine all same day shipment |
| YY | Split pick-up |
| ZZZ | Mutually defined |

---

## VAT Exemption Reason Codes (VATEX)

**Usage:** Provides standardized reasons for VAT exemptions
**Element:** `cac:TaxCategory/cbc:TaxExemptionReasonCode`

### EU-Specific VATEX Codes

| Code | Description | Tax Category |
|------|-------------|--------------|
| VATEX-EU-79-C | Exempt based on article 79, point c of Council Directive 2006/112/EC | E |
| VATEX-EU-132 | Exempt based on article 132 of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1A | Exempt based on article 132, section 1 (a) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1B | Exempt based on article 132, section 1 (b) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1C | Exempt based on article 132, section 1 (c) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1D | Exempt based on article 132, section 1 (d) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1E | Exempt based on article 132, section 1 (e) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1F | Exempt based on article 132, section 1 (f) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1G | Exempt based on article 132, section 1 (g) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1H | Exempt based on article 132, section 1 (h) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1I | Exempt based on article 132, section 1 (i) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1J | Exempt based on article 132, section 1 (j) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1K | Exempt based on article 132, section 1 (k) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1L | Exempt based on article 132, section 1 (l) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1M | Exempt based on article 132, section 1 (m) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1N | Exempt based on article 132, section 1 (n) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1O | Exempt based on article 132, section 1 (o) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1P | Exempt based on article 132, section 1 (p) of Council Directive 2006/112/EC | E |
| VATEX-EU-132-1Q | Exempt based on article 132, section 1 (q) of Council Directive 2006/112/EC | E |
| VATEX-EU-143 | Exempt based on article 143 of Council Directive 2006/112/EC | E |
| VATEX-EU-143-1A | Exempt based on article 143, section 1 (a) of Council Directive 2006/112/EC | E |
| VATEX-EU-143-1B | Exempt based on article 143, section 1 (b) of Council Directive 2006/112/EC | E |
| VATEX-EU-143-1C | Exempt based on article 143, section 1 (c) of Council Directive 2006/112/EC | E |
| VATEX-EU-143-1D | Exempt based on article 143, section 1 (d) of Council Directive 2006/112/EC | E |
| VATEX-EU-143-1E | Exempt based on article 143, section 1 (e) of Council Directive 2006/112/EC | E |
| VATEX-EU-143-1F | Exempt based on article 143, section 1 (f) of Council Directive 2006/112/EC | E |
| VATEX-EU-143-1FA | Exempt based on article 143, section 1 (fa) of Council Directive 2006/112/EC | E |
| VATEX-EU-143-1G | Exempt based on article 143, section 1 (g) of Council Directive 2006/112/EC | E |
| VATEX-EU-143-1H | Exempt based on article 143, section 1 (h) of Council Directive 2006/112/EC | E |
| VATEX-EU-143-1I | Exempt based on article 143, section 1 (i) of Council Directive 2006/112/EC | E |
| VATEX-EU-143-1J | Exempt based on article 143, section 1 (j) of Council Directive 2006/112/EC | E |
| VATEX-EU-143-1K | Exempt based on article 143, section 1 (k) of Council Directive 2006/112/EC | E |
| VATEX-EU-143-1L | Exempt based on article 143, section 1 (l) of Council Directive 2006/112/EC | E |
| VATEX-EU-148 | Exempt based on article 148 of Council Directive 2006/112/EC | G |
| VATEX-EU-148-A | Exempt based on article 148, section (a) of Council Directive 2006/112/EC | G |
| VATEX-EU-148-B | Exempt based on article 148, section (b) of Council Directive 2006/112/EC | G |
| VATEX-EU-148-C | Exempt based on article 148, section (c) of Council Directive 2006/112/EC | G |
| VATEX-EU-148-D | Exempt based on article 148, section (d) of Council Directive 2006/112/EC | G |
| VATEX-EU-148-E | Exempt based on article 148, section (e) of Council Directive 2006/112/EC | G |
| VATEX-EU-148-F | Exempt based on article 148, section (f) of Council Directive 2006/112/EC | G |
| VATEX-EU-148-G | Exempt based on article 148, section (g) of Council Directive 2006/112/EC | G |
| VATEX-EU-309 | Exempt based on article 309 of Council Directive 2006/112/EC | K |
| VATEX-EU-AE | Reverse charge | AE |
| VATEX-EU-D | Margin scheme - Travel agents | E |
| VATEX-EU-F | Margin scheme - Second-hand goods | E |
| VATEX-EU-G | Export outside the EU | G |
| VATEX-EU-I | Margin scheme - Works of art | E |
| VATEX-EU-IC | Intra-Community supply | K |
| VATEX-EU-J | Margin scheme - Collector's items and antiques | E |
| VATEX-EU-O | Not subject to VAT | O |

---

## Unit of Measure Codes (UN/ECE Recommendation 20)

**Standard:** UN/ECE Recommendation 20 with Recommendation 21
**Element:** `cbc:InvoicedQuantity/@unitCode`, `cbc:BaseQuantity/@unitCode`
**Usage:** Unit of measure for quantities

### Common Unit Codes

| Code | Description |
|------|-------------|
| C62 | One (piece) |
| DAY | Day |
| HUR | Hour |
| KGM | Kilogram |
| KTM | Kilometre |
| KWH | Kilowatt hour |
| LS | Lump sum |
| LTR | Litre |
| MIN | Minute |
| MMK | Square millimetre |
| MMT | Millimetre |
| MTK | Square metre |
| MTQ | Cubic metre |
| MTR | Metre |
| NAR | Number of articles |
| NPR | Number of pairs |
| P1 | Percent |
| SET | Set |
| TNE | Tonne (metric ton) |
| WEE | Week |
| XPP | Portion/Piece |

For a complete list (over 600 codes), refer to UN/ECE Recommendation 20.

---

## MIME Type Codes (IANA Subset)

**Standard:** IANA MIME types
**Element:** `cbc:EmbeddedDocumentBinaryObject/@mimeCode`
**Usage:** Document attachment MIME types

### Allowed MIME Types

| Code | Description |
|------|-------------|
| application/pdf | PDF document |
| application/vnd.openxmlformats-officedocument.spreadsheetml.sheet | Excel (XLSX) |
| application/vnd.openxmlformats-officedocument.wordprocessingml.document | Word (DOCX) |
| application/vnd.openxmlformats-officedocument.presentationml.presentation | PowerPoint (PPTX) |
| image/png | PNG image |
| image/jpeg | JPEG image |
| text/csv | CSV file |
| application/xml | XML document |
| text/plain | Plain text |

---

## Item Classification Codes (UNCL 7143)

**Standard:** UN/CEFACT Code List 7143
**Element:** `cac:CommodityClassification/cbc:ItemClassificationCode/@listID`
**Usage:** Scheme identifier for item classification

### Common Classification Schemes

| Code | Description |
|------|-------------|
| STI | Standard Type Identification |
| CPV | Common Procurement Vocabulary |
| GPC | GS1 Global Product Classification |
| UNSPSC | United Nations Standard Products and Services Code |
| eCl@ss | eCl@ss classification |
| TST | Type of service (ZALEX) |

---

## Summary

All code lists are maintained to ensure:
- **Interoperability**: Cross-border document exchange
- **Standardization**: Common understanding across systems
- **Compliance**: Meeting legal and regulatory requirements
- **Automation**: Enable automatic processing and validation

For the most current versions of these code lists, refer to the official Peppol documentation at https://docs.peppol.eu/poacc/billing/3.0/codelist/
