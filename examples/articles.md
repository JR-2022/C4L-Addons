# Uploading Articles to Cloud4Log (C4L) Addons

## Prerequisites

First you have to understand that Cloud4Log consists of two systems: The **BASIC** system and the **ADDONS** system.

> **Important:** Ensure that your organization has access to the C4L BASIC & ADDONS system before proceeding.  
> If you are not yet onboarded, please contact: [torsten.jaenicke-roessler@t-systems.com](mailto:torsten.jaenicke-roessler@t-systems.com)

## Workflow

Via the basic system you need to upload a delivery note first. After that, you can upload articles to the delivery note via the ADDONS system.

## API Documentation Links

### BASIC System

- **PROD:** [https://api.cloud4log.com/api-docs-combined/](https://api.cloud4log.com/api-docs-combined/)
- **API-TEST:** [https://dlsbackend.apitest.cloud4log.dev/api-docs-combined/](https://dlsbackend.apitest.cloud4log.dev/api-docs-combined/) *(test freely here)*

### ADDONS System

- **PROD:** [https://dls.addons.cloud4log.dev/api-docs-combined/](https://dls.addons.cloud4log.dev/api-docs-combined/)
- **API-TEST:** [https://apitest.dls.addons.cloud4log.dev/api-docs-combined/](https://apitest.dls.addons.cloud4log.dev/api-docs-combined/) *(test freely here)*

## Example: Uploading Articles

### Endpoint

```
POST /organization-sites/{organizationSiteKey}/consignor/delivery-notes/{deliveryNoteKey}/articles
```

### Parameters

- `organizationSiteKey` - Your organization site identifier
- `deliveryNoteKey` - The delivery note identifier

### Request Body

```json
[
    {
        "index": 0,
        "gtin": "",
        "description": "",
        "pos": "",
        "articleNumber": "string",
        "customerArticleNumber": "",
        "containerType": "string",
        "quantity": 1,
        "danger": true,
        "dangerClass": "",
        "dateExpired": 9007199254740991,
        "batchNumber": "",
        "qs": true,
        "organic": true,
        "naturland": true,
        "gqb": true,
        "articleOrderNumber": "",
        "ggn": "string",
        "countryOfOrigin": "string"
    }
]
```

## Additional Operations

There are many other endpoints available for managing articles in C4L Addons, such as:

- Editing articles
- Checking articles
- Deleting articles

Refer to the API documentation links above for complete details on required headers, request parameters, and response formats.

## Property Descriptions

### `index`
Index is used for identifying each item uniquely in the list. It should be a unique number for each item, starting at 0 and incrementing by 1 for each subsequent item. Also used to maintain the order of items in the list.

### `pos`
The position can be any string value that helps identify the item's position.  
**Examples:** `0, 1, 2` or `1A, 1B, 1C` or any custom format  
Can be omitted if not applicable.

### `articleNumber`
Internal article reference number.  
**Common labels:** Nr., Art.-Nr., Artikelnummer, Artikel, Art.Nr.  
You can provide any string aligned with your internal system.

### `customerArticleNumber`
Customer-specific article number.  
**Common labels:** Kunde Art.-Nr., Kunden-Artikelnummer, K-Art.Nr., KdArtNr, Ihre Artikelnummer  
You can provide any string aligned with your internal system, or omit if not applicable.

### `containerType`
Should always exist.  
**Examples:** Karton, Europalette, DDP Halbpalette, H1-Palette, CHEP-Variants, etc.
