---
title: updateGiftRegistry mutation | Commerce Web APIs
edition: ee
---

# updateGiftRegistry mutation

The `updateGiftRegistry` mutation modifies properties of specified gift registry. It does not update the items in a gift registry or registrants. Use the `updateGiftRegistryItems` or `updateGiftRegistryRegistrants` mutation to modify gift registry items or registrants.

This mutation requires a valid [customer authentication token](../../customer/mutations/generate-token.md).

## Syntax

```graphql
mutation {
  updateGiftRegistry(
    giftRegistryUid: ID!
    giftRegistry: UpdateGiftRegistryInput!
  ) {
    UpdateGiftRegistryOutput
  }
}
```

## Example usage

The following example changes the privacy, the message, and the event date for a gift registry.

**Request:**

```graphql
mutation{
  updateGiftRegistry(
    giftRegistryUid: "D0R6d2B7aZWOQuuWftHZ0iwuexQPgaei",
    giftRegistry: {
      privacy_settings: PUBLIC
      message: "Help us celebrate Bill and Julie's wedding, which will be held on May 8, 2021"
      dynamic_attributes: {
        code: "event_date"
        value: "2021-05-08"
      }
    })
  {
    gift_registry {
      uid
      event_name
      message
      status
      privacy_settings
      dynamic_attributes {
        code
        label
        value
      }
    }
  }
}
```

**Response:**

```json
{
  "data": {
    "updateGiftRegistry": {
      "gift_registry": {
        "uid": "D0R6d2B7aZWOQuuWftHZ0iwuexQPgaei",
        "event_name": "Bill and Julie's wedding",
        "message": "Help us celebrate Bill and Julie's wedding, which will be held on May 8, 2021",
        "status": "ACTIVE",
        "privacy_settings": "PUBLIC",
        "dynamic_attributes": [
          {
            "code": "event_country",
            "label": "Country",
            "value": "US"
          },
          {
            "code": "event_date",
            "label": "Wedding Date",
            "value": "2021-05-08"
          },
          {
            "code": "event_location",
            "label": "Location",
            "value": "Ann Arbor, MI"
          },
          {
            "code": "number_of_guests",
            "label": "Number of Guests",
            "value": "101"
          }
        ]
      }
    }
  }
}
```

## Input attributes

The `updateGiftRegistry` mutation requires the following input objects.

Attribute |  Data Type | Description
--- | --- | ---
`giftRegistryUid` | ID! | The unique ID of the gift registry to update
`giftRegistry` | [UpdateGiftRegistryInput!](#updategiftregistryinput-attributes) | Defines the attributes to be updated.

### UpdateGiftRegistryInput attributes

The `UpdateGiftRegistryInput` object contains the following attributes:

Attribute |  Data Type | Description
--- | --- | ---
`dynamic_attributes` | [[GiftRegistryDynamicAttributeInput](#giftregistrydynamicattributeinput-attributes)] | An array of attributes that define elements of the gift registry. Each attribute is specified as a code-value pair
`event_name` | String | The name of the event
`message` | String | A message describing the event
`privacy_settings` | GiftRegistryPrivacySettings! | Indicates whether the registry is PRIVATE or PUBLIC
`shipping_address` | [GiftRegistryShippingAddressInput](#giftregistryshippingaddressinput-attributes) | The address for shipping the gift registry. Specify either the `address_data` object or the `address_id` attribute. Validation fails if both are provided
`status` | GiftRegistryStatus | An enum that states whether the gift registry is ACTIVE or INACTIVE. Only the registry owner can access this attribute

### GiftRegistryDynamicAttributeInput attributes

The `GiftRegistryDynamicAttributeInput` object contains the following attributes:

Attribute |  Data Type | Description
--- | --- | ---
`code` | ID! | A unique key for an additional attribute of the event
`value` | String! | A corresponding value for the code

### GiftRegistryShippingAddressInput attributes

The `GiftRegistryShippingAddressInput` object contains the following attributes:

Attribute |  Data Type | Description
--- | --- | ---
`address_data` | [CustomerAddressInput](#customeraddressinput-attributes) | The complete details of the shipping address
`address_id` | ID | The ID of a pre-defined customer address

### CustomerAddressInput attributes

import CustomerAddressInput from '/src/pages/_includes/graphql/customer-address-input-24.md'

<CustomerAddressInput />

## Output attributes

The `UpdateGiftRegistryOutput` output object contains the following attribute:

Attribute |  Data Type | Description
--- | --- | ---
`gift_registry` | [GiftRegistry](#giftregistry-attributes) | Contains the updated gift registry

### GiftRegistry attributes

import GiftRegistry from '/src/pages/_includes/graphql/gift-registry.md'

<GiftRegistry />
