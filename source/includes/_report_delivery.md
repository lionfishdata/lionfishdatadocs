#Report delivery

##Email

If you choose to have your reports delivered using email, an email will be sent to the address your schedule specified. The email will contain a download url.

##Webhook
> Example json that would be posted to your webhook

```shell
{
    "list_name": "MyList",
    "download_url":"https://lionfish-reports.s3.amazonaws.com/2eea6ae4-205e-4b34-9872-a48d8114b7c6/2017-08-15/e1ca2d69e92349d1a886e5a8ace3504f.csv"
    "schedule_id": "BxnPDkeVzcFbz7b5xdCJg3"
    "run_id": "FMCURdeAERDVdzUb1PQZoD"
    "job_type": "details"
    "user_id": "6o1q5PyxH4URELKq9k5Qvy"
    "list_id": "Kue8WUQNTSn5tqJ3EvTkQx"
}
```

If you choose to have your reports delivered using webhook we will post JSON to the url you specified when creating your schedule. That json will contain a URL (under the json key `download_url`) from which your report can be downloaded from.
