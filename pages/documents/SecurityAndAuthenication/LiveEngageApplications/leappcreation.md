---
pagename: Installing LivePerson Applications
redirect_from:
  - guides-le-applications-installing.html
Keywords:
sitesection: Documents
categoryname: "Security & Authentication"
documentname: LivePerson Applications
order: 20
permalink: LivePerson-applications-installing-liveperson-applications.html
indicator: both
---

### Overview

In order to install a private application, you will need to upload a valid JSON schema. You can do this by navigating to the Applications area by clicking on the "puzzle" icon on the left hand menu in LiveEngage. Navigate to the "Private apps" tab by clicking on the "Private apps" button at the top left side of the Applications area. Then, click on the "ADD YOUR PRIVATE APP" box which will appear in the tab. Choose a valid JSON schema as detailed below to upload your application.

**Screenshot**

### Sample Schema

Below you will find a sample of a valid LivePerson Application schema, along with tables describing the different parameters, their usage, and accepted values.

```json
{
  "client_name": "My First LE-App",
  "description": "This is my first LE-App",
  "grant_types": [
    "client_credentials"
  ],
  "response_types": ["code"],
  "redirect_uris": ["https://www.myredirecturi.com"],
  "scope": "msg.consumer",
  "logo_uri": "/src/modules/campaigns/assets/img/software/Mobile-App.png",
  "quick_launch_enabled": true,
  "entry_uri": "https://myservice.mydomain.com/appentry",
  "enabled_for_profiles": [42, 43],
  "capabilities": {
    "webhooks": {
      "ms.MessagingEventNotification.ContentEvent": {
        "endpoint": "https://your/webhooks/endpoint",
        "max_retries": 3,
        "headers": [{"header_name": "NAME", "header_value": "VALUE"}]
      },
      "ms.MessagingEventNotification.RichContentEvent": {
        "endpoint": "https://your/webhooks/endpoint",
        "max_retries": 5,
        "headers": [{"header_name": "NAME", "header_value": "VALUE"}]
      },
      "ms.MessagingEventNotification.AcceptStatusEvent": {
        "endpoint": "https://your/webhooks/endpoint",
        "max_retries": 1
      },
      "ms.MessagingEventNotification.ChatStateEvent": {
        "endpoint": "https://your/webhooks/endpoint"
      },
      "cqm.ExConversationChangeNotification": {
        "endpoint": "https://your/webhooks/endpoint"
      }
    },
    "engagement": {
      "design_engagement": false,
      "design_window": false,
      "entry_point": [
        "section"
      ],
      "visitor_behavior": [
        "visited_location",
        "time_on_location",
        "flow",
        "engaged_in_session",
        "about_to_abandon",
        "cart_value",
        "cart_items",
        "visitor_error",
        "viewed_products",
        "service_activity"
      ],
      "target_audience": [
        "external_referral",
        "search_keywords",
        "ip",
        "platform",
        "geo_location",
        "returning_visitors",
        "marketing_source",
        "customer_type",
        "age",
        "balance",
        "customer_id",
        "gender",
        "store_zip_code",
        "store_number",
        "company_size",
        "registration_date"
      ],
      "goal": [
        "url",
        "purchase_total",
        "num_of_pages",
        "lead",
        "service_activity"
      ],
      "consumer_identity": [
        "auth"
      ],
      "language_selection": false
    }
  }
}
```

### LivePerson Application Manifest Schema - Parameters

| Property | Description | Type | Required| Notes|
|--- | --- | ---| ---| ---|
|client_name | Choose the name for your Connector application | string| Yes | Can be internationalized by adding 5646 language tag after hash chararcter. <br /> Max length: 128|
|description | App description | string | No| max length: 256|
|grant_types | Authorization grant according to OAuth 2.0 | array | No | supported values: "client_credentials"<br />"authorization_code"<br />"refresh_token"|
|redirect_uris | For web/native apps, the URIs to which the JWT/code will be sent after redirect | array of strings | No | max length: 128|
|response_types | OAuth 2.0 response type strings that the client can use at the authorization endpoint | array | No |supported values: "code"<br />"token"<br />"id_token"<br />"id_token token"|
|scope | Space-separated list of scope values that the client can use when requesting access tokens| string| No |supported values: "msg.consumer" <br /> max length: 128|
|logo_uri | URL string that references a logo for the client | string | No | logo size is must be exactly 70x70 pixels <br /> max length: 1024|
|capabilities| LivePerson capabilities utilized by this app. This array defines the various LivePerson services or applications that can interface with this application| object (See supported values structure in the tables below)| No | supported values: "webhooks", "engagement". <br /> <br /> webhooks: Contains the endpoints where UMS (Messaging Service) will send notifications <br /> <br />  engagement: This determines how the application interfaces with LivePerson engagements and their creation |
|enabled | Whether the application is enabled or not | boolean | No | default value: true |
|quick_launch_enabled | Whether the application should be displayed in the quicklaunch menu | boolean | No | default value: false |
|entry_uri | The URI to start the application | string | No | max length: 1024 |
|enabled_for_profiles | A list of profiles to which this application should be available | array of integers | No |  |

#### webhooks (optional object within capabilities object)

| Property | Description | Type | Required| Notes|
|--- | --- | ---| ---| ---|
|ms.MessagingEventNotification .ContentEvent | Indicates the HTTPS configuration endpoint of your server to receive notifications of type ContentEvent. | webhook | No | |
|ms.MessagingEventNotification .RichContentEvent |  Indicates the HTTPS configuration endpoint of your server to receive notifications of type RichContentEvent. | webhook | No | |
|ms.MessagingEventNotification .AcceptStatusEvent |Indicates the HTTPS configuration endpoint of your server to receive notifications of type AcceptStatusEvent. |  webhook | No | |
|ms.MessagingEventNotification .ChatStateEvent | Indicates the HTTPS configuration endpoint of your server to receive notifications of type ChatStateEvent. |  webhook | No | |
|ms.MessagingEventNotification .ExConversationChangeNotification | Indicates the HTTPS configuration endpoint of your server to receive notifications of type ExConversationChangeNotification. |  webhook | No | |

#### webhook (optional object within webhooks object)

| Property | Description | Type | Required| Notes|
|--- | --- | ---| --- | ---|
|endpoint | The url to send the notification to, including query parameters | string| Yes |Starts by "https://"|
|max_retries | The max number of retry attempts to send the notification if it fails | integer| No| minimum value: 0, maximum value: 5|
|headers | List of http headers to add to the notification request | array of headers | No| Example value:  [{"header_name": "NAME1", "header_value": "VALUE1"},{"header_name": "NAME2", "header_value": "VALUE2"}]|

#### engagements

| Property | Description | Type | Required| Notes|
|--- | --- | ---| ---| ---|
|design_engagement |Toggles the ability to design the engagement button and apparence | boolean |Yes | |
|design_window | Toggles the ability to add an engagement window | boolean | Yes | |
|entry_point |  Indicates where to display the engagement which invites consumers to engage with you | array| Yes | supported values: section, url|
|visitor_behavior | The browsing behavior of visitors which is of interest to you.  | array| Yes | supported values: visited_location, time_on_location, flow, engaged_in_session, about_to_abandon, cart_value, visitor_error, viewed_products, service_activity|
|target_audience | The visitors you specifically want to target |  string | Yes | supported values: external_referral, search_keywords, ip, platform, geo_location, returning_visitors, marketing_source, customer_type, age,balance, customer_id,gender, store_zip_code, store_number, company_size, registration_date |
|goal |  Indicates what you want to achieve with the engagement | string| Yes |supported values: url, purchase_total, num_of_pages, lead, service_activity |
|consumer_identity | If the consumer does or doesn't have to be an authenticated user |  array| Yes | The value has to be set to auth. supported values: auth, unauth|
|language_selection | Indicates the possibility of language selection  |  boolean |Yes ||

### Quicklaunch menu

Applications can be added to the QuickLaunch menu in the LivePerson UI. For applications to be available in the QuickLaunch menu, some criteria have to be met. In case of a Private LivePerson Application the JSON Manifest should contain the following properties:

* `"quick_launch_enabled" : true`,

* non-empty `entry_uri`,

* the user profile should match one of the profiles listed in `enabled_for_profiles`.
