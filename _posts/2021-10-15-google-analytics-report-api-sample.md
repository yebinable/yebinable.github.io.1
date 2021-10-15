---
layout: post
title: Google Report API Sample
description: Google Report API Sample
summary: Google Report API Sample
tags: [3rd-party-api, google]
---


# Method: reports.batchGet
#### API Endpoint : `POST https://analyticsreporting.googleapis.com/v4/reports:batchGet`
### Request Payload Sample
```json
{
  "reportRequests": [
    {
      "dateRanges": [
        {
          "startDate": "2020-11-01",
          "endDate": "2020-11-30"
        }
      ],
      "viewId": "12345678",
      "metrics": [
        {
          "expression": "ga:users"
        },
        {
          "expression": "ga:pageviews"
        },
        {
          "expression": "ga:sessions"
        },
        {
          "expression": "ga:pageviewsPerSession"
        }
      ],
      "filtersExpression": "ga:pageTitle==Blah Blah"
    }
  ]
}
```
### Response Payload Sample
```
{
    "reports": [{
            "columnHeader": {
                "metricHeader": {
                    "metricHeaderEntries": [{
                            "name": "ga:users",
                            "type": "INTEGER"
                        }, {
                            "name": "ga:pageviews",
                            "type": "INTEGER"
                        }, {
                            "name": "ga:sessions",
                            "type": "INTEGER"
                        }, {
                            "name": "ga:pageviewsPerSession",
                            "type": "FLOAT"
                        }
                    ]
                }
            },
            "data": {
                "rows": [{
                        "metrics": [{
                                "values": [
                                    "2057",
                                    "10639",
                                    "3501",
                                    "3.0388460439874323"
                                ]
                            }
                        ]
                    }
                ],
                "totals": [{
                        "values": [
                            "2057",
                            "10639",
                            "3501",
                            "3.0388460439874323"
                        ]
                    }
                ],
                "rowCount": 1,
                "minimums": [{
                        "values": [
                            "2057",
                            "10639",
                            "3501",
                            "3.0388460439874323"
                        ]
                    }
                ],
                "maximums": [{
                        "values": [
                            "2057",
                            "10639",
                            "3501",
                            "3.0388460439874323"
                        ]
                    }
                ],
                "isDataGolden": true
            }
        }
    ]
}
```

### Auth 2.0 / Api call Code Sample
```c#
string keyFilePath = Server.MapPath("~/App_Data/Your-API-Key-Filename.json");
string json = System.IO.File.ReadAllText(keyFilePath);

var cr = JsonConvert.DeserializeObject(json);

var xCred = new ServiceAccountCredential(new ServiceAccountCredential.Initializer(cr.client_email)
{
    Scopes = new[] {
        AnalyticsReportingService.Scope.Analytics
    }
}.FromPrivateKey(cr.private_key));

using (var svc = new AnalyticsReportingService(
    new BaseClientService.Initializer
    {
        HttpClientInitializer = xCred,
        ApplicationName = "[Your Application Name]"
    })
)
{
    // Create the DateRange object.
    DateRange dateRange = new DateRange() { StartDate = "2017-05-01", EndDate = "2017-05-31" };

    // Create the Metrics object.
    Metric sessions = new Metric { Expression = "ga:sessions", Alias = "Sessions" };

    //Create the Dimensions object.
    Dimension browser = new Dimension { Name = "ga:browser" };

    // Create the ReportRequest object.
    ReportRequest reportRequest = new ReportRequest
    {
        ViewId = "[A ViewId in your account]",
        DateRanges = new List() { dateRange },
        Dimensions = new List() { browser },
        Metrics = new List() { sessions }
    };

    List requests = new List();
    requests.Add(reportRequest);

    // Create the GetReportsRequest object.
    GetReportsRequest getReport = new GetReportsRequest() { ReportRequests = requests };

    // Call the batchGet method.
    GetReportsResponse response = svc.Reports.BatchGet(getReport).Execute();
}
```
### Set Account permission
https://stackoverflow.com/questions/12837748/analytics-google-api-error-403-user-does-not-have-any-google-analytics-account

# Reference
* Dimensions & Metrics Keys : https://ga-dev-tools.appspot.com/dimensions-metrics-explorer/
* `C#` NuGet Package download : https://www.nuget.org/packages/Google.Apis.AnalyticsReporting.v4
* `.NET` Code sample : https://developers.google.com/api-client-library/dotnet/get_started#simple
* `.NET` Lib : https://developers.google.com/api-client-library/dotnet/guide/aaa_oauth#oauth-2.0-protocol
* `.NET` OAuth 2.0 : https://developers.google.com/api-client-library/dotnet/guide/aaa_oauth
* `Google API` : https://developers.google.com/analytics/devguides/reporting/core/v4/rest/v4/reports/batchGet

