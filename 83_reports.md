# Reports

### Standard Reports

#### Retrieve a report

```
DEFINITION
GET http://apiserver/reports/:id

EXAMPLE REQUEST
$.get("http://localhost:49195/report/1");

EXAMPLE RESPONSE
{
    "id": "1",
    "name": "Account Annual Summary",
    "description": "Yearly Donation Revenue from Specified Start Date",
    "category": "ACCOUNT",
    "saw": "RSR0001",
    "subCategory": "LISTING",
    "origin": "DonorStudio",
    "comment": "PURPOSE\r\n \r\nFor each account, a ten year summary is provided for each year beginning with the start year as specified as an input parameter. The report will show all donations by year, as well as a total and lifetime amount, for each account in the specified job and segment.  The total column in the report is the sum of all the year columns and the lifetime column is the sum of all donations given over the lifetime of the account.  Additionally, there is a grand total at the end of the report summing the total for each year, the total for the specified decade and the total over the lifetime of all accounts in the job and segment.  In order for this report to be run, a job and segment must be created for the accounts wanted to be displayed in the report.\r\n\r\nINPUT PARAMETERS\r\n\r\nStart Year: The start year for the decade. \r\n\r\nJob: The selection of account donations to be included in this report.  Jobs and their segments are created within the Marketing and Analysis module, Segmentation component.\r\n\r\nCurrency Code:  Only those donations in the job and segment that were given in the currency type specified (e.g., US Dollars, Canadian Dollar, Euro) will be included in the report.\r\n\r\nType: Available choices are Deductible Only, Non-Deductible Only or All Donations.  Only those donations matching this criterion are included in the report.\r\n\r\nOUTPUT INFORMATION\r\n\r\nAcct Nbr and Name:  Number and name on the account providing the donation.  If the job was run requesting that it use family accounts then the account name will be the family account name even though the donation may have been made on the spouse’s account (unless it was explicitly stated not to consolidate with the family) or made on a dependent’s account.\r\n\r\nStart Year through Start Year+10:  Shows all donations for that account for each of those years.\r\n\r\nTotal:  Sum of all donations for that account in the specified decade.\r\n\r\nLifetime:  Sum of all donations over the lifetime of that account is selected within that job and segment even if the donation falls outside of the specified decade.\r\n\r\nAdditionally, there is a report footer that provides a grand total of all donations per year, total donations for the decade and total lifetime donations.\r\n\r\nNote:  Donations appearing in the job and segment made in a transaction where the status has been marked on hold, will not be included in the report totals.\r\n\r\n",
    "image": null,
    "url": "http://SQL01/ReportServer?%2fSE_8_0_0%2fACCOUNT%2fAccount+Annual+Summary&Environment=8_0_0"
}

```

Retrieves the details of an existing report. You need only supply the report id. The image is a base64 string of the image bytes similar to attachments.

##### Arguments

##### Returns

Returns a report object if a valid id was provided.

#### List all reports

```
DEFINITION
GET http://apiserver/reports

EXAMPLE REQUEST
$.get("http://localhost:49195/reports?name=Account*");

EXAMPLE RESPONSE
{
    "paging": {
        "limit": 10,
        "offset": 0,
        "total": 3
    },
    "items": [
        {
            "id": "1",
            "name": "Account Annual Summary",
            "description": "Yearly Donation Revenue from Specified Start Date",
            "category": "ACCOUNT",
            "saw": "RSR0001",
            "subCategory": "LISTING",
            "origin": "DonorStudio",
            "comment": "PURPOSE\r\n \r\nFor each account, a ten year summary is provided for each year beginning with the start year as specified as an input parameter. The report will show all donations by year, as well as a total and lifetime amount, for each account in the specified job and segment.  The total column in the report is the sum of all the year columns and the lifetime column is the sum of all donations given over the lifetime of the account.  Additionally, there is a grand total at the end of the report summing the total for each year, the total for the specified decade and the total over the lifetime of all accounts in the job and segment.  In order for this report to be run, a job and segment must be created for the accounts wanted to be displayed in the report.\r\n\r\nINPUT PARAMETERS\r\n\r\nStart Year: The start year for the decade. \r\n\r\nJob: The selection of account donations to be included in this report.  Jobs and their segments are created within the Marketing and Analysis module, Segmentation component.\r\n\r\nCurrency Code:  Only those donations in the job and segment that were given in the currency type specified (e.g., US Dollars, Canadian Dollar, Euro) will be included in the report.\r\n\r\nType: Available choices are Deductible Only, Non-Deductible Only or All Donations.  Only those donations matching this criterion are included in the report.\r\n\r\nOUTPUT INFORMATION\r\n\r\nAcct Nbr and Name:  Number and name on the account providing the donation.  If the job was run requesting that it use family accounts then the account name will be the family account name even though the donation may have been made on the spouse’s account (unless it was explicitly stated not to consolidate with the family) or made on a dependent’s account.\r\n\r\nStart Year through Start Year+10:  Shows all donations for that account for each of those years.\r\n\r\nTotal:  Sum of all donations for that account in the specified decade.\r\n\r\nLifetime:  Sum of all donations over the lifetime of that account is selected within that job and segment even if the donation falls outside of the specified decade.\r\n\r\nAdditionally, there is a report footer that provides a grand total of all donations per year, total donations for the decade and total lifetime donations.\r\n\r\nNote:  Donations appearing in the job and segment made in a transaction where the status has been marked on hold, will not be included in the report totals.\r\n\r\n",
            "image": null,
            "url": "http://SQL01/ReportServer?%2fSE_8_0_0%2fACCOUNT%2fAccount+Annual+Summary&Environment=8_0_0"
        },
        {...},
    ]
}

```

Returns a list of all reports. The image field will always be null. To get the image, retrieve a single report.

May be sorted by providing column criteria. Please see [Paged Response](#paged-response) section above for more details about sorting.

##### Arguments

* id (optional) - Filter list by id.
* name (optional) - Filter list by the partial match of report name.
* description (optional) - Filter list by partial match of report description.
* category (optional) - Filter list by partial match of report category.
* subCategory (optional) - Filter list by partial match of report sub category.
* origin (optional) - Filter list by partial match of report origin.

##### Returns

A dictionary with an items property that contains an array of up to limit reports, starting at index offset. Each entry in the array is a separate report object. If no more report are available, the resulting array will be empty. This request should never return an error.