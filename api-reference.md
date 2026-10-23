# API Reference

Mirrored from [smoovops.com/doc/api-reference](https://smoovops.com/doc/api-reference) — see
this repository's [README](README.md) for the Postman collection that goes with it.

This page lists every endpoint available to a [Personal API Token](https://smoovops.com/doc/api-access) —
auto-generated from the backend's route definitions, so it always matches what's actually
deployed. Every request must carry both required headers:

```
Authorization: Bearer smv_live_...
x-api-key: <your API key>
```

See [API Access](https://smoovops.com/doc/api-access) for how to generate a token, and for rate limits and
quotas.

**Response bodies are not yet documented here** — every endpoint below shows the request
shape (query parameters and body, if any); the shape of a successful response isn't part of this generated reference
yet. A [standalone PDF](https://smoovops.com/smoovops-api-reference-en.pdf) of this page is also available.


## API Tokens

### GET `/v1/api-tokens`

_No request body._

### POST `/v1/api-tokens`

| Field | Type | Required |
| --- | --- | --- |
| `name` | string | Yes |
| `expiresAt` | string | No |

### DELETE `/v1/api-tokens/{tokenId}`

_No request body._

## Account

### GET `/v1/account/addresses`

_No request body._

### PUT `/v1/account/addresses`

| Field | Type | Required |
| --- | --- | --- |
| `version` | integer | Yes |
| `addresses` | array of object (AddressSchema) | Yes |

### PATCH `/v1/account/addresses`

| Field | Type | Required |
| --- | --- | --- |
| `version` | integer | Yes |
| `budgetsSuppressed` | boolean | No |
| `reminderEmail` | string | No |
| `allowContractReminderOverride` | boolean | No |
| `allowInvoiceLineItemOverride` | boolean | No |
| `dashboardWidgets` | array of object (DashboardWidgetSettingsSchema) | No |
| `companyProfile` | object (CompanyProfileSchema) | No |
| `dateFormat` | DD.MM.YYYY | DD/MM/YYYY | YYYY-MM-DD | No |
| `numberFormat` | 1.234,56 | 1,234.56 | No |
| `currency` | EUR | GBP | CHF | SEK | DKK | NOK | PLN | CZK | HUF | RON | BGN | ISK | No |
| `incomingPaymentTerm` | SOLL | HABEN | No |

## Audit Trail

### GET `/v1/audit-events`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `cursor` | string | No | — |
| `limit` | integer | No | `20` |
| `userId` | string | No | — |

_No request body._

## Authentication

### POST `/v1/auth/confirm`

_No request body._

### POST `/v1/auth/forgot-password`

_No request body._

### POST `/v1/auth/login`

_No request body._

### POST `/v1/auth/logout`

_No request body._

### POST `/v1/auth/refresh`

_No request body._

### POST `/v1/auth/register`

_No request body._

### POST `/v1/auth/reset-password`

_No request body._

## Bank Statement Imports

### POST `/v1/bank-statement-imports`

| Field | Type | Required |
| --- | --- | --- |
| `fileId` | string | Yes |
| `key` | string | Yes |
| `fileName` | string | No |
| `periodFrom` | string | Yes |
| `periodTo` | string | Yes |
| `autoApprove` | boolean | No |

### GET `/v1/bank-statement-imports/active`

_No request body._

### GET `/v1/bank-statement-imports/{importId}`

_No request body._

### DELETE `/v1/bank-statement-imports/{importId}`

_No request body._

### POST `/v1/bank-statement-imports/{importId}/finalize`

| Field | Type | Required |
| --- | --- | --- |
| `version` | integer | Yes |

### PATCH `/v1/bank-statement-imports/{importId}/transactions/{index}`

| Field | Type | Required |
| --- | --- | --- |
| `version` | integer | Yes |
| `decision` | ACCEPTED | REJECTED | Yes |

## Budget Categories

### GET `/v1/budget-categories`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `limit` | integer | No | `20` |
| `page` | integer | No | `1` |

_No request body._

### POST `/v1/budget-categories`

| Field | Type | Required |
| --- | --- | --- |
| `name` | string | Yes |
| `monthlyLimit` | number | Yes |
| `currency` | string | Yes |
| `keywords` | array of string | Yes |
| `active` | boolean | Yes |

### PATCH `/v1/budget-categories/{categoryId}`

| Field | Type | Required |
| --- | --- | --- |
| `version` | integer | Yes |
| `name` | string | No |
| `monthlyLimit` | number | No |
| `currency` | string | No |
| `keywords` | array of string | No |
| `active` | boolean | No |

### DELETE `/v1/budget-categories/{categoryId}`

_No request body._

## Budget Entries

### GET `/v1/budget-entries`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `categoryId` | string | No | — |
| `limit` | integer | No | `20` |
| `page` | integer | No | `1` |

_No request body._

### POST `/v1/budget-entries`

| Field | Type | Required |
| --- | --- | --- |
| `categoryId` | string | Yes |
| `categoryName` | string | No |
| `amount` | number | Yes |
| `currency` | string | Yes |
| `entryDate` | string | Yes |
| `documentId` | string | No |
| `vendorName` | string | No |

### DELETE `/v1/budget-entries/{entryId}`

_No request body._

## Contracts

### GET `/v1/contracts`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `partnerId` | string | No | — |
| `sort` | string | No | — |
| `limit` | integer | No | `20` |
| `page` | integer | No | `1` |

_No request body._

### POST `/v1/contracts`

| Field | Type | Required |
| --- | --- | --- |
| `name` | string | Yes |
| `partnerId` | string | Yes |
| `partnerName` | string | Yes |
| `partnerType` | CUSTOMER | VENDOR | No |
| `startDate` | string | Yes |
| `totalValue` | number | Yes |
| `currency` | string | Yes |
| `status` | DRAFT | ACTIVE | EXPIRED | CANCELLED | No |
| `endDate` | string | No |
| `description` | string | No |
| `tags` | array of string | No |
| `advanced` | object (ContractAdvanced) | No |

### GET `/v1/contracts/{contractId}`

_No request body._

### PUT `/v1/contracts/{contractId}`

| Field | Type | Required |
| --- | --- | --- |
| `version` | integer | Yes |
| `name` | string | No |
| `partnerId` | string | No |
| `partnerName` | string | No |
| `partnerType` | CUSTOMER | VENDOR | No |
| `status` | DRAFT | ACTIVE | EXPIRED | CANCELLED | No |
| `startDate` | string | No |
| `endDate` | string | No |
| `totalValue` | number | No |
| `currency` | string | No |
| `description` | string | No |
| `tags` | array of string | No |
| `advanced` | object (ContractAdvanced) | No |

### DELETE `/v1/contracts/{contractId}`

_No request body._

## Dashboard

### GET `/v1/dashboard/cash-anchor`

_No request body._

### PUT `/v1/dashboard/cash-anchor`

| Field | Type | Required |
| --- | --- | --- |
| `openingBalance` | number | Yes |
| `effectiveDate` | string | Yes |

### GET `/v1/dashboard/stats`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `from` | string | No | — |
| `to` | string | No | — |

_No request body._

### GET `/v1/dashboard/timeseries`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `metric` | string | No | — |
| `granularity` | string | No | — |
| `view` | string | No | — |
| `to` | string | No | — |
| `from` | string | No | — |

_No request body._

## Document Rasterization

### POST `/v1/documents/rasterize`

_No request body._

## Document Templates

### GET `/v1/document-templates`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `status` | string | No | — |
| `limit` | integer | No | `20` |
| `page` | integer | No | `1` |

_No request body._

### POST `/v1/document-templates`

| Field | Type | Required |
| --- | --- | --- |
| `name` | string | Yes |
| `documentType` | LETTER | OFFER | INVOICE | OTHER | Yes |
| `contentSource` | string | Yes |
| `fields` | array of object (TemplateField) | No |
| `headerSource` | string | No |
| `headerVisibility` | ALL_PAGES | FIRST_PAGE_ONLY | LAST_PAGE_ONLY | No |
| `footerSource` | string | No |
| `footerVisibility` | ALL_PAGES | FIRST_PAGE_ONLY | LAST_PAGE_ONLY | No |
| `showLogo` | boolean | No |
| `logoPosition` | TOP_LEFT | TOP_RIGHT | No |
| `status` | DRAFT | PUBLISHED | No |
| `systemKey` | TERMINATION | NOTICE | OFFER | INVOICE | No |
| `compiledHeaderHtml` | string | No |
| `compiledContentHtml` | string | No |
| `compiledFooterHtml` | string | No |

### POST `/v1/document-templates/compile`

| Field | Type | Required |
| --- | --- | --- |
| `name` | string | Yes |
| `documentType` | LETTER | OFFER | INVOICE | OTHER | Yes |
| `contentSource` | string | Yes |
| `fields` | array of object (TemplateField) | No |
| `headerSource` | string | No |
| `headerVisibility` | ALL_PAGES | FIRST_PAGE_ONLY | LAST_PAGE_ONLY | No |
| `footerSource` | string | No |
| `footerVisibility` | ALL_PAGES | FIRST_PAGE_ONLY | LAST_PAGE_ONLY | No |
| `showLogo` | boolean | No |
| `logoPosition` | TOP_LEFT | TOP_RIGHT | No |
| `status` | DRAFT | PUBLISHED | No |
| `systemKey` | TERMINATION | NOTICE | OFFER | INVOICE | No |
| `compiledHeaderHtml` | string | No |
| `compiledContentHtml` | string | No |
| `compiledFooterHtml` | string | No |

### GET `/v1/document-templates/{templateId}`

_No request body._

### PUT `/v1/document-templates/{templateId}`

| Field | Type | Required |
| --- | --- | --- |
| `version` | integer | Yes |
| `name` | string | No |
| `documentType` | LETTER | OFFER | INVOICE | OTHER | No |
| `contentSource` | string | No |
| `fields` | array of object (TemplateField) | No |
| `status` | DRAFT | PUBLISHED | No |
| `headerSource` | string | No |
| `headerVisibility` | ALL_PAGES | FIRST_PAGE_ONLY | LAST_PAGE_ONLY | No |
| `footerSource` | string | No |
| `footerVisibility` | ALL_PAGES | FIRST_PAGE_ONLY | LAST_PAGE_ONLY | No |
| `showLogo` | boolean | No |
| `logoPosition` | TOP_LEFT | TOP_RIGHT | No |
| `systemKey` | TERMINATION | NOTICE | OFFER | INVOICE | No |
| `compiledHeaderHtml` | string | No |
| `compiledContentHtml` | string | No |
| `compiledFooterHtml` | string | No |

### DELETE `/v1/document-templates/{templateId}`

_No request body._

## Documents

### GET `/v1/documents`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `contractId` | string | No | — |
| `limit` | integer | No | `20` |
| `page` | integer | No | `1` |

_No request body._

### POST `/v1/documents`

| Field | Type | Required |
| --- | --- | --- |
| `documentType` | CONTRACT | INVOICE | DELIVERY | LETTER | OFFER | RECEIPT | OTHER | Yes |
| `name` | string | Yes |
| `documentNumber` | string | No |
| `contractId` | string | No |
| `contractName` | string | No |
| `partnerId` | string | No |
| `partnerName` | string | No |
| `creationDate` | string | Yes |
| `status` | DRAFT | FINAL | No |
| `source` | GENERATED | UPLOADED | No |
| `templateId` | string | No |
| `sourceDocumentId` | string | No |
| `lineItems` | array of object (LineItemSchema) | No |
| `taxBreakdown` | array of object (TaxBreakdownEntrySchema) | No |
| `netAmount` | number | No |
| `taxAmount` | number | No |
| `totalAmount` | number | No |
| `currency` | string | No |
| `dueDate` | string | No |
| `fileId` | string | No |
| `fileType` | string | No |

### POST `/v1/documents/processing`

| Field | Type | Required |
| --- | --- | --- |
| `documentType` | CONTRACT | INVOICE | DELIVERY | LETTER | OFFER | RECEIPT | OTHER | Yes |
| `name` | string | Yes |
| `documentNumber` | string | No |
| `contractId` | string | No |
| `contractName` | string | No |
| `partnerId` | string | No |
| `partnerName` | string | No |
| `creationDate` | string | Yes |
| `status` | DRAFT | FINAL | No |
| `source` | GENERATED | UPLOADED | No |
| `templateId` | string | No |
| `sourceDocumentId` | string | No |
| `lineItems` | array of object (LineItemSchema) | No |
| `taxBreakdown` | array of object (TaxBreakdownEntrySchema) | No |
| `netAmount` | number | No |
| `taxAmount` | number | No |
| `totalAmount` | number | No |
| `currency` | string | No |
| `dueDate` | string | No |
| `fileId` | string | No |
| `fileType` | string | No |

### GET `/v1/documents/{documentId}`

_No request body._

### PUT `/v1/documents/{documentId}`

| Field | Type | Required |
| --- | --- | --- |
| `version` | integer | Yes |
| `documentType` | CONTRACT | INVOICE | DELIVERY | LETTER | OFFER | RECEIPT | OTHER | No |
| `name` | string | No |
| `documentNumber` | string | No |
| `contractId` | string | No |
| `contractName` | string | No |
| `partnerId` | string | No |
| `partnerName` | string | No |
| `creationDate` | string | No |
| `status` | DRAFT | FINAL | No |
| `source` | GENERATED | UPLOADED | No |
| `templateId` | string | No |
| `sourceDocumentId` | string | No |
| `lineItems` | array of object (LineItemSchema) | No |
| `taxBreakdown` | array of object (TaxBreakdownEntrySchema) | No |
| `netAmount` | number | No |
| `taxAmount` | number | No |
| `totalAmount` | number | No |
| `currency` | string | No |
| `dueDate` | string | No |
| `fileId` | string | No |
| `fileType` | string | No |

### DELETE `/v1/documents/{documentId}`

_No request body._

### POST `/v1/documents/{documentId}/generate-einvoice`

_No request body._

### POST `/v1/documents/{documentId}/send`

_No request body._

## Files

### GET `/v1/files`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `limit` | integer | No | `20` |
| `page` | integer | No | `1` |

_No request body._

### GET `/v1/files/download-url`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `key` | string | No | — |
| `fileId` | string | No | — |

_No request body._

### POST `/v1/files/upload-url`

| Field | Type | Required |
| --- | --- | --- |
| `fileName` | string | Yes |
| `fileSize` | integer | No |
| `contentType` | string | No |
| `skipProcessing` | boolean | No |

### DELETE `/v1/files/{fileId}`

_No request body._

## Leads

### GET `/v1/leads`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `status` | string | No | — |
| `limit` | integer | No | `20` |
| `page` | integer | No | `1` |

_No request body._

### POST `/v1/leads`

| Field | Type | Required |
| --- | --- | --- |
| `name` | string | Yes |
| `contactEmail` | string | No |
| `contactPhone` | string | No |
| `source` | WEBSITE | REFERRAL | EVENT | LINKEDIN | OTHER | Yes |
| `notes` | string | No |

### GET `/v1/leads/{leadId}`

_No request body._

### PUT `/v1/leads/{leadId}`

| Field | Type | Required |
| --- | --- | --- |
| `version` | integer | Yes |
| `name` | string | No |
| `contactEmail` | string | No |
| `contactPhone` | string | No |
| `source` | WEBSITE | REFERRAL | EVENT | LINKEDIN | OTHER | No |
| `status` | LEAD | QUALIFIED | WON | LOST | No |
| `notes` | string | No |

### DELETE `/v1/leads/{leadId}`

_No request body._

### POST `/v1/leads/{leadId}/convert`

| Field | Type | Required |
| --- | --- | --- |
| `contractName` | string | No |
| `totalValue` | number | No |
| `currency` | string | No |
| `startDate` | string | No |

## Licenses

### GET `/v1/licenses`

_No request body._

## Newsletter

### GET `/v1/newsletter/confirm`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `token` | string | No | — |

_No request body._

### POST `/v1/newsletter/signup`

| Field | Type | Required |
| --- | --- | --- |
| `email` | string | Yes |

### GET `/v1/newsletter/unsubscribe`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `token` | string | No | — |

_No request body._

## Notes

### GET `/v1/notes`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `parentType` | string | No | — |
| `parentId` | string | No | — |
| `limit` | integer | No | `20` |
| `page` | integer | No | `1` |

_No request body._

### POST `/v1/notes`

| Field | Type | Required |
| --- | --- | --- |
| `parentType` | PARTNER | CONTRACT | PAYMENT | PRODUCT | Yes |
| `parentId` | string | Yes |
| `type` | NOTE | REMINDER | Yes |
| `title` | string | Yes |
| `content` | string | Yes |
| `dueDate` | string | No |

### GET `/v1/notes/{noteId}`

_No request body._

### PUT `/v1/notes/{noteId}`

| Field | Type | Required |
| --- | --- | --- |
| `version` | integer | Yes |
| `title` | string | No |
| `content` | string | No |
| `dueDate` | string | No |
| `done` | boolean | No |

### DELETE `/v1/notes/{noteId}`

_No request body._

## Partners

### GET `/v1/partners`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `limit` | integer | No | `20` |
| `page` | integer | No | `1` |

_No request body._

### POST `/v1/partners`

| Field | Type | Required |
| --- | --- | --- |
| `name` | string | Yes |
| `type` | CUSTOMER | VENDOR | Yes |
| `description` | string | No |
| `website` | string | No |
| `logoFileId` | string | No |
| `addresses` | array of object (AddressSchema) | No |
| `tags` | array of string | No |
| `vatId` | string | No |
| `registrationCourt` | string | No |
| `registrationNumber` | string | No |

### GET `/v1/partners/{partnerId}`

_No request body._

### PUT `/v1/partners/{partnerId}`

| Field | Type | Required |
| --- | --- | --- |
| `version` | integer | Yes |
| `name` | string | No |
| `type` | CUSTOMER | VENDOR | No |
| `description` | string | No |
| `website` | string | No |
| `logoFileId` | string | No |
| `addresses` | array of object (AddressSchema) | No |
| `tags` | array of string | No |
| `vatId` | string | No |
| `registrationCourt` | string | No |
| `registrationNumber` | string | No |

### DELETE `/v1/partners/{partnerId}`

_No request body._

## Payments

### GET `/v1/payments`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `documentId` | string | No | — |
| `contractId` | string | No | — |
| `sort` | string | No | — |
| `limit` | integer | No | `1000` |
| `page` | integer | No | `1` |

_No request body._

### POST `/v1/payments`

| Field | Type | Required |
| --- | --- | --- |
| `direction` | INCOMING | OUTGOING | Yes |
| `documentId` | string | No |
| `documentNumber` | string | No |
| `contractId` | string | No |
| `contractName` | string | No |
| `partnerId` | string | Yes |
| `partnerName` | string | Yes |
| `amount` | number | Yes |
| `currency` | string | Yes |
| `paymentDate` | string | Yes |
| `status` | PENDING | MARKED | SUCCEEDED | FAILED | REFUNDED | No |
| `paymentMethod` | BANK_TRANSFER | CREDIT_CARD | DIRECT_DEBIT | OTHER | No |
| `stripePaymentIntentId` | string | No |
| `failureReason` | string | No |

### GET `/v1/payments/{paymentId}`

_No request body._

### PUT `/v1/payments/{paymentId}`

| Field | Type | Required |
| --- | --- | --- |
| `version` | integer | Yes |
| `status` | PENDING | MARKED | SUCCEEDED | FAILED | REFUNDED | No |
| `amount` | number | No |
| `currency` | string | No |
| `paymentDate` | string | No |
| `paymentMethod` | BANK_TRANSFER | CREDIT_CARD | DIRECT_DEBIT | OTHER | No |
| `stripePaymentIntentId` | string | No |
| `failureReason` | string | No |
| `contractId` | string | No |
| `contractName` | string | No |

### DELETE `/v1/payments/{paymentId}`

_No request body._

### POST `/v1/webhooks/stripe`

| Field | Type | Required |
| --- | --- | --- |
| `direction` | INCOMING | OUTGOING | Yes |
| `documentId` | string | No |
| `documentNumber` | string | No |
| `contractId` | string | No |
| `contractName` | string | No |
| `partnerId` | string | Yes |
| `partnerName` | string | Yes |
| `amount` | number | Yes |
| `currency` | string | Yes |
| `paymentDate` | string | Yes |
| `status` | PENDING | MARKED | SUCCEEDED | FAILED | REFUNDED | No |
| `paymentMethod` | BANK_TRANSFER | CREDIT_CARD | DIRECT_DEBIT | OTHER | No |
| `stripePaymentIntentId` | string | No |
| `failureReason` | string | No |

## Plans

### GET `/v1/plans`

_No request body._

### PATCH `/v1/plans`

_No request body._

## Products

### GET `/v1/products`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `limit` | integer | No | `20` |
| `page` | integer | No | `1` |

_No request body._

### POST `/v1/products`

| Field | Type | Required |
| --- | --- | --- |
| `name` | string | Yes |
| `type` | SERVICE | GOODS | Yes |
| `unitPrice` | number | Yes |
| `currency` | string | Yes |
| `unit` | string | No |
| `description` | string | No |
| `photoFileId` | string | No |
| `taxRateId` | string | No |
| `tags` | array of string | No |

### GET `/v1/products/{productId}`

_No request body._

### PUT `/v1/products/{productId}`

| Field | Type | Required |
| --- | --- | --- |
| `version` | integer | Yes |
| `name` | string | No |
| `type` | SERVICE | GOODS | No |
| `unitPrice` | number | No |
| `currency` | string | No |
| `unit` | string | No |
| `description` | string | No |
| `photoFileId` | string | No |
| `taxRateId` | string | No |
| `tags` | array of string | No |

### DELETE `/v1/products/{productId}`

_No request body._

## Startup Metrics

### GET `/v1/startup-metrics/timeseries`

_No request body._

## Subscription Billing

### POST `/v1/webhooks/stripe-subscriptions`

| Field | Type | Required |
| --- | --- | --- |
| `paymentMethodId` | string | Yes |

## Tax Rates

### GET `/v1/tax-rates`

**Query parameters**

| Parameter | Type | Required | Default |
| --- | --- | --- | --- |
| `limit` | integer | No | `20` |
| `page` | integer | No | `1` |

_No request body._

### POST `/v1/tax-rates`

| Field | Type | Required |
| --- | --- | --- |
| `name` | string | Yes |
| `rate` | number | Yes |
| `isDefault` | boolean | No |
| `vatCategoryCode` | string | No |

### PATCH `/v1/tax-rates/{taxRateId}`

| Field | Type | Required |
| --- | --- | --- |
| `version` | integer | Yes |
| `name` | string | No |
| `rate` | number | No |
| `isDefault` | boolean | No |
| `vatCategoryCode` | string | No |

### DELETE `/v1/tax-rates/{taxRateId}`

_No request body._

## Usage

### GET `/v1/usage`

_No request body._

## Users

### PATCH `/v1/me/newsletter-subscription`

| Field | Type | Required |
| --- | --- | --- |
| `subscribed` | boolean | Yes |

### GET `/v1/users`

_No request body._

### POST `/v1/users`

| Field | Type | Required |
| --- | --- | --- |
| `name` | string | Yes |
| `email` | string | Yes |
| `role` | admin | user | Yes |

### POST `/v1/users/confirm`

| Field | Type | Required |
| --- | --- | --- |
| `name` | string | Yes |
| `email` | string | Yes |
| `role` | admin | user | Yes |

### GET `/v1/users/{userId}`

_No request body._

### PATCH `/v1/users/{userId}`

| Field | Type | Required |
| --- | --- | --- |
| `role` | admin | user | Yes |

### DELETE `/v1/users/{userId}`

_No request body._
