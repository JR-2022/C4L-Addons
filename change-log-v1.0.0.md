# Change Log for Cloud4Log Addons

## Release 1.0.0 Breaking Changes

**Note:** This is a preliminary version and is still subject to change.

### Consignee order number endpoint
- Endpoint change:
    - Deleted: `PUT /delivery-notes/{deliveryNoteKey}/consigneeOrderNumber`

### Certification numbers checked PATCH endpoint
- Endpoint name change:
    - From: `PATCH /delivery-notes/{deliveryNoteKey}/certification-numbers-checked`
    - To:   `PATCH /organization-sites/{organizationSiteKey}/consignee/delivery-notes/{deliveryNoteKey}`
- Function name change:
    - From: `patchCertificationNumbersChecked`
    - To:   `patchDeliveryNoteConsigneeData`
- Parameter change (in path name):
    `PATCH /organization-sites/{organizationSiteKey}/consignee/delivery-notes/{deliveryNoteKey}` requires `organizationSiteKey` as parameter
- Parameter change (in request body):
    - This endpoint now includes the `consigneeOrderNumber` property, which was previously part of the deleted consignee order number endpoint: `PUT /delivery-notes/{deliveryNoteKey}/consigneeOrderNumber`.

### Certification numbers checked GET endpoint
- Endpoint name change:
    - From: `GET /organization-sites/{organizationSiteKey}/delivery-notes/{deliveryNoteKey}`
    - To:   `GET /organization-sites/{organizationSiteKey}/consignee/delivery-notes/{deliveryNoteKey}`
- Function name change:
    - From: `getCertificationNumbersChecked`
    - To:   `getSingleDeliveryNoteMetaDataAddons`

### Article endpoints
- The property `pos` is now a string instead of a number through the entire API.

- Endpoint path name, permission and schema changes.
    - PATCH Article Edit
        - From: `PATCH /organization-sites/{organizationSiteKey}/articles/{articleKey}/edit`
        - To:   `PATCH /organization-sites/{organizationSiteKey}/consignee/articles/{articleKey}/edit`
        - Permission change: Only usable by consignee
        - Schema change: Response property `expirationDate` renamed to `dateExpired` and type changed from string to number
        - Schema change: Currently only the `edits` object is returned. Now it returns not only the `edits` object but also all of the other articles properties. E.g. same as in `GET /organization-sites/{organizationSiteKey}/delivery-notes/{deliveryNoteKey}/articles`.

    - POST Article Edit
        - From: `POST /organization-sites/{organizationSiteKey}/delivery-notes/{deliveryNoteKey}/articles/edit`
        - To:   `POST /organization-sites/{organizationSiteKey}/consignee/delivery-notes/{deliveryNoteKey}/articles/edit`
        - Permission change: Only usable by consignee
        - Schema change: Request body now has required properties (`index`, `quantity`, `containerType`, `description`, `articleNumber`). Previously, all properties were optional.
        - Schema change: Request body property `expirationDate` renamed to `dateExpired` and type changed from string to number
        - Schema change: Response property `expirationDate` renamed to `dateExpired` and type changed from string to number (also in the nested objects)
        - Schema change: Response property `metaData` is now an array.

    - DELETE Article Edit
        - From: `DELETE /organization-sites/{organizationSiteKey}/articles/{articleKey}/edit`
        - To:   `DELETE /organization-sites/{organizationSiteKey}/consignee/articles/{articleKey}/edit`
        - Permission change: Only usable by consignee

    - PATCH Article Check
        - From: `PATCH /organization-sites/{organizationSiteKey}/articles/{articleKey}/check`
        - To:   `PATCH /organization-sites/{organizationSiteKey}/consignee/articles/{articleKey}/check`
        - Permission change: Only usable by consignee
        - Status code change: 204 -> 200. With the changed status code the endpoint now also returns the article as object.

    - GET Articles
        - `GET /organization-sites/{organizationSiteKey}/delivery-notes/{deliveryNoteKey}/articles`
        - Permission change: No access to the articles by anyone other than the consignor if the delivery note is in status open.
        - Schema change: Response property `expirationDate` renamed to `dateExpired` and type changed from string to number (also in the nested objects)
        - Schema change: Response property `metaData` is now an array.
    
    - POST Articles
        - `POST /organization-sites/{organizationSiteKey}/consignor/delivery-notes/{deliveryNoteKey}/articles`
        - Schema change: Request body now has required properties (`index`, `quantity`, `containerType`, `description`, `articleNumber`). Previously, all properties were optional.
        - Schema change: Request body property `expirationDate` renamed to `dateExpired` and type changed from string to number
        - Schema change: Response property `expirationDate` renamed to `dateExpired` and type changed from string to number (also in the nested objects)
        - Schema change: Response property `metaData` is now an array.

### Discrepancy endpoints
- Permission changes
    - `GET /organization-sites/{organizationSiteKey}/delivery-notes/{deliveryNoteKey}/articles/{articleKey}/discrepancies`
    - `GET /organization-sites/{organizationSiteKey}/delivery-notes/{deliveryNoteKey}/articles/{articleKey}/discrepancies/{discrepancyKey}`
    - Permission change: Consignor and carrier can only access discrepancies if the delivery note is closed.

### API Keys
- `POST /api-keys-storage/renew`
- Previously, the description stated that it returns a 201 or 204, whereas it just returned 201.
- Now, the endpoint returns status codes 200 and 201 depending on the type of modification (create or update). For both status codes, the response now includes the expiryDate as an object.

### Property customerArticleNumber
- Renamed `costumerArticleNumber` to `customerArticleNumber` throughout the entire API.
- Endpoints:
    - `GET /organization-sites/{organizationSiteKey}/delivery-notes/{deliveryNoteKey}/articles`
    - `POST /organization-sites/{organizationSiteKey}/consignor/delivery-notes/{deliveryNoteKey}/articles`
    - `POST /organization-sites/{organizationSiteKey}/delivery-notes/{deliveryNoteKey}/articles/edit`
    - `PATCH /organization-sites/{organizationSiteKey}/articles/{articleKey}/edit`
