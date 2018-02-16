# NeXus API documentation version v1

---

## /o/token
All NeXus APIs use token based security. You'll need the credentials you were provided to recieve your token. The detail below is the process for obtaining a token.

### /o/token

#### **POST**:
Authorization with client ID and secret

#### application/x-www-form-urlencoded (application/x-www-form-urlencoded) 

##### *application/x-www-form-urlencoded*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| client_id |  string | Client ID for authentication | true |  |
| client_secret |  string | Client secret, a hash token | true |  |
| grant_type |  string |  | true |  |
| scope |  string |  | true |  |

### Response code: 200

#### application/json (application/json) 

```
{
  "access_token": "60qJ8mC4NUFxKjBXFJF0XOb5UKtpJT",
  "token_type": "Bearer",
  "expires_in": 36000,
  "scope": "read"
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| access_token |  string |  | true |  |
| expires_in |  number |  | true |  |
| scope |  string |  | true |  |
| token_type |  string |  | true |  |

### Response code: 401

#### application/json (application/json) 

```
{
  "error_message": "Authentication credentials were not provided."
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| error_message |  string |  | true |  |

---

## /dispo/sample-accounts/

### /dispo/sample-accounts/

#### **GET**:
Get Sample account numbers

### Response code: 200

#### application/json (application/json) 

```
[
  {
    "account_number": 2123123123123253
  },
  {
    "account_number": 1234567891007852
  }
]
```

##### List of *items*:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| account_number |  integer |  | true |  |

### Response code: 401

#### application/json (application/json) 

```
{
  "error_message": "Authentication credentials were not provided."
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| error_message |  string |  | true |  |

---

## /arb/ebi-model-types-recommendations/

### /arb/ebi-model-types-recommendations/

#### **GET**:
Get Ebi Model types with recommendations

### Response code: 200

#### application/json (application/json) 

```
[
  {
    "id": 1,
    "type": "Behavior",
    "recommendations": [
      {
        "rec_name": "ALL_FSIK"
      },
      {
        "rec_name": "SUB_AUTOPAY"
      },
      {
        "rec_name": "SUB_CALL_ANYQUEUE"
      },
      {
        "rec_name": "SUB_NUDGE_VALUE"
      },
      {
        "rec_name": "SUB_SELF_SERVICE"
      },
      {
        "rec_name": "SUB_TRUCKROLL"
      }
    ]
  },
  {
    "id": 2,
    "type": "Retention",
    "recommendations": [
      {
        "rec_name": "SUB_CHURN_NPD"
      },
      {
        "rec_name": "SUB_CHURN_TOTAL"
      },
      {
        "rec_name": "SUB_DNG_X1"
      }
    ]
  }
]
```

##### List of *items*:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| id |  integer |  | true |  |
| type |  string |  | true |  |
| recommendations | items array |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| rec_name |  string |  | true |  |

### Response code: 401

#### application/json (application/json) 

```
{
  "error_message": "Authentication credentials were not provided."
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| error_message |  string |  | true |  |

---

## /iapi/get-ebi-recommendations/

### /iapi/get-ebi-recommendations/

#### **POST**:
Submit ebi arbitrate form and get recommendations

#### application/json (application/json) 

```
{
  "account_number": "8220204141109707",
  "house_key": " ",
  "model_type_id": [],
  "recs_requested": 4,
  "recs_by_model_type": true,
  "timestamp": "2018-01-18T11:53:24.334407"
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| account_number |  string |  | true |  |
| house_key |  string |  | false |  |
| model_type_id | items array |  | true |  |
| recs_by_model_type |  boolean |  | true |  |
| recs_requested |  integer |  | true |  |
| timestamp |  string |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| model_type_id |  integer |  | true |  |
| model_recommendations | items array |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| rec_name |  string |  | true |  |

### Response code: 200

#### application/json (application/json) 

```
{
  "recs_by_model_type": true,
  "recs_requested": 2,
  "recs_available": 8,
  "account_number": 8220204141109707,
  "timestamp": "2018-02-13T18:32:43.178537",
  "recommendations": [
    {
      "rec_name": "SUB_DNG_X1",
      "model_type_id": 2,
      "rec_label": "Likelihood of a customer to drop X1 product within the next 90 days",
      "priority": 1,
      "probability": "9.83%",
      "rec_id": "EBI_N16_01_002"
    },
    {
      "rec_name": "SUB_CHURN_TOTAL",
      "model_type_id": 2,
      "rec_label": "Likelihood of a customer to disconnect all service within the next 90 days. HELLO MY NAME IS KEVIN. HELLO MY NAME IS KEVIN. HELLO MY NAME IS KEVIN. HELLO MY NAME IS KEVIN",
      "priority": 2,
      "probability": "8.95%",
      "rec_id": "EBI_N16_06_018"
    },
    {
      "rec_name": "SUB_AUTOPAY",
      "model_type_id": 1,
      "rec_label": "The likelihood of a Comcast subscriber to enroll in AutoPay withwithin the next 90 days.",
      "priority": 1,
      "probability": "7.27%",
      "rec_id": "EBI_N16_04_009"
    },
    {
      "rec_name": "SUB_UPG_DOUBLEPLAY",
      "model_type_id": 3,
      "rec_label": "Likelihood of an existing single product customer to subscribe to Doubleplay (VIDEO/HSD, HSD/VIDEO) within the next 90 days.",
      "priority": 1,
      "probability": "6.31%",
      "rec_id": "EBI_N16_01_019"
    },
    {
      "rec_name": "SUB_UPG_XHOME",
      "model_type_id": 3,
      "rec_label": "Likelihood of a customer to add XFINITY Home (XH) within the next 90 days. HELLO MY NAME IS KEVIN",
      "priority": 2,
      "probability": "5.83%",
      "rec_id": "EBI_N16_12_003"
    },
    {
      "rec_name": "SUB_DELQ_30DAYS",
      "model_type_id": 4,
      "rec_label": "The likelihood of a customer to become delinquent in the next 30 days",
      "priority": 1,
      "probability": "1.21%",
      "rec_id": "EBI_N16_09_007"
    },
    {
      "rec_name": "SUB_TRUCKROLL",
      "model_type_id": 1,
      "rec_label": "Likelihood of a customer to request a truckroll service within the next 90 days.",
      "priority": 1,
      "probability": "0.97%",
      "rec_id": "EBI_N16_06_007"
    }
  ],
  "house_key": " "
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| account_number |  number |  | true |  |
| house_key |  string |  | true |  |
| recs_by_model_type |  boolean |  | true |  |
| recs_available |  integer |  | true |  |
| recs_requested |  integer |  | true |  |
| timestamp |  string |  | true |  |
| recommendations | items array |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| priority |  integer |  | true |  |
| model_type_id |  integer |  | true |  |
| rec_name |  string |  | true |  |
| rec_label |  string |  | true |  |
| rec_id |  string |  | true |  |
| probability |  string |  | true |  |

### Response code: 401

#### application/json (application/json) 

```
{
  "error_message": "Authentication credentials were not provided."
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| error_message |  string |  | true |  |

---

## /dispo/ebi-model-stats/

### /dispo/ebi-model-stats/

#### **GET**:
Get Ebi model statistics

### Response code: 200

#### application/json (application/json) 

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| iapirequests | items array |  | true |  |
| ebi_rec | items array |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| sucessful_req_cnt |  number |  | true |  |
| failed_req_cnt |  integer |  | true |  |
| invalid_req_cnt |  integer |  | true |  |
| month |  integer |  | true |  |
| year |  integer |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| rec_name |  string |  | true |  |
| delivered_count |  number |  | true |  |
| month |  number |  | true |  |
| year |  number |  | true |  |

### Response code: 401

#### application/json (application/json) 

```
{
  "error_message": "Authentication credentials were not provided."
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| error_message |  string |  | true |  |

---

## /iapi/get-event-types/

### /iapi/get-event-types/

#### **GET**:
Get Event types for an account number

### Response code: 200

#### application/json (application/json) 

```
{
  "timeline_response": [
    {
      "incidence_source": "WorkOrder",
      "timestamp": "02-07-2018 12:48 AM",
      "csr_desc": "A notification event log",
      "event_type": "Cancel",
      "recommendations": [],
      "event_id": "a6c237b2-f4fb-4b23-98cb-8f4a61b9a0e5"
    },
    {
      "incidence_source": "IVR",
      "timestamp": "02-07-2018 12:44 AM",
      "csr_desc": "Customer was in the billing section of the IVR before transferred.",
      "event_type": "Billing Question",
      "recommendations": [
        {
          "rec_label": "Remind the customer that we offer convenient self-service options to manage their bill. For more details you can share the article below:",
          "rec_uri": "http://einstein.cable.comcast.com/Einstein/ViewDocument/HOW9095",
          "rec_id": "Not Available"
        }
      ],
      "event_id": "f5e18338-fd38-4cb0-9f24-7dd6f878de1b"
    }
  ],
  "total_events": 13,
  "total_recs": 2
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| timeline_response | items array |  | true |  |
| total_events |  integer |  | true |  |
| total_recs |  integer |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| incidence_source |  string |  | true |  |
| timestamp |  string |  | true |  |
| csr_desc |  string |  | true |  |
| event_type |  string |  | true |  |
| recommendations | items array |  | true |  |
| event_id |  string |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| rec_label |  string |  | true |  |
| rec_uri |  string |  | true |  |
| rec_id |  string |  | true |  |

### Response code: 401

#### application/json (application/json) 

```
{
  "error_message": "Authentication credentials were not provided."
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| error_message |  string |  | true |  |

---

## /iapi/get-recommendations/

### /iapi/get-recommendations/

#### **POST**:
Submit nexus-workbench arbitrate form and get recommendations

#### application/json (application/json) 

```
{
  "account_number": 8495753104400717,
  "events": [
    {
      "event_id": "678234e3-afe1-4da8-a1ca-a70a4e0f282f",
      "event_type": "Unknown",
      "incidence_source": "",
      "csr_desc": "",
      "recommendations": [
        {
          "rec_label": "",
          "csr_desc": "",
          "event_type": "",
          "rec_uri": "",
          "rec_id": ""
        }
      ]
    }
  ],
  "recs_requested": 2,
  "recs_by_event_type": false,
  "timestamp": "1510191809043"
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| account_number |  number |  | true |  |
| recs_requested |  number |  | true |  |
| recs_by_event_type |  boolean |  | true |  |
| timestamp |  string |  | true |  |
| events | items array |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| event_id |  string |  | true |  |
| event_type |  string |  | true |  |
| incidence_source |  string |  | true |  |
| csr_desc |  string |  | true |  |
| recommendations | items array |  | false |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| rec_label |  string |  | true |  |
| csr_desc |  string |  | true |  |
| event_type |  string |  | true |  |
| rec_uri |  string |  | true |  |
| rec_id |  string |  | true |  |

### Response code: 200

#### application/json (application/json) 

```
{
  "account_number": 8495753104400717,
  "recs_requested": 2,
  "recommendations": [
    {
      "rec_label": "Remind the customer that we offer convenient self-service options to make and manage payments. For more details you can share the article below:",
      "csr_desc": "Customer has a question about payments",
      "priority": 1,
      "event_type": "Payment General",
      "rec_uri": "http://einstein.cable.comcast.com/Einstein/ViewDocument/HOW9095",
      "rec_id": "90529780090957"
    },
    {
      "rec_label": "Remind the customer that we offer convenient self-service options to manage their bill. For more details you can share the article below:",
      "csr_desc": "Customer has a billing question",
      "priority": 2,
      "event_type": "Billing Question",
      "rec_uri": "http://einstein.cable.comcast.com/Einstein/ViewDocument/HOW9095",
      "rec_id": "3b77e1f0e54b48"
    }
  ],
  "timestamp": "2018-02-15T17:31:24.235015",
  "error": ""
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| account_number |  number |  | true |  |
| recs_requested |  number |  | true |  |
| recommendations | items array |  | true |  |
| timestamp |  string |  | true |  |
| error |  string |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| rec_label |  string |  | true |  |
| priority |  number |  | true |  |
| csr_desc |  string |  | true |  |
| event_type |  string |  | true |  |
| rec_uri |  string |  | true |  |
| rec_id |  string |  | true |  |

### Response code: 401

#### application/json (application/json) 

```
{
  "error_message": "Authentication credentials were not provided."
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| error_message |  string |  | true |  |

---

## /dispo/sc-stats/

### /dispo/sc-stats/

#### **GET**:
Get Smart Connect events Statistics

### Response code: 200

#### application/json (application/json) 

```
{
  "average-recommendation-delivery": [
    {
      "event-type": "Unknown",
      "delivery_percentage": 0
    },
    {
      "event-type": "Video Connection",
      "delivery_percentage": 0
    }
  ],
  "top-rgu": [
    {
      "count": 4380090,
      "rgu": "VIDEO/HSD/CDV"
    },
    {
      "count": 2880085,
      "rgu": "VIDEO/HSD/CDV/XH"
    }
  ],
  "top-event-types": [
    {
      "count": 810927,
      "event-type": "Unknown"
    },
    {
      "count": 552437,
      "event-type": "Video Connection"
    }
  ],
  "event-types-with-recommendations": [
    {
      "count": 169832,
      "event-type": "Payment General"
    },
    {
      "count": 166266,
      "event-type": "Autopay"
    }
  ],
  "event-types-without-recommendations": [
    {
      "count": 169832,
      "event-type": "Payment General"
    }
  ],
  "recommendations-per-event-type": [
    {
      "count": 810927,
      "event-type": "Unknown"
    },
    {
      "count": 552437,
      "event-type": "Video Connection"
    }
  ],
  "top-current-product-mix": [
    {
      "count": 4384795,
      "product-mix": "Video/HSD"
    }
  ],
  "top-recommendations": [
    {
      "count": 3401327,
      "recommendation": ""
    }
  ]
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| average-recommendation-delivery | items array |  | true |  |
| top-rgu | items array |  | true |  |
| top-event-types | items array |  | true |  |
| event-types-with-recommendations | items array |  | true |  |
| event-types-without-recommendations | items array |  | true |  |
| recommendations-per-event-type | items array |  | true |  |
| top-current-product-mix | items array |  | true |  |
| top-recommendations | items array |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| event-type |  string |  | true |  |
| delivery_percentage |  number |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| count |  number |  | true |  |
| rgu |  string |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| count |  number |  | true |  |
| event-type |  string |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| count |  number |  | true |  |
| event-type |  string |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| count |  number |  | true |  |
| event-type |  string |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| count |  number |  | true |  |
| event-type |  string |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| count |  number |  | true |  |
| product-mix |  string |  | true |  |

items:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| count |  number |  | true |  |
| recommendation |  string |  | true |  |

### Response code: 401

#### application/json (application/json) 

```
{
  "error_message": "Authentication credentials were not provided."
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| error_message |  string |  | true |  |

---

## /dispo/arbagg/

### /dispo/arbagg/

#### **GET**:
Get the nexus-workbench Arbitration DB snapshot.

### Response code: 200

#### application/json (application/json) 

```
[
  {
    "id": 26,
    "recommendation_id": "0672067851ab87",
    "recommendation_uri": "https://einstein360.cable.comcast.com/Einstein360/ViewDocument/TLK3305",
    "recommendation": "Technical Device Swap - Talking Points",
    "event_type": "Equipment Swap",
    "csr_description": "Customer Needs to Swap Existing Equipment - New Device Was Shipped To Them",
    "p_fix": "90.62"
  },
  {
    "id": 38,
    "recommendation_id": "9b8c4e145cbac9",
    "recommendation_uri": "https://einstein360.cable.comcast.com/einstein360/ViewDocument/HOW3274",
    "recommendation": "How to Set Up Automatic Payments - My Account Help",
    "event_type": "Autopay",
    "csr_description": "Offer to enroll in Auto-Pay",
    "p_fix": "90"
  }
]
```

##### List of *items*:

| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| id |  number |  | false |  |
| recommendation_id |  string |  | true |  |
| recommendation_uri |  string |  | true |  |
| recommendation |  string |  | true |  |
| event_type |  string |  | true |  |
| csr_description |  string |  | true |  |
| p_fix |  string |  | true |  |

### Response code: 401

#### application/json (application/json) 

```
{
  "error_message": "Authentication credentials were not provided."
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| error_message |  string |  | true |  |

---

## /atam/update-recommendation-disposition/

### /atam/update-recommendation-disposition/

#### **POST**:
Update the probability of fix in the Arbitration DB snapshot in nexus-workbench

#### application/json (application/json) 

```
{
  "account_number": 8299420184043530,
  "event_type": "Autopay",
  "rec_id": "9b8c4e145cbac9",
  "disposition": true,
  "dispo_timestamp": "2017-12-13T02:19:11.647365"
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| account_number |  number |  | true |  |
| event_type |  string |  | true |  |
| rec_id |  string |  | true |  |
| disposition |  boolean |  | true |  |
| dispo_timestamp |  string |  | true |  |

### Response code: 200

#### application/json (application/json) 

```
{
  "response_message": "Arb Disposition successful"
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| response_message |  string |  | true |  |

### Response code: 401

#### application/json (application/json) 

```
{
  "error_message": "Authentication credentials were not provided."
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| error_message |  string |  | true |  |

---

## /ajax-login
All NeXus APIs use token based security. You'll need the credentials you were provided to recieve your token. The detail below outlines the process for obtaining a token.

### /ajax-login

#### **POST**:
Authorization with client ID and secret

#### application/x-www-form-urlencoded (application/x-www-form-urlencoded) 

##### *application/x-www-form-urlencoded*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|

### Response code: 200

#### application/json (application/json) 

```
{
  "access_token": "60qJ8mC4NUFxKjBXFJF0XOb5UKtpJT"
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| access_token |  string |  | true |  |

### Response code: 401

#### application/json (application/json) 

```
{
  "error_message": "Authentication credentials were not provided."
}
```

##### *application/json*:
| Name | Type | Description | Required | Pattern |
|:-----|:----:|:------------|:--------:|--------:|
| error_message |  string |  | true |  |

---

