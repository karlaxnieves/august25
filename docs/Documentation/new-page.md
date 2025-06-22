---
title: new page
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: test
  description: testing
  image: https://files.readme.io/25ff87b-IMG_5887.jpeg
  robots: noindex
next:
  description: ''
---
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c15fc85-Income_1.png",
        "Income (1).png",
        1288
      ],
      "align": "center",
      "sizing": "80"
    }
  ]
}
[/block]



## Overview

Okra’s Income API calculates an end user’s income using real-time financial transactions from their bank accounts. At the core of the Income API is the Okra NLU (_Natural Language System_), which incorporates online machine learning and active learning to provide data for your business needs.

Whether it’s a day laborer earnings, salary, pension, or an uncle who provides monthly aid, Okra makes it easy to understand the structured and unstructured income sources of your user. This provides a wealth of opportunity in KYC validation, enabling critical eligibility information like employment verification, spending patterns, and credit power.

Understanding your customer's income history enables you to speed up your decision-making process. Okra's API provides accurate and extensive income data for many use cases, including disbursement amounts, product recommendations, payment tenures, and more.

***



## How it works

Once your user grants Okra permission to access their bank accounts, Okra services pull transactions and feed them into the Okra NLU. The NLU extracts income-related data such as Named Entities, Transaction frequency, and Transaction dates.

![](https://files.readme.io/90d3a0e-income-v2-flow-bold.png)

The NLU system analyzes and groups income data based on details such as:

- **Named Entities**: Named Entities are special keywords and sub-text identified in the transaction descriptions. These entities include _transaction beneficiary_, _utility keywords, reference codes, transaction narration_, _transaction channel,_ and _income-related_ keywords.
- **Transaction Groups**: Transactions can belong to any of these seven categories: VAT, Commissions, ATM/POS, Transfer, Deposits, Returns on Investments, and Reversals.
- **Transaction Frequency**: The API also groups similar transactions together based on their rate of recurrence.

The Income Engine uses these data groups to accurately identify income streams, and group transactions that belong to the same income stream together. Okra sorts income streams into these categories:

#### Salary

Salaries are sums of money that registered Nigerian companies transfer to your user’s account. Salary-related keywords and Named Entities that belong to registered Nigerian companies are strong indications of salary-related transactions. The Income API then processes this monthly numeric credit inflow as income.

#### Recurrent Credit

Fixed sums of money periodically credited into your user's account. Recurrent credit can come from passive returns from investments and businesses or as a steady inflow from a third-party sender. These transfers can occur monthly, quarterly, or yearly.

#### Recurrent Deposit

Similarly to recurrent credit, recurrent deposits are sums of money periodically paid into your user’s account. Recurrent deposit mainly comes from cash deposits or checks, while recurrent credit comes from USSD or Internet Transfers.

#### Unstructured Income

The Income API classifies income on accounts that do not have a fixed amount of recurring inflow as unstructured income. The market structure in Nigeria accounts for this type of income: small business owners, gig economy workers, and SME proprietors usually belong to this category.

***



## How to use

Okra recommends that you leverage the Income API in this order:

1. Use the [**`process` income**](https://docs.okra.ng/reference/processincome) operation for first-time users 

This operation analyzes the income data of a first-time user and returns a processed income profile. This process usually takes a few seconds - the duration depends on the depth of the user’s transaction history, and the number of income streams.

2. Use the **`get` income** operations based on your business needs

These operations enable you to retrieve already processed income data faster. Power your application by retrieving data based on [**ID**](https://docs.okra.ng/reference/getincomebyid), [**customer**](https://docs.okra.ng/reference/getincomebycustomer), [**date**](https://docs.okra.ng/reference/getincomebydate), [**record**](https://docs.okra.ng/reference/getbyrecord), or by retrieving [**all your users’ income data**](https://docs.okra.ng/reference/getallincomes) in a single request.

***



## Key features of the Income API

### Trailing Income History

The trailing history gives a historical summary of each income stream using 3, 6, and 12 months’ chunks of transactions that the Income Engine refers to as _history blocks_. The Income Engine calculates the maximum credit amount, average monthly amount, total sum, minimum monthly amount, and count of an income stream in each _history block_. 

These _history blocks_ provide insight into how your users' income streams change over time.

### Stream Ranking

Using a proprietary algorithm, the Stream Engine ranks the different streams of income in their order of importance. Each stream of income is weighted based on its contribution to the overall income value of your user. 

This helps you identify your user’s primary stream of income.

### Evaluating the Income Model

Your user’s income model is evaluated using a _confidence score_. The NLU uses a confidence score to indicate an estimated level of accuracy in classifying transaction data as income. By extension, the confidence score also indicates the correctness of the projected income sums and the trailing history figures.

As with most machine learning models, the NLU uses accuracy, recall, and precision to evaluate the performance of the system by deriving values from a confusion matrix:

![](https://files.readme.io/49a3889-confusion_matrix.png)

- **TP**: True positive - the number of income transactions in a stream correctly identified as income transactions
- **FN**: False negative - the number of actual income transactions in a stream classified incorrectly as non-income transactions
- **FP:** False positive - the number of non-income transactions in a stream classified incorrectly as income transactions
- **TN:** True negative - the number of non-income transactions in a stream correctly identified as non-income transactions

> 📘 
> 
> The confidence score is the total number of correctly classified income and non-income transactions expressed as a percentage:
> 
> **Confidence Score** **=** **(TP + TN) / (TP + TN + FP + FN) \* 100**

***



## Attributes of the `income` object

An `income` object can contain these attributes:

| Attribute       | Type             | Description                                                                                                                                                                                                                                 |
| :-------------- | :--------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `confidence`    | float            | Indicates an estimated level of accuracy in classifying transaction data as income.                                                                                                                                                         |
| `summary`       | array of objects | Contains an overview of the income calculations. It includes summaries such as the number of streams, the projected sums, the sums from the previous year, and the histories (3, 6, and 12 month history blocks) for all streams of income. |
| `streams`       | array of objects | Lists the identified streams of income ranked in order of importance using the Stream Ranking algorithm. Income streams with lower ranks are returned in the `other_streams` array of objects.                                              |
| `other_streams` | array of objects | Lists the identified streams of income that are deemed less important. Has the same underlying objects as `streams`.                                                                                                                        |
| `transactions`  | array of objects | Lists the transactions that are used to calculate the different income streams.                                                                                                                                                             |

#### Attributes within `summary`

| Attribute                                      | Type    | Description                                                                                                                                                                                                                                                              |
| ---------------------------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `account_age_months`                           | integer | Indicates how long the user has been using this bank account. The value is estimated from the length and timestamps of transactions.                                                                                                                                     |
| `average_monthly_income`                       | float   | Indicates the average amount earned by the user in one month. The value is calculated as the average monthly amount of all the identified streams of income.                                                                                                             |
| `current_year`                                 | string  | The calendar year for which the income data was requested in `YYYY` format. The current calendar year is the default value. This value can be changed through the request object.                                                                                        |
| `last_two_years_income`                        | float   | Indicates the total income from two years ago. For example, if `current_year` is 2022, this value indicates the total income from the year 2020.                                                                                                                         |
| `last_two_years_to_this_year_projected_income` | float   | Indicates a total projected income using figures from the `current_year`, the previous year, and the calendar year 2 years back. For example, if `current_year` is 2022, this value uses figures from 2020, 2021, and 2022 to provide a more realistic projected income. |
| `last_year_income`                             | float   | Indicates the total income from last year. For example, if `current_year` is 2022, this value indicates the total income from the year 2021.                                                                                                                             |
| `last_year_to_this_year_projected_income`      | float   | Indicates a total projected income using figures from the `current_year` and the previous year. For example, if `current_year` is 2022, this value uses figures from 2021 and 2022 to provide a more realistic projected income.                                         |
| `number_of_streams`                            | integer | Indicates the number of identified income streams.                                                                                                                                                                                                                       |
| `past_three_months`                            | object  | Contains the summary of all income streams of the past 3 months.                                                                                                                                                                                                         |
| `past_six_months`                              | object  | Contains the summary of all income streams of the past 6 months.                                                                                                                                                                                                         |
| `past_twelve_months`                           | object  | Contains the summary of all income streams of the past 12 months.                                                                                                                                                                                                        |
| `primary_stream_age_months`                    | integer | Indicates the number of months the primary income stream has existed on a specific account. This value provides an estimate of how long a user has been earning income from that income stream.                                                                          |
| `this_year_projected_sum`                      | float   | Indicates the total income that the user is estimated to make by the end of the current calendar year. The value is calculated using the _monthly_income_, _number_of_months_, and _projected_months_ of each income stream.                                             |

##### Attributes for past income data in the `summary` object

The objects `past_three_months`, `past_six_months`, and `past_twelve_months` contain these attributes. Each object returns data that corresponds to a specific period of time, which is shown in the object’s name.

| Attribute           | Type  | Description                                                                        |
| ------------------- | ----- | ---------------------------------------------------------------------------------- |
| `average_per_month` | float | Indicates the average monthly income which is calculated using all income streams. |
| `max_per_month`     | float | Shows the highest identified income value from all streams.                        |
| `min_per_month`     | float | Shows the lowest identified income value from all streams.                         |
| `total`             | float | Indicates the total monthly sum of all income streams.                             |

#### Objects within `streams`

| Attribute | Type   | Description                                       |
| --------- | ------ | ------------------------------------------------- |
| `details` | object | Lists the details of each income stream.          |
| `history` | object | Lists the trailing history of each income stream. |

##### Attributes within `details`

| Attribute                | Type        | Description                                                                                                                                                                                                                                                                                                                |
| ------------------------ | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `account`                | string      | The bank account in which the stream was identified.                                                                                                                                                                                                                                                                       |
| `bank`                   | object      | The name or ID of the bank that holds the user’s account.                                                                                                                                                                                                                                                                  |
| `source`                 | object      | Provides details about user's source of income as identified by the Named Entity Recognition (NER).                                                                                                                                                                                                                        |
| `monthly_amount`         | float       | The amount of income generated on a monthly basis by this income stream.                                                                                                                                                                                                                                                   |
| `number_of_transactions` | integer     | The number of transactions that are part of this income stream.                                                                                                                                                                                                                                                            |
| `occurrence`             | object      | Lists details about dates, actual and projected occurrences, and total number of income transactions for this income stream.                                                                                                                                                                                               |
| `primary_stream`         | boolean     | Indicates whether the current stream is the primary source of income.                                                                                                                                                                                                                                                      |
| `stream_id`              | string uuid | A unique identifier for this income stream.                                                                                                                                                                                                                                                                                |
| `stream_rank`            | float       | Indicates a relative rank of an income stream with respect to the other streams. The highest value is 1.0, while the lowest is 0.0. The stream with the highest value is designated as the primary stream. stream_rank is calculated using weighted attributes such as total amounts of income, and number of occurrences. |
| `type`                   | string      | Indicates the type of income. Possible values: `salary`, `recurrent credit`, `recurrent deposit`, `rent`, `unstructured`.                                                                                                                                                                                                  |
| `working_days_this_year` | integer     | Indicates the number of working days this year for which the income stream was made.                                                                                                                                                                                                                                       |

###### Attributes within `source`

| Attribute | Type   | Description                                                                                                                                                                     |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `type`    | string | Identifies the type of an income source. For example, when the income stream type is `salary`, the `source.type` is shown as `employer`. Possible values: `employer`, `others`. |
| `name`    | string | Names the source of the income stream as identified by the Named Entity Recognition system (NER), which is part of the Okra NLU system.                                         |

##### Attributes within `occurrence`

Lists details about dates, actual and projected occurrences, and total number of income transactions for this income stream:

| Attribute                        | Type      | Description                                                                                                      |
| -------------------------------- | --------- | ---------------------------------------------------------------------------------------------------------------- |
| `first_date`                     | timestamp | Indicates the date when the income stream was first identified. The timestamp value follows the ISO 8601 format. |
| `last_date`                      | timestamp | Indicates the date when the income stream was last identified. The timestamp value follows the ISO 8601 format.  |
| `occurrence_this_year`           | integer   | The number of months when the income stream has occurred in the current year.                                    |
| `projected_occurrence_this_year` | integer   | Indicates the number of months the income stream is projected to occur in the current year.                      |
| `total_count`                    | integer   | Indicates the total number of months the income has already occurred.                                            |

#### Objects within `history`

These objects provide the trailing history of each income stream:

| Attribute            | Type   | Description                                                     |
| -------------------- | ------ | --------------------------------------------------------------- |
| `past_three_months`  | object | Contains a summary of the income stream for the past 3 months.  |
| `past_six_months`    | object | Contains a summary of the income stream for the past 6 months.  |
| `past_twelve_months` | object | Contains a summary of the income stream for the past 12 months. |

##### Attributes for past income data in `history`

The objects `past_three_months`, `past_six_months`, and `past_twelve_months` contain these attributes. Each object returns data that corresponds to a specific period of time, which is shown in the object’s name.

| Attribute           | Type  | Description                                                                              |
| ------------------- | ----- | ---------------------------------------------------------------------------------------- |
| `average_per_month` | float | Indicates the average monthly income which is calculated using all income streams.       |
| `max_per_month`     | float | Shows the highest identified income value from all streams.                              |
| `min_per_month`     | float | Shows the lowest identified income value from all streams.                               |
| `occurrence`        | float | Indicates the number of times this income stream has occurred in a given period of time. |
| `total`             | float | Indicates the total monthly sum of all income streams.                                   |

#### Attributes within `transactions`

| Attribute    | Type             | Description                                                                                                                                                  |
| ------------ | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `id`         | string uuid      | The unique transaction ID.                                                                                                                                   |
| `stream_ids` | array of strings | Lists the UUID of the income stream where a transaction belongs to.                                                                                          |
| `term`       | string           | Defines which history block a transaction within an income stream belongs to. Possible values: `past_three_months`, `past_six_months`, `past_twelve_months`. |

> 📘 
> 
> `term` helps pinpoint which 3, 6, or 12 months’ chunk of transactions, or history block does a transaction belong to. Transactions within the `past_tree_months` term are a subset of transactions within `past_six_months`, which in turn are a subset of `past_twelve_months`.

## Sample objects

```curl Request Sample
curl -X POST https://api.okra.ng/api/v2/income/getById
-H 'Content-Type: application/json' 
-H 'Authorization: Bearer <secretKey>'
-d '{id: xxxxxxxxxxxxx}'
```
```json Response Sample
{
        "income":{
            "_id":"1357e608c067dcd068014c85",
            "customer":{
                "_id":"1142188c965e0d0318fa4e44",
                "name":"User name"
            },
            "__v":0,
            "confidence":96.82,
            "created_at":"2022-10-25T13:35:04.691Z",
            "env":"production",
            "last_updated":"2022-11-02T15:17:26.643Z",
            "number_of_transactions":323,
            "other_streams":[
                "1357e608c067dcd068014c4b"
            ],
            "owner":[
                "5da6358130a943486f33dced"
            ],
            "projects":[
                "5ff62b99aea7a57a5c3baa01"
            ],
            "record":[
                "1357e5fd9fd44f0157940283",
                "135919279fd44f0157947c8a",
                "135fb2f9ccfaaa01a964abcf",
                "136242ca63712c2497b11f54",
                "136289fa63712c2497b1890e"
            ],
            "streams":[
                {
                    "stream_id":"1142188b965e0d0318fa4e43-1",
                    "__v":0,
                    "account":[
                        "1142188b965e0d0318fa4e43"
                    ],
                    "bank":[
                        {
                            "_id":"1d6fe57a4099cc4b210bbebc",
                            "name":"Bank name",
                            "colors":{
                                "primary":"#990D81",
                                "accent":"#990D81",
                                "bg":"#990D81",
                                "button":"#880972"
                            },
                            "logo":"Bank logo URL",
                            "icon":"Bank icon URL"
                        }
                    ],
                    "created_at":"2022-10-25T13:35:04.643Z",
                    "history":{
                        "past_six_months":{
                            "average_per_month":36585.96,
                            "max_per_month":27000,
                            "min_per_month":1.88,
                            "occurrence":6,
                            "total":219515.76
                        },
                        "past_three_months":{
                            "average_per_month":33916.59,
                            "max_per_month":20698,
                            "min_per_month":1.88,
                            "occurrence":3,
                            "total":101749.76
                        },
                        "past_twelve_months":{
                            "average_per_month":20742.98,
                            "max_per_month":27000,
                            "min_per_month":1.88,
                            "occurrence":12,
                            "total":248915.76
                        }
                    },
                    "last_updated":"2022-11-02T15:17:26.595Z",
                    "monthly_amount":300990.64,
                    "number_of_transactions":3,
                    "occurrence":{
                        "first_date":"2020-07-15T00:00:00.000Z",
                        "last_date":"2021-09-20T00:00:00.000Z",
                        "occurrence_this_year":0,
                        "projected_occurrence_this_year":0,
                        "total_count":15
                    },
                    "primary_stream":true,
                    "source":{
                        "name":"Multiple Sources",
                        "type":"other"
                    },
                    "stream_rank":0.9999999999999998,
                    "type":"Unstructured",
                    "working_days_this_year":0
                },
                {
                    "stream_id":"1142188b965e0d0318fa4e43-2",
                    "__v":0,
                    "account":[
                        "1142188b965e0d0318fa4e43"
                    ],
                    "bank":[
                        {
                            "name":"Bank name",
                            "colors":{
                                "primary":"#990D81",
                                "accent":"#990D81",
                                "bg":"#990D81",
                                "button":"#880972"
                            },
                            "logo":"Bank logo URL",
                            "icon":"Bank icon URL"
                        }
                    ],
                    "created_at":"2022-10-25T13:35:04.643Z",
                    "history":{
                        "past_six_months":{
                            "average_per_month":40000,
                            "max_per_month":70000,
                            "min_per_month":10000,
                            "occurrence":4,
                            "total":160000
                        },
                        "past_three_months":{
                            "average_per_month":160000,
                            "max_per_month":70000,
                            "min_per_month":10000,
                            "occurrence":1,
                            "total":160000
                        },
                        "past_twelve_months":{
                            "average_per_month":50000,
                            "max_per_month":70000,
                            "min_per_month":10000,
                            "occurrence":6,
                            "total":300000
                        }
                    },
                    "last_updated":"2022-11-02T15:17:26.595Z",
                    "monthly_amount":150000,
                    "number_of_transactions":8,
                    "occurrence":{
                        "first_date":"2021-02-15T00:00:00.000Z",
                        "last_date":"2021-07-15T00:00:00.000Z",
                        "occurrence_this_year":0,
                        "projected_occurrence_this_year":0,
                        "total_count":6
                    },
                    "source":{
                        "name":"User name",
                        "type":"other"
                    },
                    "stream_rank":0.8131059981494424,
                    "type":"Recurrent Credit",
                    "working_days_this_year":0
                },
                {
                    "stream_id":"1142188b965e0d0318fa4e43-3",
                    "__v":0,
                    "account":[
                        "1142188b965e0d0318fa4e43"
                    ],
                    "bank":[
                        {
                            "name":"Bank name",
                            "colors":{
                                "primary":"#990D81",
                                "accent":"#990D81",
                                "bg":"#990D81",
                                "button":"#880972"
                            },
                            "logo":"Bank logo URL",
                            "icon":"Bank icon URL"
                        }
                    ],
                    "created_at":"2022-10-25T13:35:04.643Z",
                    "history":{
                        "past_six_months":{
                            "_id":"13628a0663712c2497b1892c",
                            "average_per_month":11692,
                            "max_per_month":12000,
                            "min_per_month":30,
                            "occurrence":5,
                            "total":58460
                        },
                        "past_three_months":{
                            "_id":"13628a0663712c2497b1892b",
                            "average_per_month":13230,
                            "max_per_month":6000,
                            "min_per_month":30,
                            "occurrence":2,
                            "total":26460
                        },
                        "past_twelve_months":{
                            "_id":"13628a0663712c2497b1892a",
                            "average_per_month":29922.86,
                            "max_per_month":23300,
                            "min_per_month":30,
                            "occurrence":7,
                            "total":209460
                        }
                    },
                    "last_updated":"2022-11-02T15:17:26.595Z",
                    "monthly_amount":34910,
                    "number_of_transactions":44,
                    "occurrence":{
                        "first_date":"2021-02-15T00:00:00.000Z",
                        "last_date":"2021-08-04T00:00:00.000Z",
                        "occurrence_this_year":0,
                        "projected_occurrence_this_year":0,
                        "total_count":7
                    },
                    "source":{
                        "name":"User name",
                        "type":"other"
                    },
                    "stream_rank":0.6944853796438775,
                    "type":"Recurrent Credit",
                    "working_days_this_year":0
                },
                {
                    "stream_id":"1142188b965e0d0318fa4e43-4",
                    "__v":0,
                    "account":[
                        "1142188b965e0d0318fa4e43"
                    ],
                    "bank":[
                        {
                            "name":"Bank name",
                            "colors":{
                                "primary":"#990D81",
                                "accent":"#990D81",
                                "bg":"#990D81",
                                "button":"#880972"
                            },
                            "logo":"Bank logo URL",
                            "icon":"Bank icon URL"
                        }
                    ],
                    "created_at":"2022-10-26T11:25:39.624Z",
                    "history":{
                        "past_six_months":{
                            "average_per_month":66000,
                            "max_per_month":33000,
                            "min_per_month":33000,
                            "occurrence":1,
                            "total":66000
                        },
                        "past_three_months":{
                            "average_per_month":66000,
                            "max_per_month":33000,
                            "min_per_month":33000,
                            "occurrence":1,
                            "total":66000
                        },
                        "past_twelve_months":{
                            "average_per_month":66000,
                            "max_per_month":33000,
                            "min_per_month":33000,
                            "occurrence":1,
                            "total":66000
                        }
                    },
                    "last_updated":"2022-11-02T15:17:26.595Z",
                    "monthly_amount":66000,
                    "number_of_transactions":2,
                    "occurrence":{
                        "first_date":"2021-09-14T00:00:00.000Z",
                        "last_date":"2021-09-14T00:00:00.000Z",
                        "occurrence_this_year":0,
                        "projected_occurrence_this_year":0,
                        "total_count":1
                    },
                    "source":{
                        "name":"User name",
                        "type":"other"
                    },
                    "stream_rank":0.590443853272314,
                    "type":"Recurrent Credit",
                    "working_days_this_year":0
                },
                {
                    "stream_id":"1142188b965e0d0318fa4e43-5",
                    "__v":0,
                    "account":[
                        "1142188b965e0d0318fa4e43"
                    ],
                    "bank":[
                        {
                            "name":"Bank name",
                            "colors":{
                                "primary":"#990D81",
                                "accent":"#990D81",
                                "bg":"#990D81",
                                "button":"#880972"
                            },
                            "logo":"Bank logo URL",
                            "icon":"Bank icon URL"
                        }
                    ],
                    "created_at":"2022-10-26T11:25:39.624Z",
                    "history":{
                        "past_six_months":{
                            "average_per_month":27800,
                            "max_per_month":13000,
                            "min_per_month":100,
                            "occurrence":2,
                            "total":55600
                        },
                        "past_three_months":{
                            "average_per_month":27800,
                            "max_per_month":13000,
                            "min_per_month":100,
                            "occurrence":2,
                            "total":55600
                        },
                        "past_twelve_months":{
                            "average_per_month":27800,
                            "max_per_month":13000,
                            "min_per_month":100,
                            "occurrence":2,
                            "total":55600
                        }
                    },
                    "last_updated":"2022-11-02T15:17:26.595Z",
                    "monthly_amount":27800,
                    "number_of_transactions":10,
                    "occurrence":{
                        "first_date":"2021-08-09T00:00:00.000Z",
                        "last_date":"2021-09-14T00:00:00.000Z",
                        "occurrence_this_year":0,
                        "projected_occurrence_this_year":0,
                        "total_count":2
                    },
                    "source":{
                        "name":"User name",
                        "type":"other"
                    },
                    "stream_rank":0.4415437636637305,
                    "type":"Recurrent Credit",
                    "working_days_this_year":0
                }
            ],
            "summary":{
                "account_age_months":15,
                "average_monthly_income":115940.13,
                "current_year":2022,
                "last_two_years_income":8583323.14,
                "last_two_years_to_this_year_projected_income":5722215.43,
                "last_year_income":8583323.14,
                "last_year_to_this_year_projected_income":4291661.57,
                "number_of_streams":5,
                "past_six_months":{
                    "average_per_month":31087.54,
                    "max_per_month":70000,
                    "min_per_month":1.88,
                    "occurrence":18,
                    "total":559575.76
                },
                "past_three_months":{
                    "average_per_month":45534.42,
                    "max_per_month":70000,
                    "min_per_month":1.88,
                    "occurrence":9,
                    "total":409809.76
                },
                "past_twelve_months":{
                    "average_per_month":31427.71,
                    "max_per_month":70000,
                    "min_per_month":1.88,
                    "occurrence":28,
                    "total":879975.76
                },
                "primary_stream_age_months":15,
                "this_year_projected_sum":0
            },
            "transactions":[
                {
                    "stream_ids":[
                        "1142188b965e0d0318fa4e43-1"
                    ],
                    "id":"114218beabfcf35206834183",
                    "term":"past_three_months"
                },
                {
                    "stream_ids":[
                        "1142188b965e0d0318fa4e43-1"
                    ],
                    "id":"114218beabfcf352068341c6",
                    "term":"past_three_months"
                },
                {
                    "stream_ids":[
                        "1142188b965e0d0318fa4e43-1"
                    ],
                    "id":"114228aaabfcf35206c17bec",
                    "term":"past_three_months"
                }
            ]
        }
```
```json Webhook sample
{
      "method":"INCOME",
      "callback_type":"INCOME",
      "callback_code":"PRODUCT_IS_READY",
      "type":"CALLBACK",
      "code":"PRODUCT_IS_READY",
      "callbackURL":"https://16764cf0511d.ngrok.io/v1/callback",
      "env":"production",
      "status":"is_success",
      "started_at":"2021-10-14T00:33:13.068Z",
      "ended_at":"2021-10-14T00:36:44.195Z",
      "message":"Record callback started!",
      "accountId":"xxxxxxxxxxxxxxxxxxxxx",
      "options":{},
      "meta":{},
}
```