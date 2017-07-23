---
title: Types of Engagement Attributes
Keywords:
level1: Documents
level2: Guides
level3: Engagement Attributes
order: 20
permalink: engagment-attributes-types.html
indicator: both
---

There are 10 supported Engagement Attributes, organized into 3 categories:

* eCommerce info

* Visitor info

* Visitor journey

Each Engagement Attribute has its own data structure and can be sent to LivePerson using JavaScript code, or extracted from your page using LivePerson’s scraping tool.

**Code example**:

```javascript
lpTag.sdes = lpTag.sdes||[];
lpTag.sdes.push(
// SDEs located here
);
```

### eCommerce info

eCommerce info Engagement Attributes allow you to track eCommerce-related activities on your website.

#### Cart update

This Engagement Attribute is used to get the status of the visitor’s shopping cart. The cart status includes the product items within the cart and its total monetary value.

The cart value and/or the products in the cart can be used to target visitors. For example, you can target low value shoppers and encourage them to buy more in order to get your free shipping coupon. You can also offer complementary products in addition to products in the cart.

**Data structure**:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| type | The event name ("cart") | string  | "cart" | true |
| total | Total cart value | double  | 11.7 | true |
| currency | currenct of the total cart value | string  | USD | false |
| numItems | Number of items in cart | integer  | 6 | true |
| products | array of items in cart | array of Products objects  | [ {<br>"product":{...},<br>"quantity": 2<br>}<br>, {<br>"product": {...},<br>"quantity": 1<br>} ] | false |

**Products Object**:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| product | Product details | product<br>object  | {<br>"name": "prod1",<br>"category":<br>"cat_1",<br>"sku": "sku",<br>"price": 7.8<br>} | true |
| quantity | Number of items of this product in cart | integer  | 1 | false |

**Product Object**:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| name | Product name | string  | "prod1" | false |
| category | Product category name | string  | "category1" | false |
| sku | Product SKU or unique identifier | string  | "dep1" | false |
| price | product price | double  | 7.8 | false |

**Cart update SDE JSON example**:

```json
{
  "type": "cart", //MANDATORY
  "total": 11.7, //TOTAL CART VALUE
  "currency": "USD", //CURRENCY CODE
  "numItems": 6, //NUMBER OF ITEMS IN CART
  "products": [{ //ARRAY OF PRODUCTS
    "product": {
    "name": "prod1", //PRODUCT NAME
    "category": "category", //PRODUCT CATEGORY NAME
    "sku": "sku", //PRODUCT SKU OR UNIQUE IDENTIFIER
    "price": 7.8 //PRODUCT PRICE
    }, "quantity": 1 //NUMBER OF PRODUCTS
  }]
}
```

#### Transaction

This Engagement Attribute is used to track any money transaction, purchase of items, or deposit, including the items themselves and their details. The total transaction value can be used to track conversions. It is also displayed in your revenue reports as a means of measuring the monetary value of your campaigns.

**Data structure**:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| type | The event name ("purchase") | string  | "purchase" | true |
| total | Total transaction value | double  | 11.7 | false |
| currency | Currency of the total transaction value | string  | USD | false |
| orderId | Unique order or receipt ID | string  | "orderId123" | false |
| cart | Cart details | Cart object  | {<br>"numItems": 6,<br>"products":<br>[ {... },<br>{...}]<br>} | false |

**Cart Object**

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| Products | Array of Items in cart | array of Products objects  | [ {<br>"product": {...},<br>"quantity": 2<br>}<br>, {<br>"product": {...},<br>"quantity": 1<br>} ] | true |
| numItems | Number of items in cart | integer  | 6 | false |

**Transaction SDE JSON example**:

```json
{
  "type": "purchase", //MANDATORY
  "total": 11.7, //TOTAL VALUE OF THE TRANSACTION AFTER DISCOUNT
  "currency": "USD", //CURRENCY CODE
  "orderId": "DRV1534XC", //UNIQUE ORDER ID OR RECEIPT ID
  "cart":{
      "products": [{
            "product": {
              "name": "antivirus pro plan", //PRODUCT NAME
              "category": "software", //PRODUCT CATEGORY NAME
              "sku": "xyz001", //PRODUCT SKU OR UNIQUE IDENTIFIER
              "price": 7.8 //SINGLE PRODUCT PRICE
            },
      "quantity": 3 //QUANTITY OF THIS PRODUCT
      }]
    }
}
```

#### Viewed product

This Engagement Attribute is used to track a product or service that interests visitors. Each product is described by Name, Category, and SKU.

This information can be used to target visitors. For example, you can offer products to visitors which are in the same category or price range as the products they previously viewed.

**Data structure**:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| type | The event name ("prodView")  | string | "prodView" | true |
| currency | Currency of the viewed products | string  | USD | false |
| products | Array of items in cart | array of Products objects  | U[ {<br>"product": {...},<br>"quantity": 2<br>}<br>, {<br>"product": {...},<br>"quantity": 1<br>} ] | false |

**Viewed Product SDE JSON example**:

```json
{
    "type": "prodView", //MANDATORY
    "currency": "USD", //CURRENCY CODE
    "products": [{ //ARRAY OF PRODUCTS
        "product": {
            "name": "red high heel shoe", //PRODUCT NAME
            "category": "women shoes", //PRODUCT CATEGORY NAME
            "sku": "xyz567", //PRODUCT SKU OR UNIQUE IDENTIFIER
            "price": 77.8 //SINGLE PRODUCT PRICE
        }
    }]
}
```

### Visitor Info

Visitor Info Engagement Attributes allow you to collect more information about your visitors, including where they came from, and the affiliates they are associated with.

#### Customer Info

This Engagement Attribute is used to collect information about a registered visitor such as the customer type (for example, VIP or Platinum), and their unique identifier.

This information can be used to segment visitors and tailor an experience based on their attributes (customer type, status, and balance). For example, you can invite your most valuable customers to chat with your relevant agents, while offering self-service content to low-tier customers.

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| type | The event name ("ctmrinfo")  | string | "ctmrinfo" | true |
| ctype | Customer type/tier (case insensitive) | string  | "Gold" | false |
| cstatus | Customer status (case insensitive) | string  | "migrated" | false |
| balance | Customer's finanicial balance | double  | 2.6 | false |
| currency | Currency of the customer's financial balance | string  | USD | false |
| customerId | Customer's unique identifier | string  | "1234abc" | false |
| socialId | Social Media identifier(e.g., Facebook, Twitter). This parameter represents your internal identifier. | "11256324780"  | 2.6 | false |
| imei | Unique device/phone identifier | string  | "3543546543545688" | false |
| userName | Customer's user name | string  | "user000" | false |
| companySize | Number of company employees | int  | 500 | false |
| companyBranch | Company branch | string  | "East village" | false |
| accountName | Customer's company name | string  | "oxford insurance company" | false |
| role | Customer's title | string  | "Marketing manager" | false |
| lastPaymentDate | Last payment date. This parameter consists of 3 integer fields: year, month, day, | data object  | {<br>"day": 15,<br>"month": 10,<br>"year": 2014<br>} | false |
| registrationDate | Registration date. This parameter consists of 3 integer fields: year, month, day, | data object  | {<br>"day": 23,<br>"month": 5,<br>"year": 2013<br>} | false |
| loginStatus | Login status | integer  |  | false |
| storeZipCode | A store ZIP code the customer is associated with. The ZIP code is mapped to multiple stores in the same geographic area. | string  | "12205" | false |
| storeNumber  | A specific store number the customer is associated with | string  | "1241" | false |

**Customer info SDE JSON example**:

```json
{
    "type": "ctmrinfo", //MANDATORY
    "info": {
    10
    ENGAGEMENT ATTRIBUTES OVERVIEW
    "cstatus": "cancelled", //CUSTOMER LIFECYCLE STATUS. FROM PRE-DEFINED LIST
    "ctype": "vip", //CUSTOMER TYPE OR TIER. FROM PRE-DEFINED LIST
    "customerId": "138766AC", //UNIQUE CUSTOMER IDENTIFIER
    "balance": -400.99, //THE CUSTOMER FINANCIAL BALANCE IN DECIMAL VALUE
    "currency": "USD", //CURRENCY CODE
    "socialId": "11256324780", //SOCIAL ID OF YOUR CHOICE: FACEBOOK, TWITTER
    ETC...
    "imei": "3543546543545688", //UNIQUE DEVICE OR PHONE IDENTIFIER
    "userName": "user000", //CONSUMER NICKNAME OR USERNAME
    "companySize": 500, //COMPANY SIZE MEASURED BY NUMBER OF EMPLOYEES
    "accountName": "bank corp", //THE CUSTOMER'S COMPANY NAME
    "role": "broker", //CONSUMER ROLE TITLE
    "lastPaymentDate": {
      "day": 15, //THE DAY OF THE LAST PAYMENT NUMERIC VALUE
      "month": 10, //THE MONTH OF THE LAST PAYMENT NUMERIC VALUE
      "year": 2014 //THE YEAR OF THE LAST PAYMENT NUMERIC VALUE
    },
    "registrationDate": {
      "day": 23, //THE DAY OF THE REGISTRATION NUMERIC VALUE
      "month": 5, //THE MONTH OF THE REGISTRATION NUMERIC VALUE
      "year": 2013 //THE YEAR OF THE REGISTRATION NUMERIC VALUE
    },
    "storeNumber": "123865", //STORE NUMBER
    "storeZipCode": "20505" //STORE ZIP CODE
  }
}
```

### Marketing source

This Engagement Attribute is used to obtain more information about the marketing source of your visitors, which channel or campaign drove visitors to your website, and with which affiliates they are associated.

This information can be used to segment visitors and tailor an experience based on the traffic source (originating channel, campaign or affiliate). For example, you can display a specific offer to visitors that arrived to the website through a specific affiliate, or route a visitor to a relevant agent based on the originating channel.

**Data structure**:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| type | The event name ("mrktInfo")  | string | "mrktInfo" | true |
| info | Marketing source information | Info object  | {<br>"channel": "1",<br>"Affiliate":<br>"Yahoo", "campaignId":<br>"US coupon campaign" } | false |

Info object:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| channel | Originating marketing channel  | integer | 0-Direct,<br>1-Search,<br>2-Social,<br>3-Email,<br>4-Referral | false |
| affiliate | Affiliate name | string  | "Yahoo" | false |
| campaignID | Campaign ID | string  | "camp12" | false |

**Marketing source SDE JSON example**:

``json
{
  "type": "mrktInfo", //MANDATORY
    "info": {
      "channel": "1", //ORIGINATING CHANNEL ENUM:
      "affiliate": "Yahoo", //AFFILIATE NAME
      "campaignId": "US coupon campaign" //EXTERNAL ORIGINATING CAMPAIGN
  }
}
```

#### Personal info

This Engagement Attribute is used to collect personal information about your visitors. You can pass login information from cookies, or from questions you ask them in your forms.

This information can be used to segment visitors and tailor an experience based on their attributes (age and gender). For example, you can exclude visitors that are too young for your service/product, or display different wording or offers based on the visitor’s gender.

**Data structure**:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| type | The event name ("personal")  | string | "personal" | true |
| firstname | Visitor's first name | string  | "John" | false |
| lastname | Visitor's surname | string  | "Doe" | false |
| age | Visitor's age | Age object  | {<br>"age": 34,<br>"year": 1980,<br>"month": 4,<br>"day": 15<br>} | false |
| contacts | Visitors contact info | array of Contact object  | [{<br>"email":"m@m.com",<br>"phone":<br>"+1 212-788-8877" }] | false |
| gender | Visitor's gender | integer  | 0-MALE,<br>1-FEMALE,<br>2-OTHER | false |
| company | Visitor's company | string  | "Microsoft Ltd." | false |
| language | Campaign ID | Visitor's language. The value is an ISO 639-1 Alpha-2 [ISO639‑1] language code in lowercase and an ISO string “en-US” false 3166-1 Alpha-2 [ISO3166‑1] country code in uppercase, separated by a dash or underscore (for compatibility). For example, en-US or fr-CA.  | "en-US" | false |

Age object:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| age | Visitor’s age. **Note**: If this parameter is not provided, the age is calculated using year, month, day.  | integer | 47 | false |
| year | Visitor’s year of birth **Note**: This parameter is mandatory if the visitor’s age needs to be calculated. | integer  | "1969" | false |
| month | Visitor's month of birth | integer  | 2 | false |
| day | Visitor's day of birth | integer  | 12 | false |

Contact object:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| email | Visitor's email address  | string | "john@doe.com" | false |
| phone | Visitor's phone number | string  | "5558982312" | false |
| phoneType |Phone type | string  | “HOME”,<br>“MOBILE”,<br>“WORK”,<br>“FAX”,<br>“MAIN”,<br>“HOME_FAX”,<br>“WORK_FAX”,<br>“PAGER”,<br>“OTHER” | false |
| address | Visitor's personal addresses | Address object  | {<br>"country":<br>STRING<br>(,<br>"region": STRING<br>}] | false |
| country | Visitor's country | string. The value is 2 letter code in uppser case ISO3166-1 Alpha-2  | "US" | false |
| region | Visitor's region | string  | "North America" | false |

**Personal info SDE JSON example**:

```json
{
    "type": "personal", //MANDATORY
      "personal": {
        "firstname": "John", // FIRST NAME
        "lastname": "Doe", // SURNAME
      "age": {
          "age": 34, // AGE AS INTEGER
          "year": 1980, // BIRTH YEAR
          "month": 4, // BIRTH MONTH
          "day": 15 // BIRTH DAY
        },
      "contacts": [{
        "email": "myname@example.com", // EMAIL
        "phone": "+1 212-788-8877" // PHONE NUMBER
      }],
      "gender": "MALE", // MALE, FEMALE, OTHER
      "language": "en-US", // LANGUAGE
      "company": "company" // VISITOR COMPANY NAME
    }
}
```

### Visitor Journey

Visitor Journey Engagement Attributes allow you to collect information about key actions that visitors take along their journey, and customize their experience accordingly. This includes the leads they generated, errors they experienced, and more.

#### Lead

This Engagement Attribute is used to track lead information that can help you identify what your visitors are interested in, and where they are in your funnel. This information can be used to track conversions. The lead value will also appear in your revenue reports as a means to measure the monetary value of your campaigns. A session can have more than a single lead in it, and can be connected to a single ticket ID or multiple tickets.

**Data Structure**:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| type | The event name ("lead")  | string | "lead" | true |
| lead | Lead details | Lead object  | "{<br>"topic":<br>"luxury car",<br>"value": 22.22,"<br>"leadId":<br>"xyz123" } | false |

Lead object:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| topic | Lead's name/topic  | string | "topic1" | false |
| value | Lead's value | double  | 99.99 | false |
| currency | Currency of the lead value | string  | USD | false |
| leadId | Lead's identifier / ticket id | string  | "Id12" | false |

**Lead SDE JSON example**:

```json
{
  "type": "lead", //MANDATORY
    "lead": {
      "topic": "luxury car test drive 2015", //TOPIC OR NAME OF A SUBMITTED LEAD
      "value": 22.22, //EVALUATED VALUE OF THE LEAD
      "currency": "USD", //CURRENCY CODE
      "leadId": "xyz123" //LEAD IDENTIFIER OR TICKET ID
  }
}
```

#### Service activity

This Engagement Attribute is used to measure service activities, for example, ordering a checkbook, submitting an application, or requesting a mortgage.

This information can be used to track conversions, for example, a visitor that completed a loan application. It can additionally be used to follow up with visitors, for example, engaging with a visitor whose application has been cancelled. A session can have more than one service activity in it.

**Data structure**:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| type | The event name ("service")  | string | "service" | True |
| service | Service details | Service object  | {<br>"topic": "order",<br>"status": 0,<br>"category":<br>"finance",<br>"serviceId":<br>"service12"<br>} | false |

Service object:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| topic | Service topic or name  | string | "order checkbook" | false |
| status | Status | integer  | 0-Complete,<br>1-In Progress,<br>2- Approved,<br>3- cancelled,<br>4-Not Approved,<br>5-Reviewed,<br>6- Missing Details,<br>7- Closed,<br>8-Removed,<br>9-Assigned,<br>10-Waiting | false |
| category | Category name  | string | "Finance" | false |
| serviceId | Service unique idenitifer or ticket id  | string | "service17" | false |

**Service Activity SDE JSON example**:

```json
{
  "type": "service", //MANDATORY
  "service": {
    "topic": "order checkbook", // SERVICE ACTIVITY TOPIC OR NAME
    "status": 0, // STATUS ENUM
    "category": "finance", // SERVICE CATEGORY NAME
    "serviceId": "service12" // SERVICE UNIQUE IDENTIFIER OR TICKET ID
  }
}
```

#### Visitor error

This Engagement Attribute is used to collect information about errors that visitors experience when they browse the website and fill out forms. All errors are aggregated in a list during
the session until resolved.

This information can be used to offer help to visitors who are struggling to complete a specific action.

**Data Structure**:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| type | The event name ("error")  | string | "error" | True |
| error | Error details | Error object  | {<br>"contextId":<br>" application",<br>"message":<br>"Missing data",<br>"code":<br>"er100004"<br>"level": 10,<br>"resolved": false<br>} | false |

Error object:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| contextId | Error context  | string | "Credit card application" | false |
| message | Error message | string  | "Expiration date missing" | false |
| code | Error code  | string | "XV45EZT" | false |
| level | Error level  | long | 10 | false |
| resolved | Resolution status  | Boolean | false | false |

**Visitor Error SDE JSON example**:

```json
{
  "type": "error", //MANDATORY
  "error": {
    "contextId": "Credit card application",
    "message": "Expiration date missing", // ERROR MESSAGE
    "code": "er100004" // ERROR CODE
      "level": 10,
    "resolved": false
  }
}
```

#### Searched content

This Engagement Attribute is used to to report on content that was searched by consumers on the brand’s website such as FAQ and different articles or products.

This information can be used to offer help to visitors based on their searches.

Data structure:

| Name | Description  | Type  | Value/Example | Mandatory  |
|------|--------------|-------|---------------|------------|
| type | The event name ("searchInfo")  | string | "searchInfo" | True |
| keywords | Array of the search keywords | array  | ["Reset password"] | false |

**Searched content SDE JSON example**:

```json
{
  "type": "searchInfo", //MANDATORY
  "keywords": ["Reset password"], //TERMS SEARCHED BY A VISITOR. FOR EXAMPLE: FAQ
  ABOUT RESET PASSWORD
}
```

#### Section

This Engagement Attribute is used to determine the appropriate Location for engaging with visitors, or to display where the visitors are browsing.

**Code example**:
```json
lpTag.section = [ //SET A LIST OF YOUR SITE SECTIONS
"electronics", //CAN BE A SECTION OR A SUB-SECTION
"user agreement faqs"
];
```
