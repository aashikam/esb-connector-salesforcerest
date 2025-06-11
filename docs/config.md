# Salesforce Connector Configuration and Operations Guide

## Table of Contents

*   [Prerequisites](#prerequisites)
*   [Connector Configuration](#connector-configuration)
    *   [General Configuration Parameters](#general-configuration-parameters)
    *   [OAuth 2.0 Configuration (for REST and Bulk API v2)](#1-oauth-20-configuration-for-rest-and-bulk-api-v2)
    *   [Username-Password Configuration (Primarily for SOAP API, also an option for REST)](#2-username-password-configuration-primarily-for-soap-api-also-an-option-for-rest)
    *   [Importing the Salesforce Certificate](#importing-the-salesforce-certificate)
*   [Bulk API V2 Operations](#bulk-api-v2-operations)
    *   [Bulk API 2.0 Ingest](#bulk-api-20-ingest)
        *   [salesforce.createJob](#salesforcecreatejob)
        *   [salesforce.uploadJobData](#salesforceuploadjobdata)
        *   [salesforce.closeJob](#salesforceclosejob)
        *   [salesforce.abortJob](#salesforceabortjob)
        *   [salesforce.deleteJob](#salesforcedeletejob)
        *   [salesforce.getJobInfo](#salesforcegetjobinfo)
        *   [salesforce.getAllJobs](#salesforcegetalljobs)
        *   [salesforce.getJobSuccessfulRecordResults](#salesforcegetjobsuccessfulrecordresults)
        *   [salesforce.getJobFailedRecordResults](#salesforcegetjobfailedrecordresults)
        *   [salesforce.getJobUnprocessedRecordResults](#salesforcegetjobunprocessedrecordresults)
    *   [Bulk API 2.0 Query](#bulk-api-20-query)
        *   [salesforce.createQueryJob](#salesforcecreatequeryjob)
        *   [salesforce.getQueryJobInfo](#salesforcegetqueryjobinfo)
        *   [salesforce.getQueryJobResults](#salesforcegetqueryjobresults)
        *   [salesforce.abortQueryJob](#salesforceabortqueryjob)
        *   [salesforce.deleteQueryJob](#salesforcedeletequeryjob)
        *   [salesforce.getAllQueryJobs](#salesforcegetallqueryjobs)
*   [SOAP API Operations](#soap-api-operations)
    *   [salesforce.soapConvertLead](#salesforcesoapconvertlead)
    *   [salesforce.soapCreate](#salesforcesoapcreate)
    *   [salesforce.soapDelete](#salesforcesoapdelete)
    *   [salesforce.soapDescribeGlobal](#salesforcesoapdescribeglobal)
    *   [salesforce.soapDescribeSObject](#salesforcesoapdescribesobject)
    *   [salesforce.soapDescribeSObjects](#salesforcesoapdescribesobjects)
    *   [salesforce.soapEmptyRecycleBin](#salesforcesoapemptyrecyclebin)
    *   [salesforce.soapFindDuplicates](#salesforcesoapfindduplicates)
    *   [salesforce.soapFindDuplicatesByIds](#salesforcesoapfindduplicatesbyids)
    *   [salesforce.soapGetDeleted](#salesforcesoapgetdeleted)
    *   [salesforce.soapGetServerTimestamp](#salesforcesoapgetservertimestamp)
    *   [salesforce.soapGetUpdated](#salesforcesoapgetupdated)
    *   [salesforce.soapGetUserInfo](#salesforcesoapgetuserinfo)
    *   [salesforce.soapLogout](#salesforcesoaplogout)
    *   [salesforce.soapMerge](#salesforcesoapmerge)
    *   [salesforce.soapQuery](#salesforcesoapquery)
    *   [salesforce.soapQueryAll](#salesforcesoapqueryall)
    *   [salesforce.soapQueryMore](#salesforcesoapquerymore)
    *   [salesforce.soapResetPassword](#salesforcesoapresetpassword)
    *   [salesforce.soapRetrieve](#salesforcesoapretrieve)
    *   [salesforce.soapSearch](#salesforcesoapsearch)
    *   [salesforce.soapSendEmail](#salesforcesoapsendemail)
    *   [salesforce.soapSendEmailMessage](#salesforcesoapsendemailmessage)
    *   [salesforce.soapSetPassword](#salesforcesoapsetpassword)
    *   [salesforce.soapUndelete](#salesforcesoapundelete)
    *   [salesforce.soapUpdate](#salesforcesoapupdate)
    *   [salesforce.soapUpsert](#salesforcesoapupsert)
*   [REST API Operations](#rest-api-operations)
    *   [AppMenu Operations](#appmenu-operations)
        *   [salesforce.listItemsInMenu](#salesforcelistitemsinmenu)
        *   [salesforce.tabs](#salesforcetabs)
        *   [salesforce.themes](#salesforcethemes)
    *   [Approval Operations](#approval-operations)
        *   [salesforce.listApprovals](#salesforcelistapprovals)
    *   [Event Monitoring Operations](#event-monitoring-operations)
        *   [salesforce.describeEventMonitoring](#salesforcedescribeeventmonitoring)
        *   [salesforce.queryEventMonitoringData](#salesforcequeryeventmonitoringdata)
    *   [Invocable Actions Operations](#invocable-actions-operations)
        *   [salesforce.getListOfAction](#salesforcegetlistofaction)
        *   [salesforce.getSpecificListOfAction](#salesforcegetspecificlistofaction)
        *   [salesforce.getAttributeOfSpecificAction](#salesforcegetattributeofspecificaction)
    *   [Layout Operations](#layout-operations)
        *   [salesforce.sObjectLayouts](#salesforcesobjectlayouts)
        *   [salesforce.globalSObjectLayouts](#salesforceglobalsobjectlayouts)
        *   [salesforce.compactLayouts](#salesforcecompactlayouts)
        *   [salesforce.sObjectApprovalLayouts](#salesforcesobjectapprovallayouts)
        *   [salesforce.sObjectCompactLayouts](#salesforcesobjectcompactlayouts)
        *   [salesforce.sObjectNamedLayouts](#salesforcesobjectnamedlayouts)
    *   [List View Operations](#list-view-operations)
        *   [salesforce.listViews](#salesforcelistviews)
        *   [salesforce.listViewById](#salesforcelistviewbyid)
        *   [salesforce.recentListViews](#salesforcerecentlistviews)
        *   [salesforce.describeListViewById](#salesforcedescribelistviewbyid)
        *   [salesforce.listViewResults](#salesforcelistviewresults)
    *   [Process Rule Operations](#process-rule-operations)
        *   [salesforce.listProcessRules](#salesforcelistprocessrules)
        *   [salesforce.getSpecificProcessRule](#salesforcegetspecificprocessrule)
    *   [Query Operations](#query-operations)
        *   [salesforce.query](#salesforcequery)
        *   [salesforce.queryAll](#salesforcequeryall)
        *   [salesforce.queryMore](#salesforcequerymore)
        *   [salesforce.queryAllMore](#salesforcequeryallmore)
        *   [salesforce.queryPerformanceFeedback](#salesforcequeryperformancefeedback)
        *   [salesforce.listviewQueryPerformanceFeedback](#salesforcelistviewqueryperformancefeedback)
    *   [Quick Action Operations](#quick-action-operations)
        *   [salesforce.quickActions](#salesforcequickactions)
        *   [salesforce.sObjectQuickActions](#salesforcesobjectquickactions)
        *   [salesforce.getSpecificQuickAction](#salesforcegetspecificquickaction)
        *   [salesforce.describeSpecificQuickAction](#salesforcedescribespecificquickaction)
        *   [salesforce.getDefaultValuesOfQuickAction](#salesforcegetdefaultvaluesofquickaction)
    *   [Record Operations](#record-operations)
        *   [salesforce.createRecord](#salesforcecreaterecord)
        *   [salesforce.getRecord](#salesforcegetrecord)
        *   [salesforce.updateRecord](#salesforceupdaterecord)
        *   [salesforce.deleteRecord](#salesforcedeleterecord)
        *   [salesforce.upsertRecord](#salesforceupsertrecord)
        *   [salesforce.createMultipleRecords](#salesforcecreatemultiplerecords)
        *   [salesforce.createNestedRecords](#salesforcecreatenestedrecords)
        *   [salesforce.getRecentlyViewedItems](#salesforcegetrecentlyvieweditems)
        *   [salesforce.getDeletedRecords](#salesforcegetdeletedrecords)
        *   [salesforce.getUpdatedRecords](#salesforcegetupdatedrecords)
    *   [sObject Operations](#sobject-operations)
        *   [salesforce.describeGlobal](#salesforcedescribeglobal)
        *   [salesforce.describeSObject](#salesforcedescribesobject)
        *   [salesforce.sObjectBasicInfo](#salesforcesobjectbasicinfo)
        *   [salesforce.getSObjectRows](#salesforcegetsobjectrows)
        *   [salesforce.listAvailableApiVersions](#salesforcelistavailableapiversions)
        *   [salesforce.listOrganizationLimits](#salesforcelistorganizationlimits)
        *   [salesforce.listResourcesByApiVersion](#salesforcelistresourcesbyapiversion)
        *   [salesforce.sObjectPlatformActionInfo](#salesforcesobjectplatformactioninfo)
    *   [Search Operations](#search-operations)
        *   [salesforce.search](#salesforcesearch)
        *   [salesforce.searchScopeAndOrder](#salesforcesearchscopeandorder)
        *   [salesforce.searchResultLayout](#salesforcesearchresultlayout)
        *   [salesforce.searchSuggestedRecords](#salesforcesearchsuggestedrecords)
    *   [User Operations](#user-operations)
        *   [salesforce.getUserInformation](#salesforcegetuserinformation)
        *   [salesforce.resetPassword](#salesforceresetpassword)
        *   [salesforce.setPassword](#salesforcesetpassword)
    *   [Report Operations](#report-operations)
        *   [salesforce.getReportMetadata](#salesforcegetreportmetadata)
        *   [salesforce.executeReport](#salesforceexecutereport)
        *   [salesforce.listReports](#salesforcelistreports)
    *   [Fault Handler Sequence](#fault-handler-sequence)

## Prerequisites

*   A Salesforce account. If you don't have one, sign up at [https://developer.salesforce.com/signup](https://developer.salesforce.com/signup).
*   For OAuth authentication (recommended for REST and Bulk API), you'll need to create a Connected App in Salesforce to obtain a Client ID and Client Secret. Follow Salesforce documentation for creating a Connected App and understanding OAuth scopes.
*   For SOAP API basic authentication, you'll need your Salesforce username, password, and security token.
*   Import the Salesforce certificate into your WSO2 Micro Integrator's client keystore. Detailed steps can be found in the "Importing the Salesforce Certificate" section below.

## Connector Configuration

Proper configuration is essential for the Salesforce Connector to communicate with your Salesforce instance. The connector supports different authentication mechanisms depending on the API you are interacting with.

### General Configuration Parameters

These parameters are generally applicable or form the base for specific API interactions.

??? note "Common Connection Configuration"
    It's recommended to manage connection configurations as [local entries]({{base_path}}/develop/creating-artifacts/registry/creating-local-registry-entries/) in WSO2 MI for reusability. You can then reference this configuration in operations using a `configKey` attribute.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
            <th>Notes</th>
        </tr>
        <tr>
            <td>salesforce.config.name</td>
            <td>A unique name for this Salesforce configuration.</td>
            <td>Yes</td>
            <td>Used to reference this specific configuration in operations.</td>
        </tr>
        <tr>
            <td>salesforce.instanceUrl</td>
            <td>Your Salesforce instance URL (e.g., <code>https://yourdomain.my.salesforce.com</code>).</td>
            <td>Yes</td>
            <td>This is the base URL for API calls. Not applicable for SOAP API login.</td>
        </tr>
    </table>

### 1. OAuth 2.0 Configuration (for REST and Bulk API v2)

Salesforce REST and Bulk API v2 use OAuth 2.0 for authentication. The connector can manage token refresh automatically if provided with the necessary credentials.

??? note "OAuth 2.0 Parameters"
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
            <th>Notes</th>
        </tr>
        <tr>
            <td>salesforce.clientId</td>
            <td>The Consumer Key (Client ID) of your Salesforce Connected App.</td>
            <td>Conditionally</td>
            <td>Required if not providing a pre-existing `salesforce.accessToken`, or for token refresh.</td>
        </tr>
        <tr>
            <td>salesforce.clientSecret</td>
            <td>The Consumer Secret of your Salesforce ConnectedApp.</td>
            <td>Conditionally</td>
            <td>Required for token refresh.</td>
        </tr>
        <tr>
            <td>salesforce.refreshToken</td>
            <td>The refresh token obtained during the OAuth authorization flow.</td>
            <td>Conditionally</td>
            <td>Required for the connector to automatically refresh the access token.</td>
        </tr>
        <tr>
            <td>salesforce.accessToken</td>
            <td>A pre-existing Salesforce access token.</td>
            <td>Conditionally</td>
            <td>Can be used if managing token lifecycle externally. If `clientId`, `clientSecret`, and `refreshToken` are provided, the connector will use/refresh this token. Required if other OAuth params are not set.</td>
        </tr>
        <tr>
            <td>salesforce.apiVersion</td>
            <td>The version of the Salesforce API (e.g., <code>v59.0</code>).</td>
            <td>Yes</td>
            <td>Applies to REST and Bulk API calls.</td>
        </tr>
        <tr>
            <td>salesforce.hostName</td>
            <td>Salesforce OAuth endpoint (e.g., <code>https://login.salesforce.com</code>).</td>
            <td>Yes</td>
            <td>Used for token requests.</td>
        </tr>
         <tr>
            <td>salesforce.tokenEndpointHostname</td>
            <td>The endpoint of the refresh token that you invoke to refresh the API access token. </td>
            <td>No</td>
            <td>Typically the same as `salesforce.hostName`.</td>
        </tr>
        <tr>
            <td>salesforce.blocking</td>
            <td>Indicates whether the connector needs to perform blocking invocations to Salesforce.</td>
            <td>Yes</td>
            <td>Default: `false`.</td>
        </tr>
    </table>

    > **Note:** It is highly recommended to use `salesforce.clientId`, `salesforce.clientSecret`, and `salesforce.refreshToken` to allow the connector to manage the access token lifecycle, including renewal.

    **Sample XML Configuration (OAuth for REST/Bulk):**
    ```xml
    <localEntry key="MySFConfig" xmlns="http://ws.apache.org/ns/synapse">
        <salesforce.init>
            <salesforce.config.name>MySFConfig</salesforce.config.name>
            <salesforce.instanceUrl>https://yourdomain.my.salesforce.com</salesforce.instanceUrl>
            <salesforce.apiVersion>v59.0</salesforce.apiVersion>
            <salesforce.hostName>https://login.salesforce.com</salesforce.hostName>
            <salesforce.clientId>YOUR_CLIENT_ID</salesforce.clientId>
            <salesforce.clientSecret>YOUR_CLIENT_SECRET</salesforce.clientSecret>
            <salesforce.refreshToken>YOUR_REFRESH_TOKEN</salesforce.refreshToken>
            <salesforce.blocking>false</salesforce.blocking>
        </salesforce.init>
        <description/>
    </localEntry>
    ```

    Refer to Salesforce documentation on [Understanding Authentication](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm) and OAuth flows for more details.


### 2. Username-Password Configuration (Primarily for SOAP API, also an option for REST)

This method uses your Salesforce username, password, and security token.

??? note "Username-Password Parameters"
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>salesforce.username</td>
            <td>Your Salesforce username.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>salesforce.password</td>
            <td>Your Salesforce password, appended with your security token. (e.g., `mypasswordMYSECURITYTOKEN`).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>salesforce.loginUrl</td>
            <td>The Salesforce SOAP API login URL (e.g., `https://login.salesforce.com/services/Soap/u/59.0`). Ensure the API version in the URL matches your needs.</td>
            <td>Yes (for SOAP)</td>
        </tr>
        <tr>
            <td>salesforce.clientId</td>
            <td>The Consumer Key (Client ID) of your Salesforce Connected App.</td>
            <td>Yes (for REST Username-Password flow)</td>
        </tr>
        <tr>
            <td>salesforce.clientSecret</td>
            <td>The Consumer Secret of your Salesforce ConnectedApp.</td>
            <td>Yes (for REST Username-Password flow)</td>
        </tr>
         <tr>
            <td>salesforce.hostName</td>
            <td>Salesforce OAuth endpoint (e.g., <code>https://login.salesforce.com</code>).</td>
            <td>Yes (for REST Username-Password flow, used to obtain access token)</td>
        </tr>
        <tr>
            <td>salesforce.apiVersion</td>
            <td>The version of the Salesforce API (e.g., <code>v59.0</code>).</td>
            <td>Yes (for REST Username-Password flow)</td>
        </tr>
         <tr>
            <td>salesforce.blocking</td>
            <td>Indicates whether the connector needs to perform blocking invocations to Salesforce.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration (SOAP Username-Password):**
    ```xml
    <localEntry key="MySFSoapConfig" xmlns="http://ws.apache.org/ns/synapse">
        <salesforce.init>
            <salesforce.config.name>MySFSoapConfig</salesforce.config.name>
            <salesforce.username>your_salesforce_username</salesforce.username>
            <salesforce.password>your_salesforce_password_and_token</salesforce.password>
            <salesforce.loginUrl>https://login.salesforce.com/services/Soap/u/59.0</salesforce.loginUrl>
            <salesforce.blocking>false</salesforce.blocking>
        </salesforce.init>
        <description/>
    </localEntry>
    ```

    **Sample XML Configuration (REST Username-Password):**
    ```xml
     <localEntry key="MySFRestUserPassConfig" xmlns="http://ws.apache.org/ns/synapse">
        <salesforce.init>
            <salesforce.config.name>MySFRestUserPassConfig</salesforce.config.name>
            <salesforce.instanceUrl>https://yourdomain.my.salesforce.com</salesforce.instanceUrl>
            <salesforce.username>your_salesforce_username</salesforce.username>
            <salesforce.password>your_salesforce_password_and_token</salesforce.password>
            <salesforce.clientId>YOUR_CLIENT_ID</salesforce.clientId>
            <salesforce.clientSecret>YOUR_CLIENT_SECRET</salesforce.clientSecret>
            <salesforce.hostName>https://login.salesforce.com</salesforce.hostName> <!-- Used for the token call -->
            <salesforce.apiVersion>v59.0</salesforce.apiVersion>
            <salesforce.blocking>false</salesforce.blocking>
        </salesforce.init>
        <description/>
    </localEntry>
    ```

### Importing the Salesforce Certificate

Before you start configuring the connector, import the Salesforce certificate to your WSO2 MI's client keystore.

1.  Log in to your Salesforce account in your browser (e.g., `https://login.salesforce.com`).
2.  View the certificate (usually by clicking the lock icon in the address bar) and export it to your file system.
3.  Import the certificate into the MI's client keystore:
    ```bash
    keytool -importcert -file <path_to_certificate_file> -keystore <MI_HOME>/repository/resources/security/client-truststore.jks -alias "Salesforce" -storepass wso2carbon
    ```
    (Replace `<path_to_certificate_file>` and `<MI_HOME>` with actual paths. The default password for `client-truststore.jks` is `wso2carbon`.)
4.  Restart the WSO2 Micro Integrator.

## Bulk API V2 Operations

The Salesforce Bulk API 2.0 provides a programmatic way to quickly and efficiently load, delete, or query large sets of data into your Salesforce org. It is an asynchronous API that processes data in batches. Bulk API 2.0 is built on the Salesforce REST framework and uses OAuth 2.0 for authentication.

### Bulk API 2.0 Ingest

Ingest operations are used to load data into Salesforce. This involves creating a job, uploading data in CSV format, and then monitoring the job's progress.

??? note "salesforce.createJob"
    The `salesforce.createJob` operation creates a new bulk ingest job in Salesforce. This job specifies the object you’re processing (e.g., Account, Contact) and the operation you’re performing (e.g., insert, update, delete).

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The `salesforce.config.name` of the Salesforce configuration local entry (e.g., `MySFConfig`) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>object</td>
            <td>The object type for the data being processed (e.g., <code>Account</code>, <code>Contact</code>, <code>CustomObject__c</code>).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>operation</td>
            <td>
                The processing operation for all data in the job. Valid values are:
                <ul>
                    <li><code>insert</code>: Create new records.</li>
                    <li><code>delete</code>: Delete records.</li>
                    <li><code>hardDelete</code>: Permanently delete records (if enabled in your org).</li>
                    <li><code>update</code>: Update existing records.</li>
                    <li><code>upsert</code>: Update records if they exist, or insert them if they don't. Requires specifying an <code>externalIdFieldName</code>.</li>
                </ul>
            </td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>columnDelimiter</td>
            <td>
                The column delimiter used for CSV job data. Valid values are:
                <ul>
                    <li><code>BACKQUOTE</code> (`)</li>
                    <li><code>CARET</code> (^)</li>
                    <li><code>COMMA</code> (,) - Default</li>
                    <li><code>PIPE</code> (|)</li>
                    <li><code>SEMICOLON</code> (;)</li>
                    <li><code>TAB</code> (\t)</li>
                </ul>
            </td>
            <td>No</td>
        </tr>
        <tr>
            <td>contentType</td>
            <td>The content type for the job. Currently, only <code>CSV</code> is supported. Defaults to <code>CSV</code>.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>externalIdFieldName</td>
            <td>The external ID field name to be used for <code>upsert</code> operations. This field must be defined as an External ID field on the specified object.</td>
            <td>Conditionally (Required for <code>upsert</code>)</td>
        </tr>
        <tr>
            <td>lineEnding</td>
            <td>
                The line ending used for CSV job data. Valid values are:
                <ul>
                    <li><code>LF</code> (Line Feed) - Default</li>
                    <li><code>CRLF</code> (Carriage Return Line Feed)</li>
                </ul>
            </td>
            <td>No</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <salesforce.createJob configKey="MySFConfig">
        <object>Account</object>
        <operation>insert</operation>
        <contentType>CSV</contentType>
        <columnDelimiter>COMMA</columnDelimiter>
        <lineEnding>LF</lineEnding>
    </salesforce.createJob>
    ```

    **Sample Response:**
    ```json
    {
        "id": "750R0000000zhQVIAY",
        "operation": "insert",
        "object": "Account",
        "createdById": "005R0000000jNhGIAU",
        "createdDate": "2023-10-27T10:00:00.000+0000",
        "systemModstamp": "2023-10-27T10:00:00.000+0000",
        "state": "Open",
        "concurrencyMode": "Parallel",
        "contentType": "CSV",
        "apiVersion": "59.0",
        "jobType": "V2Ingest",
        "lineEnding": "LF",
        "columnDelimiter": "COMMA"
    }
    ```

??? note "salesforce.uploadJobData"
    The `salesforce.uploadJobData` operation uploads CSV data for a previously created bulk ingest job. The request body should be the raw CSV data.

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The `salesforce.config.name` of the Salesforce configuration local entry (e.g., `MySFConfig`) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>jobId</td>
            <td>The ID of the bulk ingest job to which the data should be uploaded. This is obtained from the `salesforce.createJob` response.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>csvData</td>
            <td>The CSV data to upload. This should be provided as the message payload or constructed within the sequence. Example: <code>"Name,BillingCity\nSalesforce,San Francisco"</code></td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <!-- Assuming CSV data is in a property or message body -->
    <property name="csvPayload" value="Name,Industry,NumberOfEmployees\nTestCompany1,Tech,100\nTestCompany2,Finance,250" scope="default" type="STRING"/>
    <salesforce.uploadJobData configKey="MySFConfig">
        <jobId>{$ctx:jobIdFromCreate}</jobId>
        <csvData>{$ctx:csvPayload}</csvData>
    </salesforce.uploadJobData>
    ```
    This operation returns an HTTP 201 Created status on success with an empty body.

??? note "salesforce.closeJob"
    The `salesforce.closeJob` operation signals to Salesforce that all data for a bulk ingest job has been uploaded. Once a job is closed, Salesforce begins processing the data. No more data can be uploaded to this job.

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The `salesforce.config.name` of the Salesforce configuration local entry (e.g., `MySFConfig`) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>jobId</td>
            <td>The ID of the bulk ingest job to close.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <salesforce.closeJob configKey="MySFConfig">
        <jobId>{$ctx:jobIdFromCreate}</jobId>
    </salesforce.closeJob>
    ```

    **Sample Response (Job successfully closed and processing started):**
    ```json
    {
        "id": "750R0000000zhQVIAY",
        "operation": "insert",
        "object": "Account",
        "createdById": "005R0000000jNhGIAU",
        "createdDate": "2023-10-27T10:00:00.000+0000",
        "systemModstamp": "2023-10-27T10:05:00.000+0000",
        "state": "UploadComplete", // State changes to UploadComplete
        "concurrencyMode": "Parallel",
        "contentType": "CSV",
        "apiVersion": "59.0",
        "jobType": "V2Ingest",
        "lineEnding": "LF",
        "columnDelimiter": "COMMA"
    }
    ```

??? note "salesforce.abortJob"
    The `salesforce.abortJob` operation aborts a bulk ingest job. Aborted jobs are not processed.

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The `salesforce.config.name` of the Salesforce configuration local entry (e.g., `MySFConfig`) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>jobId</td>
            <td>The ID of the bulk ingest job to abort.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <salesforce.abortJob configKey="MySFConfig">
        <jobId>{$ctx:jobIdFromCreate}</jobId>
    </salesforce.abortJob>
    ```

    **Sample Response (Job successfully aborted):**
    ```json
    {
        "id": "750R0000000zhQVIAY",
        "operation": "insert",
        "object": "Account",
        "createdById": "005R0000000jNhGIAU",
        "createdDate": "2023-10-27T10:00:00.000+0000",
        "systemModstamp": "2023-10-27T10:10:00.000+0000",
        "state": "Aborted", // State changes to Aborted
        "concurrencyMode": "Parallel",
        "contentType": "CSV",
        "apiVersion": "59.0",
        "jobType": "V2Ingest",
        "lineEnding": "LF",
        "columnDelimiter": "COMMA"
    }
    ```

??? note "salesforce.deleteJob"
    The `salesforce.deleteJob` operation deletes a completed or aborted bulk ingest job. This does not delete the data that was processed by the job, only the job record itself.

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The `salesforce.config.name` of the Salesforce configuration local entry (e.g., `MySFConfig`) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>jobId</td>
            <td>The ID of the bulk ingest job to delete.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <salesforce.deleteJob configKey="MySFConfig">
        <jobId>{$ctx:jobIdFromCreate}</jobId>
    </salesforce.deleteJob>
    ```
    This operation returns an HTTP 204 No Content status on success.

??? note "salesforce.getJobInfo"
    The `salesforce.getJobInfo` operation retrieves detailed information about a specific bulk ingest job, including its current state, processing statistics, and error messages.

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The `salesforce.config.name` of the Salesforce configuration local entry (e.g., `MySFConfig`) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>jobId</td>
            <td>The ID of the bulk ingest job for which to retrieve information.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <salesforce.getJobInfo configKey="MySFConfig">
        <jobId>{$ctx:jobIdFromCreate}</jobId>
    </salesforce.getJobInfo>
    ```

    **Sample Response (Job in 'JobComplete' state):**
    ```json
    {
        "id": "750R0000000zhQVIAY",
        "operation": "insert",
        "object": "Account",
        "createdById": "005R0000000jNhGIAU",
        "createdDate": "2023-10-27T10:00:00.000+0000",
        "systemModstamp": "2023-10-27T10:15:00.000+0000",
        "state": "JobComplete", // State showing job is complete
        "concurrencyMode": "Parallel",
        "contentType": "CSV",
        "apiVersion": "59.0",
        "jobType": "V2Ingest",
        "lineEnding": "LF",
        "columnDelimiter": "COMMA",
        "numberRecordsProcessed": 1500,
        "numberRecordsFailed": 5,
        "retries": 0,
        "totalProcessingTime": 120050, // Milliseconds
        "apiActiveProcessingTime": 110000,
        "apexProcessingTime": 0
    }
    ```

??? note "salesforce.getAllJobs"
    The `salesforce.getAllJobs` operation retrieves a list of all bulk ingest jobs in your Salesforce org, with optional filtering by job type, state, and date.

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The `salesforce.config.name` of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>jobType</td>
            <td>
                Filters jobs by type. Valid values:
                <ul>
                    <li><code>BigObjectIngest</code></li>
                    <li><code>Classic</code> (for Bulk API 1.0 jobs)</li>
                    <li><code>V2Ingest</code> (Default, for Bulk API 2.0 ingest jobs)</li>
                </ul>
            </td>
            <td>No</td>
        </tr>
        <tr>
            <td>queryLocator</td>
            <td>If the initial request does not return all jobs, the response includes a <code>nextRecordsUrl</code>. Use the <code>queryLocator</code> from this URL to retrieve the next set of results.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>isPkChunkingEnabled</td>
            <td>Filters jobs based on whether PK Chunking is enabled. (Typically more relevant for Bulk API 1.0 query jobs).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>createdDate</td>
            <td>Filters jobs by a specific creation date (YYYY-MM-DD format).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>limit</td>
            <td>Maximum number of jobs to return. Default is 1000. Maximum is 10000.</td>
            <td>No</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <salesforce.getAllJobs configKey="MySFConfig">
        <jobType>V2Ingest</jobType>
        <limit>5</limit>
    </salesforce.getAllJobs>
    ```

    **Sample Response:**
    ```json
    {
        "done": true,
        "records": [
            {
                "id": "750R0000000zhQVIAY",
                "operation": "insert",
                "object": "Account",
                // ... other job fields ...
                "state": "JobComplete"
            },
            {
                "id": "750R0000000ziTYIAY",
                "operation": "update",
                "object": "Contact",
                // ... other job fields ...
                "state": "UploadComplete"
            }
            // ... more jobs
        ],
        "nextRecordsUrl": null // or "/services/data/vXX.X/jobs/ingest?queryLocator=someLocator" if more results
    }
    ```

??? note "salesforce.getJobSuccessfulRecordResults"
    The `salesforce.getJobSuccessfulRecordResults` operation retrieves a list of record IDs that were successfully processed in a completed bulk ingest job. The results are returned in CSV format.

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The `salesforce.config.name` of the Salesforce configuration local entry (e.g., `MySFConfig`) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>jobId</td>
            <td>The ID of the completed bulk ingest job.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>locator</td>
            <td>If the result set is too large, Salesforce paginates it and provides an <code>Sforce-Locator</code> header in the response. Use this value to retrieve the next page of results.</td>
            <td>No</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <salesforce.getJobSuccessfulRecordResults configKey="MySFConfig">
        <jobId>{$ctx:completedJobId}</jobId>
    </salesforce.getJobSuccessfulRecordResults>
    ```

    **Sample Response (CSV data):**
    ```csv
    "sf__Id","sf__Created","Name","CustomField__c"
    "001R000000abcdefghij","true","Test Record 1","Value1"
    "001R000000klmnopqr","false","Test Record 2","Value2"
    ...
    ```
    The response payload will be the CSV data. Check the `Sforce-Locator` header for pagination.

??? note "salesforce.getJobFailedRecordResults"
    The `salesforce.getJobFailedRecordResults` operation retrieves a list of records that failed to process in a completed bulk ingest job, along with error messages for each failure. The results are returned in CSV format.

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The `salesforce.config.name` of the Salesforce configuration local entry (e.g., `MySFConfig`) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>jobId</td>
            <td>The ID of the completed bulk ingest job.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>locator</td>
            <td>If the result set is too large, Salesforce paginates it and provides an <code>Sforce-Locator</code> header in the response. Use this value to retrieve the next page of results.</td>
            <td>No</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <salesforce.getJobFailedRecordResults configKey="MySFConfig">
        <jobId>{$ctx:completedJobId}</jobId>
    </salesforce.getJobFailedRecordResults>
    ```

    **Sample Response (CSV data):**
    ```csv
    "sf__Id","sf__Error","Name","BillingCity"
    "","INVALID_FIELD:No such column 'InvalidColumn' on entity 'Account'.","New Corp",""
    "","FIELD_CUSTOM_VALIDATION_EXCEPTION:Custom validation rule violated.","Another Corp",""
    ...
    ```
    The response payload will be the CSV data. Check the `Sforce-Locator` header for pagination.

??? note "salesforce.getJobUnprocessedRecordResults"
    The `salesforce.getJobUnprocessedRecordResults` operation retrieves records from a bulk ingest job that were not processed. This can happen if a job is aborted or if there's an unrecoverable error during processing. The results are returned in CSV format.

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The `salesforce.config.name` of the Salesforce configuration local entry (e.g., `MySFConfig`) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>jobId</td>
            <td>The ID of the bulk ingest job.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>locator</td>
            <td>If the result set is too large, Salesforce paginates it and provides an <code>Sforce-Locator</code> header in the response. Use this value to retrieve the next page of results.</td>
            <td>No</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <salesforce.getJobUnprocessedRecordResults configKey="MySFConfig">
        <jobId>{$ctx:jobId}</jobId>
    </salesforce.getJobUnprocessedRecordResults>
    ```

    **Sample Response (CSV data):**
    The format is similar to `getJobSuccessfulRecordResults`, containing the data that was not processed. Check the `Sforce-Locator` header for pagination.

### Bulk API 2.0 Query

Query operations are used to retrieve large sets of data from Salesforce. This involves creating a query job, checking its status, and then retrieving the results.

??? note "salesforce.createQueryJob"
    The `salesforce.createQueryJob` operation creates a new bulk query job in Salesforce. You provide a SOQL query, and Salesforce processes it asynchronously.

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The `salesforce.config.name` of the Salesforce configuration local entry (e.g., `MySFConfig`) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>query</td>
            <td>The SOQL query to execute (e.g., <code>SELECT Id, Name FROM Account</code>). Note: Relationship queries (sub-queries) are not supported in Bulk API 2.0 queries. Also, certain SOQL clauses like <code>GROUP BY CUBE</code>, <code>OFFSET</code>, <code>TYPEOF</code> are not supported. Refer to Salesforce Bulk API 2.0 documentation for SOQL limitations.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>contentType</td>
            <td>The desired content type for the query results. Only <code>CSV</code> is supported. Defaults to <code>CSV</code>.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>columnDelimiter</td>
            <td>
                The column delimiter for the CSV query results. Valid values:
                <ul>
                    <li><code>BACKQUOTE</code> (`)</li>
                    <li><code>CARET</code> (^)</li>
                    <li><code>COMMA</code> (,) - Default</li>
                    <li><code>PIPE</code> (|)</li>
                    <li><code>SEMICOLON</code> (;)</li>
                    <li><code>TAB</code> (\t)</li>
                </ul>
            </td>
            <td>No</td>
        </tr>
        <tr>
            <td>lineEnding</td>
            <td>
                The line ending for the CSV query results. Valid values:
                <ul>
                    <li><code>LF</code> (Line Feed) - Default</li>
                    <li><code>CRLF</code> (Carriage Return Line Feed)</li>
                </ul>
            </td>
            <td>No</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <salesforce.createQueryJob configKey="MySFConfig">
        <query>SELECT Id, Name, Industry FROM Account WHERE Industry = 'Technology'</query>
        <contentType>CSV</contentType>
        <columnDelimiter>PIPE</columnDelimiter>
        <lineEnding>LF</lineEnding>
    </salesforce.createQueryJob>
    ```

    **Sample Response:**
    ```json
    {
        "id": "750R0000000zkLMAIL",
        "operation": "query",
        "object": "Account", // Inferred from query
        "createdById": "005R0000000jNhGIAU",
        "createdDate": "2023-10-27T11:00:00.000+0000",
        "systemModstamp": "2023-10-27T11:00:00.000+0000",
        "state": "UploadComplete", // Query jobs start in UploadComplete, then move to InProgress, JobComplete, or Failed
        "concurrencyMode": "Parallel",
        "contentType": "CSV",
        "apiVersion": "59.0",
        "jobType": "V2Query",
        "lineEnding": "LF",
        "columnDelimiter": "PIPE"
    }
    ```

??? note "salesforce.getQueryJobInfo"
    The `salesforce.getQueryJobInfo` operation retrieves detailed information about a specific bulk query job, including its current state, the number of records retrieved, and error messages if any.

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The `salesforce.config.name` of the Salesforce configuration local entry (e.g., `MySFConfig`) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>jobId</td>
            <td>The ID of the bulk query job for which to retrieve information.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <salesforce.getQueryJobInfo configKey="MySFConfig">
        <jobId>{$ctx:queryJobId}</jobId>
    </salesforce.getQueryJobInfo>
    ```

    **Sample Response (Job in 'JobComplete' state):**
    ```json
    {
        "id": "750R0000000zkLMAIL",
        "operation": "query",
        "object": "Account",
        "createdById": "005R0000000jNhGIAU",
        "createdDate": "2023-10-27T11:00:00.000+0000",
        "systemModstamp": "2023-10-27T11:05:00.000+0000",
        "state": "JobComplete",
        "concurrencyMode": "Parallel",
        "contentType": "CSV",
        "apiVersion": "59.0",
        "jobType": "V2Query",
        "lineEnding": "LF",
        "columnDelimiter": "PIPE",
        "numberRecordsProcessed": 5000, // Number of records retrieved
        "numberRecordsFailed": 0,
        "retries": 0,
        "totalProcessingTime": 60000, // Milliseconds
        "apiActiveProcessingTime": 55000,
        "apexProcessingTime": 0
    }
    ```

??? note "salesforce.getQueryJobResults"
    The `salesforce.getQueryJobResults` operation retrieves the results of a completed bulk query job. The results are returned in CSV format.

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The `salesforce.config.name` of the Salesforce configuration local entry (e.g., `MySFConfig`) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>jobId</td>
            <td>The ID of the completed bulk query job.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>locator</td>
            <td>If the result set is too large for a single response (typically > 1GB or based on internal Salesforce limits), Salesforce paginates it and provides an <code>Sforce-Locator</code> header in the response. Use this value to retrieve the next page of results.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>maxRecords</td>
            <td>Specifies the maximum number of records to return in the current request. Useful for controlling the size of the CSV data chunks if you are processing them incrementally. Salesforce may return fewer records than specified if the remaining data is smaller or if internal limits are hit.</td>
            <td>No</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <salesforce.getQueryJobResults configKey="MySFConfig">
        <jobId>{$ctx:completedQueryJobId}</jobId>
        <!-- <maxRecords>10000</maxRecords> --> <!-- Optional -->
    </salesforce.getQueryJobResults>
    ```

    **Sample Response (CSV data):**
    ```csv
    "Id","Name","Industry"
    "001R000000uvwxyzABCD","Tech Innovators Inc.","Technology"
    "001R000000efghijKLMN","Global Solutions Ltd.","Technology"
    ...
    ```
    The response payload will be the CSV data. Check the `Sforce-Locator` header for pagination if results are chunked. The `Content-Type` header will be `text/csv`.

??? note "salesforce.abortQueryJob"
    The `salesforce.abortQueryJob` operation aborts a bulk query job. An aborted job is not processed further, and results cannot be retrieved.

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The `salesforce.config.name` of the Salesforce configuration local entry (e.g., `MySFConfig`) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>jobId</td>
            <td>The ID of the bulk query job to abort.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <salesforce.abortQueryJob configKey="MySFConfig">
        <jobId>{$ctx:queryJobId}</jobId>
    </salesforce.abortQueryJob>
    ```

    **Sample Response (Job successfully aborted):**
    ```json
    {
        "id": "750R0000000zkLMAIL",
        "operation": "query",
        "object": "Account",
        "createdById": "005R0000000jNhGIAU",
        "createdDate": "2023-10-27T11:00:00.000+0000",
        "systemModstamp": "2023-10-27T11:02:00.000+0000",
        "state": "Aborted",
        "concurrencyMode": "Parallel",
        "contentType": "CSV",
        "apiVersion": "59.0",
        "jobType": "V2Query",
        "lineEnding": "LF",
        "columnDelimiter": "PIPE"
    }
    ```

??? note "salesforce.deleteQueryJob"
    The `salesforce.deleteQueryJob` operation deletes a completed or aborted bulk query job. This only deletes the job record, not the data that was queried.

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The `salesforce.config.name` of the Salesforce configuration local entry (e.g., `MySFConfig`) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>jobId</td>
            <td>The ID of the bulk query job to delete.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <salesforce.deleteQueryJob configKey="MySFConfig">
        <jobId>{$ctx:queryJobId}</jobId>
    </salesforce.deleteQueryJob>
    ```
    This operation returns an HTTP 204 No Content status on success.

??? note "salesforce.getAllQueryJobs"
    The `salesforce.getAllQueryJobs` operation retrieves a list of all bulk query jobs in your Salesforce org, with optional filtering.

    **Properties:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>jobType</td>
            <td>
                Filters jobs by type. For query jobs, this is typically <code>V2Query</code>.
                Valid values include:
                <ul>
                    <li><code>V2Query</code> (Default, for Bulk API 2.0 query jobs)</li>
                </ul>
            </td>
            <td>No</td>
        </tr>
        <tr>
            <td>queryLocator</td>
            <td>If the initial request does not return all jobs, the response includes a <code>nextRecordsUrl</code>. Use the <code>queryLocator</code> from this URL to retrieve the next set of results.</td>
            <td>No</td>
        </tr>
         <tr>
            <td>concurrencyMode</td>
            <td>Filters jobs by concurrency mode (<code>Parallel</code> or <code>Serial</code>).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>state</td>
            <td>
                Filters jobs by state. Valid states for query jobs:
                <ul>
                    <li><code>UploadComplete</code></li>
                    <li><code>InProgress</code></li>
                    <li><code>JobComplete</code></li>
                    <li><code>Aborted</code></li>
                    <li><code>Failed</code></li>
                </ul>
            </td>
            <td>No</td>
        </tr>
         <tr>
            <td>createdDate</td>
            <td>Filters jobs by a specific creation date (YYYY-MM-DD format).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>limit</td>
            <td>Maximum number of jobs to return. Default is 1000. Maximum is 10000.</td>
            <td>No</td>
        </tr>
    </table>

    **Sample Synapse Configuration:**
    ```xml
    <salesforce.getAllQueryJobs configKey="MySFConfig">
        <state>JobComplete</state>
        <limit>10</limit>
    </salesforce.getAllQueryJobs>
    ```

    **Sample Response:**
    ```json
    {
        "done": true,
        "records": [
            {
                "id": "750R0000000zkLMAIL",
                "operation": "query",
                "object": "Account",
                "state": "JobComplete",
                // ... other job fields ...
            },
            {
                "id": "750R0000000zlPQRST",
                "operation": "query",
                "object": "Contact",
                "state": "JobComplete",
                // ... other job fields ...
            }
        ],
        "nextRecordsUrl": null
    }
    ```

## SOAP API Operations

The Salesforce SOAP connector allows you to access the [Salesforce SOAP API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_quickstart_intro.htm?search_text=SOAP%20API%20Developer%20Guide) from the integration sequence.

??? note "salesforce.soapConvertLead"
    The `salesforce.soapConvertLead` operation interacts with the Salesforce SOAP API to convert leads to accounts and contacts. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [convertLead() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_convertlead.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation. Common parameters include:

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>leadConverts</td>
            <td>An array of LeadConvert objects. Each LeadConvert object specifies how a lead should be converted.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapConvertLead configKey="MySFSoapConfig">
        <leadConverts>
            <leadConvert>
                <leadId>00QXXXXXXXXXXXXXXX</leadId>
                <convertedStatus>Closed - Converted</convertedStatus>
                <accountId>001YYYYYYYYYYYYYYY</accountId> <!-- Optional: existing account to merge into -->
                <!-- Add other LeadConvert fields as needed -->
            </leadConvert>
        </leadConverts>
    </salesforce.soapConvertLead>
    ```

??? note "salesforce.soapCreate"
    The `salesforce.soapCreate` operation interacts with the Salesforce SOAP API to create records. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [create() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_create.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation. Common parameters include:

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjects</td>
            <td>An array of one or more sObjects to create. Each sObject must be of the same type.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapCreate configKey="MySFSoapConfig">
        <sObjects>
            <sObject xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="sf:Account" xmlns:sf="urn:sobject.partner.soap.sforce.com">
                <sf:Name>My New Account via SOAP</sf:Name>
                <sf:Industry>Technology</sf:Industry>
            </sObject>
        </sObjects>
    </salesforce.soapCreate>
    ```

??? note "salesforce.soapDelete"
    The `salesforce.soapDelete` operation interacts with the Salesforce SOAP API to delete records. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [delete() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_delete.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation. Common parameters include:

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>ids</td>
            <td>An array of one or more record IDs to delete.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapDelete configKey="MySFSoapConfig">
        <ids>
            <id>001XXXXXXXXXXXXXXX</id>
            <id>003YYYYYYYYYYYYYYY</id>
        </ids>
    </salesforce.soapDelete>
    ```

??? note "salesforce.soapDescribeGlobal"
    The `salesforce.soapDescribeGlobal` operation interacts with the Salesforce SOAP API to retrieve a list of all sObjects available in your organization. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [describeGlobal() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_describeglobal.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapDescribeGlobal configKey="MySFSoapConfig" />
    ```

??? note "salesforce.soapDescribeSObject"
    The `salesforce.soapDescribeSObject` operation interacts with the Salesforce SOAP API to retrieve metadata about a specific sObject, including its fields, child relationships, and record type information. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [describeSObject() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_describesobject.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectType</td>
            <td>The name of the sObject to describe (e.g., <code>Account</code>, <code>Contact</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapDescribeSObject configKey="MySFSoapConfig">
        <sObjectType>Account</sObjectType>
    </salesforce.soapDescribeSObject>
    ```

??? note "salesforce.soapDescribeSObjects"
    The `salesforce.soapDescribeSObjects` operation interacts with the Salesforce SOAP API to retrieve metadata for multiple sObject types in a single call. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [describeSObjects() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_describesobjects.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectTypes</td>
            <td>An array of sObject names (e.g., <code>Account</code>, <code>Contact</code>, <code>Opportunity</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapDescribeSObjects configKey="MySFSoapConfig">
        <sObjectTypes>
            <type>Account</type>
            <type>Contact</type>
            <type>Opportunity</type>
        </sObjectTypes>
    </salesforce.soapDescribeSObjects>
    ```

??? note "salesforce.soapEmptyRecycleBin"
    The `salesforce.soapEmptyRecycleBin` operation interacts with the Salesforce SOAP API to permanently delete records from the Recycle Bin. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [emptyRecycleBin() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_emptyrecyclebin.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>ids</td>
            <td>An array of record IDs currently in the Recycle Bin to be permanently deleted.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapEmptyRecycleBin configKey="MySFSoapConfig">
        <ids>
            <id>001XXXXXXXXXXXXXXX</id> <!-- ID of a deleted record -->
        </ids>
    </salesforce.soapEmptyRecycleBin>
    ```

??? note "salesforce.soapFindDuplicates"
    The `salesforce.soapFindDuplicates` operation interacts with the Salesforce SOAP API to identify duplicate records based on matching rules. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [findDuplicates() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_findduplicates.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjects</td>
            <td>An array of sObjects to check for duplicates.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapFindDuplicates configKey="MySFSoapConfig">
        <sObjects>
            <sObject xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="sf:Account" xmlns:sf="urn:sobject.partner.soap.sforce.com">
                <sf:Name>Possible Duplicate Account</sf:Name>
                <sf:BillingCity>San Francisco</sf:BillingCity>
            </sObject>
        </sObjects>
    </salesforce.soapFindDuplicates>
    ```

??? note "salesforce.soapFindDuplicatesByIds"
    The `salesforce.soapFindDuplicatesByIds` operation interacts with the Salesforce SOAP API to find duplicates for a given set of record IDs based on the matching rules for those records' object types. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters. This is similar to `findDuplicates()`, but operates on existing record IDs.

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>ids</td>
            <td>An array of record IDs to check for duplicates.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapFindDuplicatesByIds configKey="MySFSoapConfig">
        <ids>
            <id>001XXXXXXXXXXXXXXX</id>
            <id>001YYYYYYYYYYYYYYY</id>
        </ids>
    </salesforce.soapFindDuplicatesByIds>
    ```

??? note "salesforce.soapGetDeleted"
    The `salesforce.soapGetDeleted` operation interacts with the Salesforce SOAP API to retrieve a list of records that have been deleted within a specified date range for a given sObject type. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [getDeleted() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_getdeleted.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectType</td>
            <td>The name of the sObject type for which to retrieve deleted records (e.g., <code>Account</code>).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>startDate</td>
            <td>The start of the date range (inclusive) for deleted records (XML Schema dateTime format).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>endDate</td>
            <td>The end of the date range (inclusive) for deleted records (XML Schema dateTime format).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapGetDeleted configKey="MySFSoapConfig">
        <sObjectType>Account</sObjectType>
        <startDate>2023-01-01T00:00:00.000Z</startDate>
        <endDate>2023-10-28T00:00:00.000Z</endDate>
    </salesforce.soapGetDeleted>
    ```

??? note "salesforce.soapGetServerTimestamp"
    The `salesforce.soapGetServerTimestamp` operation interacts with the Salesforce SOAP API to retrieve the current system timestamp from the Salesforce server. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [getServerTimestamp() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_getservertimestamp.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapGetServerTimestamp configKey="MySFSoapConfig" />
    ```

??? note "salesforce.soapGetUpdated"
    The `salesforce.soapGetUpdated` operation interacts with the Salesforce SOAP API to retrieve a list of records that have been created or updated within a specified date range for a given sObject type. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [getUpdated() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_getupdated.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectType</td>
            <td>The name of the sObject type for which to retrieve updated records (e.g., <code>Lead</code>).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>startDate</td>
            <td>The start of the date range (inclusive) for updated records (XML Schema dateTime format).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>endDate</td>
            <td>The end of the date range (inclusive) for updated records (XML Schema dateTime format).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapGetUpdated configKey="MySFSoapConfig">
        <sObjectType>Lead</sObjectType>
        <startDate>2023-01-01T00:00:00.000Z</startDate>
        <endDate>2023-10-28T00:00:00.000Z</endDate>
    </salesforce.soapGetUpdated>
    ```

??? note "salesforce.soapGetUserInfo"
    The `salesforce.soapGetUserInfo` operation interacts with the Salesforce SOAP API to retrieve information about the currently logged-in user. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [getUserInfo() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_getuserinfo.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapGetUserInfo configKey="MySFSoapConfig" />
    ```

??? note "salesforce.soapLogout"
    The `salesforce.soapLogout` operation interacts with the Salesforce SOAP API to end the current user's session. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [logout() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_logout.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapLogout configKey="MySFSoapConfig" />
    ```

??? note "salesforce.soapMerge"
    The `salesforce.soapMerge` operation interacts with the Salesforce SOAP API to merge duplicate records. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [merge() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_merge.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>mergeRequests</td>
            <td>An array of MergeRequest objects. Each object specifies the master record and the record(s) to be merged into it.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapMerge configKey="MySFSoapConfig">
        <mergeRequests>
            <request>
                <masterRecord xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="sf:Account" xmlns:sf="urn:sobject.partner.soap.sforce.com">
                    <sf:Id>001MASTERXXXXXXX</sf:Id>
                    <!-- Other fields to update on master -->
                </masterRecord>
                <recordToMergeIds>001DUPLICATE1XXXXX</recordToMergeIds>
                <recordToMergeIds>001DUPLICATE2XXXXX</recordToMergeIds>
            </request>
        </mergeRequests>
    </salesforce.soapMerge>
    ```

??? note "salesforce.soapQuery"
    The `salesforce.soapQuery` operation interacts with the Salesforce SOAP API to execute a SOQL query. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [query() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_query.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>queryString</td>
            <td>The SOQL query string (e.g., <code>SELECT Name FROM Account</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapQuery configKey="MySFSoapConfig">
        <queryString>SELECT Id, Name, Industry FROM Account WHERE AnnualRevenue > 500000</queryString>
    </salesforce.soapQuery>
    ```

??? note "salesforce.soapQueryAll"
    The `salesforce.soapQueryAll` operation interacts with the Salesforce SOAP API to execute a SOQL query that includes archived and deleted records. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [queryAll() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_queryall.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>queryString</td>
            <td>The SOQL query string.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapQueryAll configKey="MySFSoapConfig">
        <queryString>SELECT Id, Name, IsDeleted FROM Account WHERE IsDeleted = true</queryString>
    </salesforce.soapQueryAll>
    ```

??? note "salesforce.soapQueryMore"
    The `salesforce.soapQueryMore` operation interacts with the Salesforce SOAP API to retrieve the next batch of results from a query that returned more records than the initial batch size. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [queryMore() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_querymore.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>queryLocator</td>
            <td>The query locator returned from the previous `query()` or `queryMore()` call.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapQueryMore configKey="MySFSoapConfig">
        <queryLocator>{$ctx:previousQueryLocator}</queryLocator>
    </salesforce.soapQueryMore>
    ```

??? note "salesforce.soapResetPassword"
    The `salesforce.soapResetPassword` operation interacts with the Salesforce SOAP API to initiate the password reset process for a user. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [resetPassword() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_resetpassword.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>userId</td>
            <td>The ID of the user whose password is to be reset.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapResetPassword configKey="MySFSoapConfig">
        <userId>005XXXXXXXXXXXXXXX</userId>
    </salesforce.soapResetPassword>
    ```

??? note "salesforce.soapRetrieve"
    The `salesforce.soapRetrieve` operation interacts with the Salesforce SOAP API to retrieve one or more records based on their IDs for a specified sObject type. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [retrieve() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_retrieve.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>fieldList</td>
            <td>A comma-separated string of field names to retrieve for the sObject (e.g., <code>Name,Industry,AnnualRevenue</code>).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectType</td>
            <td>The sObject type of the records being retrieved (e.g., <code>Account</code>).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>ids</td>
            <td>An array of one or more record IDs to retrieve.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapRetrieve configKey="MySFSoapConfig">
        <fieldList>Name,Industry,Phone,AnnualRevenue</fieldList>
        <sObjectType>Account</sObjectType>
        <ids>
            <id>001XXXXXXXXXXXXXXX</id>
            <id>001YYYYYYYYYYYYYYY</id>
        </ids>
    </salesforce.soapRetrieve>
    ```

??? note "salesforce.soapSearch"
    The `salesforce.soapSearch` operation interacts with the Salesforce SOAP API to execute an SOSL search query across multiple sObject types. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [search() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_search.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>searchString</td>
            <td>The SOSL search string (e.g., <code>FIND {Test Company} IN ALL FIELDS RETURNING Account(Name), Contact(FirstName,LastName)</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapSearch configKey="MySFSoapConfig">
        <searchString>FIND {Global Corp} IN NAME FIELDS RETURNING Account(Id, Name), Contact(Id, FirstName, LastName, Email)</searchString>
    </salesforce.soapSearch>
    ```

??? note "salesforce.soapSendEmail"
    The `salesforce.soapSendEmail` operation interacts with the Salesforce SOAP API to send individual emails. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [sendEmail() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_sendemail.htm). This operation is for sending individual emails and does not support mass emails.

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>messages</td>
            <td>An array of SingleEmailMessage objects. Each object defines an email to be sent.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapSendEmail configKey="MySFSoapConfig">
        <messages xsi:type="sf:SingleEmailMessage" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:sf="urn:partner.soap.sforce.com">
            <sf:toAddresses>test@example.com</sf:toAddresses>
            <sf:subject>Sample Email from MI</sf:subject>
            <sf:plainTextBody>This is a test email sent via WSO2 MI Salesforce Connector.</sf:plainTextBody>
        </messages>
    </salesforce.soapSendEmail>
    ```

??? note "salesforce.soapSendEmailMessage"
    The `salesforce.soapSendEmailMessage` operation interacts with the Salesforce SOAP API to send email messages that have been saved as EmailMessage sObjects. This is different from `sendEmail` as it operates on existing EmailMessage records. Refer to the Salesforce SOAP API Developer Guide for details on the `sendEmailMessage()` call.

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>ids</td>
            <td>An array of EmailMessage record IDs to send.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapSendEmailMessage configKey="MySFSoapConfig">
        <ids>
            <id>02sXXXXXXXXXXXXXXX</id> <!-- ID of an EmailMessage record -->
        </ids>
    </salesforce.soapSendEmailMessage>
    ```

??? note "salesforce.soapSetPassword"
    The `salesforce.soapSetPassword` operation interacts with the Salesforce SOAP API to set the password for a user. This is typically used by administrators. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [setPassword() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_setpassword.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>userId</td>
            <td>The ID of the user whose password is to be set.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>password</td>
            <td>The new password for the user.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapSetPassword configKey="MySFSoapConfig">
        <userId>005XXXXXXXXXXXXXXX</userId>
        <password>NewSecurePassword123!</password>
    </salesforce.soapSetPassword>
    ```

??? note "salesforce.soapUndelete"
    The `salesforce.soapUndelete` operation interacts with the Salesforce SOAP API to restore records from the Recycle Bin. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [undelete() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_undelete.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>ids</td>
            <td>An array of record IDs to restore from the Recycle Bin.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapUndelete configKey="MySFSoapConfig">
        <ids>
            <id>001XXXXXXXXXXXXXXX</id> <!-- ID of a record in Recycle Bin -->
        </ids>
    </salesforce.soapUndelete>
    ```

??? note "salesforce.soapUpdate"
    The `salesforce.soapUpdate` operation interacts with the Salesforce SOAP API to update existing records. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [update() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_update.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjects</td>
            <td>An array of one or more sObjects to update. Each sObject must include its ID.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapUpdate configKey="MySFSoapConfig">
        <sObjects>
            <sObject xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="sf:Account" xmlns:sf="urn:sobject.partner.soap.sforce.com">
                <sf:Id>001XXXXXXXXXXXXXXX</sf:Id>
                <sf:Phone>(415) 555-1212</sf:Phone>
                <sf:Description>Updated account information.</sf:Description>
            </sObject>
        </sObjects>
    </salesforce.soapUpdate>
    ```

??? note "salesforce.soapUpsert"
    The `salesforce.soapUpsert` operation interacts with the Salesforce SOAP API to create new records or update existing ones based on an external ID field. Refer to the Salesforce SOAP API Developer Guide for detailed information on its functionality and parameters, specifically the [upsert() call](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_upsert.htm).

    **Parameters:**

    Details on parameters for this operation should be obtained from the Salesforce SOAP API documentation.

    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFSoapConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>externalIDFieldName</td>
            <td>The name of the External ID field to use for matching records.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjects</td>
            <td>An array of one or more sObjects to upsert. Each sObject must include the external ID field.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample Configuration:**
    ```xml
    <salesforce.soapUpsert configKey="MySFSoapConfig">
        <externalIDFieldName>MyExternalId__c</externalIDFieldName>
        <sObjects>
            <sObject xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="sf:Account" xmlns:sf="urn:sobject.partner.soap.sforce.com">
                <sf:MyExternalId__c>EXT-12345</sf:MyExternalId__c>
                <sf:Name>Upsert Account Test</sf:Name>
                <sf:Industry>Manufacturing</sf:Industry>
            </sObject>
        </sObjects>
    </salesforce.soapUpsert>
    ```

## REST API Operations

### AppMenu Operations

??? note "salesforce.listItemsInMenu"
    The `salesforce.listItemsInMenu` operation retrieves a list of items in either the Salesforce app drop-down menu or the Salesforce1 navigation menu.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>menuType</td>
            <td>The type of the menu, either <code>AppSwitcher</code> or <code>Salesforce1</code>.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.listItemsInMenu configKey="MySFConfig">
        <menuType>{$ctx:menuType}</menuType>
    </salesforce.listItemsInMenu>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "menuType": "AppSwitcher"
    }
    ```

    **Sample Response:**
    ```json
    {"NetworkTabs":"/services/data/v32.0/appMenu/NetworkTabs","Salesforce1":"/services/data/v32.0/appMenu/Salesforce1","AppSwitcher":"/services/data/v32.0/appMenu/AppSwitcher"}
    ```

    **Related Salesforce documentation:**
    [App Menu Resources](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_appmenu.htm)

??? note "salesforce.tabs"
    The `salesforce.tabs` operation retrieves a list of all tabs.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.tabs configKey="MySFConfig"/>
    ```

    **Sample Request (JSON payload for the proxy - no specific parameters needed beyond configuration):**
    ```json
    {}
    ```

    **Sample Response:**
    ```json
    {"output":"[{\"colors\":[{\"color\":\"4dca76\",\"context\":\"primary\",\"theme\":\"theme4\"},{\"color\":\"319431\",\"context\":\"primary\",\"theme\":\"theme3\"}],\"custom\":true,\"iconUrl\":\"https://your-instance.my.salesforce.com/img/icon/form32.png\",..}]"}
    ```

    **Related Salesforce documentation:**
    [Tabs Resources](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_tabs.htm)

??? note "salesforce.themes"
    The `salesforce.themes` operation retrieves a list of icons and colors used by themes in the Salesforce application.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.themes configKey="MySFConfig"/>
    ```

    **Sample Request (JSON payload for the proxy - no specific parameters needed beyond configuration):**
    ```json
    {}
    ```

    **Sample Response:**
    ```json
    {
       "themeItems":[
          {
             "name":"Account",
             "icons":[
                {
                   "width":32,
                   "theme":"theme3",
                   "contentType":"image/png",
                   "url":"https://your-instance.my.salesforce.com/img/icon/accounts32.png",
                   "height":32
                }
             ]
          }
       ]
    }
    ```

    **Related Salesforce documentation:**
    [Themes Resources](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_themes.htm)

### Approval Operations

??? note "salesforce.listApprovals"
    The `salesforce.listApprovals` operation retrieves a list of approvals in Salesforce. This can include items pending approval by the current user or approvals related to a specific context (e.g., a particular record). Refer to the Salesforce documentation for more details on the specific items returned.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <!-- Add other specific parameters for listApprovals if any, e.g., sObjectName, ids, skip, etc. based on API capabilities -->
        <!-- For now, assuming it might take general query parameters or none for a default list -->
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.listApprovals configKey="MySFConfig"/>
    ```

    **Sample Request (JSON payload for the proxy - if any specific parameters are needed beyond configuration):**
    ```json
    {}
    ```
    If the operation supports filtering (e.g., by sObject type or record IDs), the payload would include those:
    ```json
    {
      "sObjectName": "Opportunity",
      "ids": ["006XXXXXXXXXXXXXXX", "006YYYYYYYYYYYYYYY"]
    }
    ```

    **Sample Response:**
    The exact structure can vary. It typically returns a list of approval processes or items.
    ```json
    {
       "approvals": {
           // Structure depends on Salesforce API version and specific request
           // Might include process instances, work items, etc.
           "currentpage": null,
           "nextpage": null,
           "approvalProcessNodes": []
       }
    }
    ```
    A more concrete example from Salesforce documentation for a specific approval query:
    ```json
    {
      "size" : 1,
      "totalSize" : 1,
      "done" : true,
      "queryLocator" : null,
      "entityTypeName" : "ProcessInstanceWorkitem",
      "records" :
      [
        {
          "attributes" :
          {
            "type" : "ProcessInstanceWorkitem",
            "url" : "/services/data/vXX.X/sobjects/ProcessInstanceWorkitem/04iD0000000ABCDFGH"
          },
          "Id" : "04iD0000000ABCDFGH",
          "ProcessInstance" :
          {
            "attributes" :
            {
              "type" : "ProcessInstance",
              "url" : "/services/data/vXX.X/sobjects/ProcessInstance/04gD0000000IJKLMNOP"
            },
            "TargetObject" :
            {
              "attributes" :
              {
                "type" : "Opportunity",
                "url" : "/services/data/vXX.X/sobjects/Opportunity/006D0000000pQRSTUVWXYZ"
              },
              "Name" : "Big Deal"
            },
            "Status" : "Pending"
          },
          "Actor" :
          {
            "attributes" :
            {
              "type" : "User",
              "url" : "/services/data/vXX.X/sobjects/User/005D0000000qrstuvwxyz"
            },
            "Name" : "Mary Jones"
          }
        }
      ]
    }
    ```

    **Related Salesforce documentation:**
    [Process and Approval Resources](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_process_approvals.htm)

### Event Monitoring Operations

??? note "salesforce.describeEventMonitoring"
    The `salesforce.describeEventMonitoring` operation retrieves the metadata for EventLogFile objects, which includes information about the available event types and their fields.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.describeEventMonitoring configKey="MySFConfig"/>
    ```

    **Sample Request (JSON payload for the proxy - no specific parameters needed):**
    ```json
    {}
    ```

    **Sample Response:**
    ```json
    {
       "objectDescribe": {
           "name": "EventLogFile",
           "label": "Event Log File",
           "fields": [
              {"name": "Id", "type": "id", "label": "Event Log File ID"},
              {"name": "EventType", "type": "picklist", "label": "Event Type"},
              {"name": "LogDate", "type": "datetime", "label": "Log Date"},
              {"name": "LogFileLength", "type": "double", "label": "Log File Length"},
              {"name": "ApiVersion", "type": "double", "label": "API Version"},
              {"name": "LogFile", "type": "string", "label": "Log File Data (URL)"}
              // ... and other fields
           ],
           // ... other object metadata
           "labelPlural":"Event Log Files"
       },
       "recentItems": []
    }
    ```
    (Note: The actual response for `describe` might be more aligned with standard sObject describe results rather than the example previously shown. The above is a more typical describe response.)

    **Related Salesforce documentation:**
    [Describe EventLogFile](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_event_log_file_describe.htm) (The old link seems to point to this, which is an sObject describe) or generally [EventLogFile documentation](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_eventlogfile.htm).

??? note "salesforce.queryEventMonitoringData"
    The `salesforce.queryEventMonitoringData` operation retrieves event log data by executing a SOQL query against the EventLogFile object.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>queryStringForEventMonitoringData</td>
            <td>The SOQL query to execute against the EventLogFile object (e.g., <code>SELECT EventType, LogDate, LogFile FROM EventLogFile WHERE EventType = 'API' AND LogDate = YESTERDAY</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.queryEventMonitoringData configKey="MySFConfig">
        <queryStringForEventMonitoringData>{$ctx:queryStringForEventMonitoringData}</queryStringForEventMonitoringData>
    </salesforce.queryEventMonitoringData>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "queryStringForEventMonitoringData": "SELECT Id, EventType, LogFile, LogDate, LogFileLength FROM EventLogFile WHERE LogDate > YESTERDAY AND EventType = 'API'"
    }
    ```

    **Sample Response:**
    ```json
    {
       "totalSize" : 1,
       "done" : true,
       "records" : [
         {
           "attributes" : {
             "type" : "EventLogFile",
             "url" : "/services/data/v59.0/sobjects/EventLogFile/0ATD000000001bROAQ"
           },
           "Id" : "0ATD000000001bROAQ",
           "EventType" : "API",
           "LogFile" : "/services/data/v59.0/sobjects/EventLogFile/0ATD000000001bROAQ/LogFile",
           "LogDate" : "2024-03-14T00:00:00.000+0000",
           "LogFileLength" : 2692.0
         }
         // ... more records if applicable
       ]
    }
    ```

    **Related Salesforce documentation:**
    [Query EventLogFile](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_event_log_file_query.htm) and [EventLogFile Object Reference](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_eventlogfile.htm).

### Invocable Actions Operations

??? note "salesforce.getListOfAction"
    The `salesforce.getListOfAction` operation retrieves a list of general action types (e.g., standard, custom) available for the current organization.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.getListOfAction configKey="MySFConfig"/>
    ```

    **Sample Request (JSON payload for the proxy - no specific parameters needed):**
    ```json
    {}
    ```

    **Sample Response:**
    ```json
    {
       "standard":"/services/data/vXX.X/actions/standard",
       "custom":"/services/data/vXX.X/actions/custom"
    }
    ```

    **Related Salesforce documentation:**
    [Invocable Actions Resource](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_actions_invocable.htm)

??? note "salesforce.getSpecificListOfAction"
    The `salesforce.getSpecificListOfAction` operation retrieves a list of specific actions (e.g., standard actions like `chatterPost`, `emailSimple`) that can be statically invoked, providing basic information for each.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>actionType</td>
            <td>The type of invocable actions to list (e.g., <code>standard</code>, <code>custom</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.getSpecificListOfAction configKey="MySFConfig">
        <actionType>{$ctx:actionType}</actionType>
    </salesforce.getSpecificListOfAction>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "actionType": "standard"
    }
    ```

    **Sample Response (for `actionType: "standard"`):**
    ```json
    [
        {
            "label": "Post to Chatter",
            "name": "chatterPost",
            "type": "CHATTERPOST",
            "urls": {
                "action": "/services/data/vXX.X/actions/standard/chatterPost"
            }
        },
        {
            "label": "Send Email",
            "name": "emailSimple",
            "type": "EMAILSIMPLE",
            "urls": {
                "action": "/services/data/vXX.X/actions/standard/emailSimple"
            }
        }
        // ... more standard actions
    ]
    ```

    **Related Salesforce documentation:**
    [Standard Actions Resource](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_actions_invocable_standard.htm)

??? note "salesforce.getAttributeOfSpecificAction"
    The `salesforce.getAttributeOfSpecificAction` operation retrieves the detailed attributes (metadata) of a single specific action (e.g., `emailSimple` under `standard` actions).

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>actionType</td>
            <td>The type of the action (e.g., <code>standard</code>, <code>custom</code>).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>attribute</td>
            <td>The name of the specific action whose details you want to retrieve (e.g., <code>emailSimple</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.getAttributeOfSpecificAction configKey="MySFConfig">
        <actionType>{$ctx:actionType}</actionType>
        <attribute>{$ctx:attribute}</attribute>
    </salesforce.getAttributeOfSpecificAction>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "actionType": "standard",
      "attribute": "emailSimple"
    }
    ```

    **Sample Response (for `actionType: "standard", attribute: "emailSimple"`):**
    ```json
    {
        "actionType": "EMAILSIMPLE",
        "description": "Send an email",
        "inputFieldMetadata": [
            {
                "defaultValue": null,
                "description": "Blind Carbon Copy Addresses",
                "label": "EmailBccAddress",
                "name": "bccAddresses",
                "required": false,
                "type": "STRING"
            },
            // ... other input fields like ccAddresses, htmlBody, subject, toAddresses etc.
        ],
        "label": "Send Email",
        "name": "emailSimple",
        "outputFieldMetadata": [],
        "urls": {
            "execute": "/services/data/vXX.X/actions/standard/emailSimple"
        }
    }
    ```

    **Related Salesforce documentation:**
    [Standard Action Attributes](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_actions_invocable_standard_action.htm) (The previous link was for the list, this is for a specific action's details)

### Layout Operations

??? note "salesforce.sObjectLayouts"
    The `salesforce.sObjectLayouts` operation returns a list of layouts and descriptions (including for actions) for a specific sObject.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject whose layouts and descriptions you want to retrieve (e.g., <code>Account</code>, <code>MyCustomObject__c</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.sObjectLayouts configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
    </salesforce.sObjectLayouts>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Account"
    }
    ```

    **Sample Response (Structure can be complex, snippet shown):**
    ```json
    {
       "layouts":[
          {
             "id": "00hXXXXXXXXXXXXXXX", // Layout ID
             "name": "Account Layout",
             "detailLayoutSections":[
                {
                   "heading":"Account Information",
                   "columns":2,
                   // ... more section details
                   "layoutRows":[
                      {
                         "layoutItems":[
                            {
                               "label": "Account Name",
                               "layoutComponents": [
                                   { "details": { "name": "Name", "type": "string" } }
                               ]
                               // ... more item details
                            }
                         ]
                      }
                   ]
                }
             ],
             "editLayoutSections": [ /* ... */ ],
             "quickActionList": { /* ... */ },
             "relatedLists": [ /* ... */ ]
          }
       ],
       "recordTypeMappings": [ /* ... */ ],
       "recordTypeSelectorVisibilities": [ /* ... */ ]
    }
    ```

    **Related Salesforce documentation:**
    [sObject Layouts](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_sobject_layouts.htm)

??? note "salesforce.globalSObjectLayouts"
    The `salesforce.globalSObjectLayouts` operation returns descriptions of global publisher layouts. These layouts define the actions available on the global publisher, such as "New Task" or "New Contact".

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.globalSObjectLayouts configKey="MySFConfig"/>
    ```

    **Sample Request (JSON payload for the proxy - no specific parameters needed):**
    ```json
    {}
    ```

    **Sample Response (Structure can be complex, snippet shown):**
    ```json
    {
       "layouts":[
          {
             "id": "00hXXXXXXXXXXXXXXX", // Global Layout ID
             "label": "Global Layout",
             "quickActionList": {
                 "quickActions": [
                     { "name": "NewTask", "type": "QuickAction", "label": "New Task" },
                     { "name": "NewContact", "type": "QuickAction", "label": "New Contact" }
                     // ... other global actions
                 ]
             }
             // ... other layout details
          }
       ]
    }
    ```

    **Related Salesforce documentation:**
    [Global Layouts (Publisher Layouts)](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_sobject_layouts_global.htm) (The previous link `resources_sobject_layouts.htm` might be too generic, this points to global layouts)

??? note "salesforce.compactLayouts"
    The `salesforce.compactLayouts` operation returns a list of compact layouts for one or more specified sObjects. Compact layouts define which fields appear in key places like an sObject's highlights panel.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectNameList</td>
            <td>A comma-separated list of sObject API names whose compact layouts you want to retrieve (e.g., <code>Account,Contact,MyCustomObject__c</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.compactLayouts configKey="MySFConfig">
        <sObjectNameList>{$ctx:sObjectNameList}</sObjectNameList>
    </salesforce.compactLayouts>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectNameList":"Account,User"
    }
    ```

    **Sample Response (Snippet showing structure for "Account"):**
    ```json
    {
       "Account":{
          "name":"SYSTEM", // System default compact layout for Account
          "id":null, // ID is null for system default
          "label":"System Default",
          "actions":[ /* ... actions available on compact layout ... */ ],
          "fieldItems": [
              { "label": "Account Name", "layoutComponents": [ { "details": { "name": "Name" } } ] },
              { "label": "Type", "layoutComponents": [ { "details": { "name": "Type" } } ] }
              // ... other fields in the compact layout
          ],
          "imageItems": [ /* ... image fields ... */ ],
          "objectType":"Account"
       },
       "User": { /* ... compact layout details for User ... */ }
    }
    ```

    **Related Salesforce documentation:**
    [Compact Layouts (for multiple sObjects)](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_compact_layouts.htm)

??? note "salesforce.sObjectApprovalLayouts"
    The `salesforce.sObjectApprovalLayouts` operation returns a list of approval layouts for a specified sObject. Approval layouts define the fields shown when a user is approving a record.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject whose approval layouts you want to retrieve (e.g., <code>Opportunity</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.sObjectApprovalLayouts configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
    </salesforce.sObjectApprovalLayouts>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName":"Opportunity"
    }
    ```

    **Sample Response:**
    ```json
    {
      "approvalLayouts":[
        {
          "id": "00hXXXXXXXXXXXXXXX", // Approval Layout ID
          "label": "Opportunity Approval Layout",
          "name": "Opportunity_Approval_Layout",
          // ... other approval layout details, field lists etc.
          "fieldItems": [
              { "label": "Opportunity Name", "layoutComponents": [ { "details": { "name": "Name" } } ] },
              { "label": "Amount", "layoutComponents": [ { "details": { "name": "Amount" } } ] }
          ]
        }
      ]
    }
    ```
    If no specific approval layouts are defined, it might return `{"approvalLayouts":[]}`.

    **Related Salesforce documentation:**
    [sObject Approval Layouts](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_sobject_approvallayouts.htm)

??? note "salesforce.sObjectCompactLayouts"
    The `salesforce.sObjectCompactLayouts` operation returns a list of all compact layouts defined for a single, specific sObject.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject whose compact layouts you want to retrieve (e.g., <code>Account</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.sObjectCompactLayouts configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
    </salesforce.sObjectCompactLayouts>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName":"Account"
    }
    ```

    **Sample Response (Snippet showing structure):**
    ```json
    {
       "compactLayouts":[
          {
             "name":"SYSTEM", // System Default
             "id":null,
             "label":"System Default",
             "actions":[ /* ... */ ],
             "fieldItems": [ /* ... */ ],
             "imageItems": [ /* ... */ ]
          },
          {
             "name":"My_Custom_Account_Compact_Layout",
             "id":"05HXXXXXXXXXXXXXXX", // ID of custom compact layout
             "label":"My Custom Account Compact Layout",
             "actions":[ /* ... */ ],
             "fieldItems": [ /* ... */ ],
             "imageItems": [ /* ... */ ]
          }
       ],
       "defaultCompactLayoutId": "05HXXXXXXXXXXXXXXX", // ID of the primary compact layout for the current user
       "recordTypeCompactLayoutMappings": [ /* ... mappings for record types ... */ ]
    }
    ```

    **Related Salesforce documentation:**
    [sObject Compact Layouts](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_sobject_compactlayouts.htm)

??? note "salesforce.sObjectNamedLayouts"
    The `salesforce.sObjectNamedLayouts` operation returns information about a specific, alternate named layout for a given sObject (e.g., a layout used for a specific profile or context).

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject (e.g., <code>User</code>, <code>Account</code>).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>layoutName</td>
            <td>The developer name of the specific named layout (e.g., <code>UserAlt</code>, <code>Account-SalesLayout</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.sObjectNamedLayouts configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <layoutName>{$ctx:layoutName}</layoutName>
    </salesforce.sObjectNamedLayouts>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName":"User",
      "layoutName": "UserAlt"
    }
    ```

    **Sample Response (Structure similar to sObjectLayouts, but for the specific named layout):**
    ```json
    {
       // The response here is an array with one element if the named layout exists
       "layouts":[
          {
             "id": "00hYYYYYYYYYYYYYYY", // Named Layout ID
             "name": "UserAlt",
             "detailLayoutSections":[
                {
                   "heading":"About",
                   "columns":2,
                   // ... more section details
                }
             ],
             "editLayoutSections": [ /* ... */ ],
             "relatedLists": [ /* ... */ ]
          }
       ],
       "recordTypeMappings": [ /* ... */ ] // Usually empty for named layouts unless record types are specifically tied to it
    }
    ```

    **Related Salesforce documentation:**
    [sObject Named Layouts](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_sobject_named_layouts.htm)

### List View Operations

??? note "salesforce.listViews"
    The `salesforce.listViews` operation retrieves the list of all available list views for a specified sObject.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject whose list views you want to retrieve (e.g., <code>Account</code>, <code>Contact</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.listViews configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
    </salesforce.listViews>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Account"
    }
    ```

    **Sample Response:**
    ```json
    {
       "done": true,
       "listviews": [
          {
             "developerName": "AllAccounts",
             "id": "00BXXXXXXXXXXXXXXX",
             "label": "All Accounts",
             "soqlCompatible": true,
             "url": "/services/data/vXX.X/sobjects/Account/listviews/00BXXXXXXXXXXXXXXX"
          },
          {
             "developerName": "NewThisWeek",
             "id": "00BYYYYYYYYYYYYYYY",
             "label": "New This Week",
             "soqlCompatible": true,
             "url": "/services/data/vXX.X/sobjects/Account/listviews/00BYYYYYYYYYYYYYYY"
          }
          // ... more list views
       ],
       "nextRecordsUrl": null,
       "size": 2, // Example size
       "sobjectType": "Account"
    }
    ```

    **Related Salesforce documentation:**
    [List Views Metadata](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_listviews.htm)

??? note "salesforce.listViewById"
    The `salesforce.listViewById` operation retrieves basic information about a single, specific list view for the specified sObject, using the list view's ID.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject to which the list view belongs.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>listViewId</td>
            <td>The ID of the specific list view whose information you want to retrieve.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.listViewById configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <listViewId>{$ctx:listViewId}</listViewId>
    </salesforce.listViewById>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Account",
      "listViewId": "00BXXXXXXXXXXXXXXX"
    }
    ```

    **Sample Response:**
    ```json
    {
       "describeUrl": "/services/data/vXX.X/sobjects/Account/listviews/00BXXXXXXXXXXXXXXX/describe",
       "developerName": "NewThisWeek",
       "id": "00BXXXXXXXXXXXXXXX",
       "label": "New This Week",
       "resultsUrl": "/services/data/vXX.X/sobjects/Account/listviews/00BXXXXXXXXXXXXXXX/results",
       "soqlCompatible": true,
       "url": "/services/data/vXX.X/sobjects/Account/listviews/00BXXXXXXXXXXXXXXX"
    }
    ```

    **Related Salesforce documentation:**
    [List View Metadata by ID](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_listview_id.htm)

??? note "salesforce.recentListViews"
    The `salesforce.recentListViews` operation retrieves the list of recently used list views for the given sObject type for the context user.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject whose recently used list views you want to retrieve.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.recentListViews configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
    </salesforce.recentListViews>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Account"
    }
    ```

    **Sample Response (similar to `listViews` but filtered for recent views):**
    ```json
    {
       "done": true,
       "listviews": [
          {
             "developerName": "MyRecentAccounts",
             "id": "00BZZZZZZZZZZZZZZZ",
             "label": "My Recent Accounts",
             "soqlCompatible": true,
             "url": "/services/data/vXX.X/sobjects/Account/listviews/00BZZZZZZZZZZZZZZZ"
          }
          // ... other recent list views
       ],
       "nextRecordsUrl": null,
       "size": 1,
       "sobjectType": "Account"
    }
    ```

    **Related Salesforce documentation:**
    [Recent List Views](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_recentlistviews.htm)

??? note "salesforce.describeListViewById"
    The `salesforce.describeListViewById` operation returns detailed information about a specific list view, including its ID, the columns it displays, and the underlying SOQL query.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject to which the list view applies.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>listViewId</td>
            <td>The ID of the list view to describe.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.describeListViewById configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <listViewId>{$ctx:listViewId}</listViewId>
    </salesforce.describeListViewById>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Account",
      "listViewId": "00BXXXXXXXXXXXXXXX"
    }
    ```

    **Sample Response:**
    ```json
    {
       "columns": [
          {"fieldNameOrPath": "Name", "label": "Account Name", /* ... */},
          {"fieldNameOrPath": "BillingCity", "label": "Billing City", /* ... */}
       ],
       "id": "00BXXXXXXXXXXXXXXX",
       "label": "New This Week",
       "developerName": "NewThisWeek",
       "orderBy": [ {"fieldNameOrPath": "Name", "sortDirection": "ascending", "nullsPosition":"first"} ],
       "query": "SELECT Name, BillingCity, Id FROM Account WHERE CreatedDate = THIS_WEEK ORDER BY Name ASC NULLS FIRST",
       "scope": "Everything", // e.g., Everything, Mine, Team's
       "sobjectType": "Account",
       "whereCondition": { /* ... details of the filter conditions ... */ }
    }
    ```

    **Related Salesforce documentation:**
    [Describe List View](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_listviewdescribe.htm)

??? note "salesforce.listViewResults"
    The `salesforce.listViewResults` operation executes the SOQL query defined for a given list view and returns the resulting data records along with presentation information.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject to which the list view applies.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>listViewId</td>
            <td>The ID of the list view whose results are to be fetched.</td>
            <td>Yes</td>
        </tr>
        <!-- Optional parameters like pageSize, offset can be added here if supported by the API for this endpoint -->
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.listViewResults configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <listViewId>{$ctx:listViewId}</listViewId>
    </salesforce.listViewResults>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Account",
      "listViewId": "00BXXXXXXXXXXXXXXX"
    }
    ```

    **Sample Response:**
    ```json
    {
       "columns": [
          {"fieldNameOrPath": "Name", "label": "Account Name", /* ... */ "type": "string"},
          {"fieldNameOrPath": "BillingCity", "label": "Billing City", /* ... */ "type": "string"}
       ],
       "developerName": "NewThisWeek",
       "done": true,
       "id": "00BXXXXXXXXXXXXXXX",
       "label": "New This Week",
       "records": [
          {
             "attributes": {"type": "Account", "url": "/services/data/vXX.X/sobjects/Account/001YYYYYYYYYYYYYY1"},
             "Id": "001YYYYYYYYYYYYYY1",
             "Name": "Sample Account 1",
             "BillingCity": "San Francisco"
          },
          {
             "attributes": {"type": "Account", "url": "/services/data/vXX.X/sobjects/Account/001YYYYYYYYYYYYYY2"},
             "Id": "001YYYYYYYYYYYYYY2",
             "Name": "Another Account Inc",
             "BillingCity": "New York"
          }
       ],
       "size": 2 // Number of records returned in this batch
    }
    ```

    **Related Salesforce documentation:**
    [List View Results](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_listviewresults.htm)

### Process Rule Operations

??? note "salesforce.listProcessRules"
    The `salesforce.listProcessRules` operation retrieves a list of all process rules in the organization. This can include workflow rules, approval processes, and other types of process automation rules.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.listProcessRules configKey="MySFConfig"/>
    ```

    **Sample Request (JSON payload for the proxy - no specific parameters needed):**
    ```json
    {}
    ```

    **Sample Response:**
    The response structure can vary based on the types of process rules in the org. It typically returns a list of rule metadata.
    ```json
    {
       "rules": [
         {
           "id": "01QD0000000APliMAG",
           "name": "Sample Workflow Rule",
           "object": "Account",
           "active": true
           // ... other rule metadata
         },
         {
           "id": "04gD0000000IKLpIAO",
           "name": "Sample Approval Process",
           "object": "Opportunity",
           "active": true
           // ... other rule metadata
         }
       ]
    }
    ```
    (The original sample `{"rules":{}}` was generic; the above is a more illustrative example of what might be returned.)

    **Related Salesforce documentation:**
    [Process Rules Resource](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_process_rules.htm)

??? note "salesforce.getSpecificProcessRule"
    The `salesforce.getSpecificProcessRule` operation retrieves the metadata for a specific sObject process rule (e.g., a workflow rule) using its ID.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject to which the process rule applies (e.g., <code>Account</code>, <code>Opportunity</code>).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>workflowRuleId</td>
            <td>The ID of the process rule (WorkflowRule ID, ApprovalProcess ID, etc.) whose metadata you want to retrieve.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.getSpecificProcessRule configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <workflowRuleId>{$ctx:workflowRuleId}</workflowRuleId>
    </salesforce.getSpecificProcessRule>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Account",
      "workflowRuleId": "01QD0000000APliMAG"
    }
    ```

    **Sample Response (for a Workflow Rule):**
    ```json
    {
      "actions": [
        {
          "id": "01VD0000000D2w7IAS", // e.g., ID of a field update or email alert
          "name": "Update_Account_Description", // Name of the action
          "type": "FieldUpdate" // Type of workflow action
        }
      ],
      "description": "This rule updates account description on certain criteria.",
      "id": "01QD0000000APliMAG", // WorkflowRule ID
      "name": "My Account Workflow Rule",
      "namespacePrefix": null,
      "object": "Account", // sObject API name
      "active": true,
      "triggerType": "onAllChanges", // e.g., onAllChanges, onمانCreateOnly, onمانCreateAndUpdateToMeetCriteria
      "workflowType": "Rule" // Indicates it's a workflow rule
      // ... other metadata specific to the rule type
    }
    ```

    **Related Salesforce documentation:**
    [Process Rule Detail Resource](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_process_rules_particular.htm) (The link mentions "Salesforce Bulk documentation" in the original, but it's a REST API resource).

### Query Operations

??? note "salesforce.query"
    The `salesforce.query` operation executes a SOQL query to retrieve data from Salesforce sObjects. It does not return records that have been deleted (i.e., are in the Recycle Bin).

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>queryString</td>
            <td>The SOQL query string (e.g., <code>SELECT Id, Name FROM Account WHERE Industry = 'Technology'</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.query configKey="MySFConfig">
        <queryString>{$ctx:queryString}</queryString>
    </salesforce.query>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "queryString": "SELECT Id, Name, AnnualRevenue FROM Account WHERE AnnualRevenue > 5000000"
    }
    ```

    **Sample Response:**
    ```json
    {
        "done": false,
        "totalSize": 150,
        "nextRecordsUrl": "/services/data/vXX.X/query/01gD0000002HU6KIAW-200", // Present if more records exist
        "records": [
            {
                "attributes": { "type": "Account", "url": "/services/data/vXX.X/sobjects/Account/001D000000IRFmaIAH" },
                "Id": "001D000000IRFmaIAH",
                "Name": "Big Corp",
                "AnnualRevenue": 60000000
            }
            // ... more records up to the batch size
        ]
    }
    ```

    **Related Salesforce documentation:**
    [Query Records (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_query.htm)

??? note "salesforce.queryAll"
    The `salesforce.queryAll` operation executes a SOQL query, similar to `salesforce.query`, but it also includes records that have been deleted and are in the Recycle Bin, as well as archived Task and Event records.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>queryString</td>
            <td>The SOQL query string. To see deleted records, you might need to add <code>IsDeleted = true</code> to your WHERE clause or query for specific records by ID.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.queryAll configKey="MySFConfig">
        <queryString>{$ctx:queryString}</queryString>
    </salesforce.queryAll>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "queryString": "SELECT Id, Name, IsDeleted FROM Account WHERE Name LIKE 'Old Test Company%'"
    }
    ```

    **Sample Response (may include records where `IsDeleted` is true):**
    ```json
    {
        "done": true,
        "totalSize": 1,
        "records": [
            {
                "attributes": { "type": "Account", "url": "/services/data/vXX.X/sobjects/Account/001D000000JsmplIAB" },
                "Id": "001D000000JsmplIAB",
                "Name": "Old Test Company Obsolete",
                "IsDeleted": true
            }
        ]
    }
    ```

    **Related Salesforce documentation:**
    [Query All Records (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_queryall.htm)

??? note "salesforce.queryMore"
    The `salesforce.queryMore` operation retrieves the next batch of records if a previous `salesforce.query` operation returned a `nextRecordsUrl` (indicating that the full result set was too large for a single response). It does not retrieve deleted records.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>nextRecordsUrl</td>
            <td>The query identifier (the value of `nextRecordsUrl` from the previous `query` or `queryMore` response).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.queryMore configKey="MySFConfig">
        <nextRecordsUrl>{$ctx:nextRecordsUrlFromPreviousQuery}</nextRecordsUrl>
    </salesforce.queryMore>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "nextRecordsUrl": "/services/data/vXX.X/query/01gD0000002HU6KIAW-200"
    }
    ```

    **Sample Response (similar to `query`, potentially with `done: true` if it's the last batch):**
    ```json
    {
        "done": true,
        "totalSize": 150, // Still shows total size of original query
        "records": [
            // ... next batch of records
        ]
    }
    ```

    **Related Salesforce documentation:**
    [Query More Records](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_querymore.htm)

??? note "salesforce.queryAllMore"
    The `salesforce.queryAllMore` operation retrieves the next batch of records if a previous `salesforce.queryAll` operation returned a `nextRecordsUrl`. This includes deleted records.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>nextRecordsUrl</td>
            <td>The query identifier from the previous `queryAll` or `queryAllMore` response.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.queryAllMore configKey="MySFConfig">
        <nextRecordsUrl>{$ctx:nextRecordsUrlFromPreviousQueryAll}</nextRecordsUrl>
    </salesforce.queryAllMore>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "nextRecordsUrl": "/services/data/vXX.X/queryAll/01gD0000002HU7KIBX-500"
    }
    ```

    **Sample Response (similar to `queryAll`):**
    ```json
    {
        "done": true,
        "totalSize": 25, // Total size of original queryAll
        "records": [
            // ... next batch of records, potentially including deleted ones
        ]
    }
    ```

    **Related Salesforce documentation:**
    [Query More (for queryAll)](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_queryallmore.htm)


??? note "salesforce.queryPerformanceFeedback"
    The `salesforce.queryPerformanceFeedback` operation (using the `explain` resource with a SOQL query) provides feedback on how Salesforce will execute your query, including information about index usage and potential performance bottlenecks.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>queryString</td>
            <td>The SOQL query string for which to get performance feedback.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.queryPerformanceFeedback configKey="MySFConfig">
        <queryString>{$ctx:queryString}</queryString>
    </salesforce.queryPerformanceFeedback>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "queryString": "SELECT Id, Name FROM Account WHERE Industry = 'Media' AND NumberOfEmployees > 5000"
    }
    ```

    **Sample Response:**
    ```json
    {
       "plans": [
          {
             "cardinality": 100, // Estimated number of records returned by this plan
             "fields": ["Industry", "NumberOfEmployees"], // Fields used in filters
             "leadingOperationType": "Index", // e.g., Index, TableScan
             "notes": [ // Potential notes about performance
                {
                   "description": "Query will use an index on Industry.",
                   "fields": ["Industry"],
                   "tableEnumOrId": "Account"
                }
             ],
             "relativeCost": 0.85, // Relative cost of this plan
             "sobjectCardinality": 50000, // Total records in the sObject
             "sobjectType": "Account"
          }
          // ... potentially other plans if Salesforce considers multiple execution paths
       ]
    }
    ```

    **Related Salesforce documentation:**
    [SOQL Query Plan (Explain Resource)](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_query_explain.htm)

??? note "salesforce.listviewQueryPerformanceFeedback"
    The `salesforce.listviewQueryPerformanceFeedback` operation (using the `explain` resource with a List View ID) retrieves query performance feedback for the SOQL query underlying a Salesforce report or list view.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>listViewId</td>
            <td>The ID of the report or list view for which to get query performance feedback.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.listviewQueryPerformanceFeedback configKey="MySFConfig">
        <listViewId>{$ctx:listViewId}</listViewId>
    </salesforce.listviewQueryPerformanceFeedback>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "listViewId": "00BXXXXXXXXXXXXXXX"
    }
    ```

    **Sample Response (similar to `queryPerformanceFeedback`):**
    ```json
    {
       "plans": [
          {
             "leadingOperationType": "Index",
             "relativeCost": 0.5,
             "sobjectCardinality": 10000,
             "fields": ["Status"], // Example field used by the list view's filter
             "cardinality": 50,
             "sobjectType": "Case" // Example sObject for the list view
          }
       ]
    }
    ```

    **Related Salesforce documentation:**
    [List View / Report Query Plan (Explain Resource)](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_query_explain_listview_report.htm) (The previous link was generic dome_query_explain)

### Quick Action Operations

??? note "salesforce.quickActions"
    The `salesforce.quickActions` operation retrieves a list of available global Quick Actions. These are actions not tied to a specific sObject context.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.quickActions configKey="MySFConfig"/>
    ```

    **Sample Request (JSON payload for the proxy - no specific parameters needed):**
    ```json
    {}
    ```

    **Sample Response:**
    ```json
    [
        {
            "label": "New Task",
            "name": "NewTask",
            "type": "Create", // Type of action (Create, Update, LogACall, Custom, etc.)
            "urls": {
                "describe": "/services/data/vXX.X/quickActions/NewTask/describe",
                "defaultValues": "/services/data/vXX.X/quickActions/NewTask/defaultValues",
                "execute": "/services/data/vXX.X/quickActions/NewTask"
            }
        },
        {
            "label": "Log a Call",
            "name": "LogACall",
            "type": "LogACall",
            "urls": { /* ... */ }
        }
        // ... more global quick actions
    ]
    ```
    (The original sample response `{"output":"[...]"}` was corrected to be a valid JSON array.)

    **Related Salesforce documentation:**
    [Global Quick Actions](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_quickactions.htm)

??? note "salesforce.sObjectQuickActions"
    The `salesforce.sObjectQuickActions` operation retrieves a list of object-specific Quick Actions available for a given sObject type.
    (Note: The original doc used `sObjectAction` for the operation name, but the endpoint is typically `/sobjects/{sObjectName}/quickActions`. Renaming to `sObjectQuickActions` for clarity.)

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject for which you want to retrieve a list of quick actions (e.g., <code>Account</code>, <code>Case</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.sObjectQuickActions configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
    </salesforce.sObjectQuickActions>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Account"
    }
    ```

    **Sample Response (for Account sObject):**
    ```json
    [
        {
            "label": "New Contact", // Action specific to Account
            "name": "NewContact",   // Could be Account.NewContact or a custom name
            "type": "Create",
            "urls": {
                "describe": "/services/data/vXX.X/sobjects/Account/quickActions/NewContact/describe",
                "defaultValues": "/services/data/vXX.X/sobjects/Account/quickActions/NewContact/defaultValues",
                "execute": "/services/data/vXX.X/sobjects/Account/quickActions/NewContact"
            }
        }
        // ... more quick actions for the specified sObject
    ]
    ```

    **Related Salesforce documentation:**
    [sObject Quick Actions](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_sobject_quickactions.htm)

??? note "salesforce.getSpecificQuickAction"
    The `salesforce.getSpecificQuickAction` operation retrieves metadata for a specific Quick Action, whether global or sObject-specific. The `actionName` should be the fully qualified name if it's an sObject action (e.g., `Account.MyCustomAction`).

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject if retrieving an sObject-specific action. Omit for global actions.</td>
            <td>No (Yes if action is sObject-specific)</td>
        </tr>
        <tr>
            <td>actionName</td>
            <td>The API name of the Quick Action (e.g., <code>LogACall</code>, <code>Case.Escalate</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration (Global Action):**
    ```xml
    <salesforce.getSpecificQuickAction configKey="MySFConfig">
        <actionName>{$ctx:actionName}</actionName>
    </salesforce.getSpecificQuickAction>
    ```
    **Sample XML Configuration (sObject-Specific Action):**
    ```xml
    <salesforce.getSpecificQuickAction configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <actionName>{$ctx:actionName}</actionName>
    </salesforce.getSpecificQuickAction>
    ```

    **Sample Request (JSON for a global action):**
    ```json
    {
      "actionName": "LogACall"
    }
    ```
    **Sample Request (JSON for an sObject-specific action):**
    ```json
    {
      "sObjectName": "Account",
      "actionName": "Account.QuickUpdate"
    }
    ```

    **Sample Response:**
    ```json
    {
       "label": "Log a Call",
       "name": "LogACall", // Or qualified name like "Account.QuickUpdate"
       "type": "LogACall",
       "iconUrl": "https://your-instance.my.salesforce.com/img/icon/log_a_call_32.png",
       "targetSobjectType": "Task", // sObject this action primarily interacts with
       "urls": { /* ... URLs for describe, defaultValues, execute ... */ }
       // ... other metadata like miniLayout, targetRecordTypeId etc.
    }
    ```

    **Related Salesforce documentation:**
    [Specific Quick Action](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_quickaction_specific.htm) (global) and [sObject Specific Quick Action](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_sobject_quickaction_specific.htm)

??? note "salesforce.describeSpecificQuickAction"
    The `salesforce.describeSpecificQuickAction` operation retrieves layout metadata and other details for a specific Quick Action.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject if describing an sObject-specific action. Omit for global actions.</td>
            <td>No (Yes if action is sObject-specific)</td>
        </tr>
        <tr>
            <td>actionName</td>
            <td>The API name of the Quick Action.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration (Global Action):**
    ```xml
    <salesforce.describeSpecificQuickAction configKey="MySFConfig">
        <actionName>{$ctx:actionName}</actionName>
    </salesforce.describeSpecificQuickAction>
    ```
    **Sample XML Configuration (sObject-Specific Action):**
    ```xml
    <salesforce.describeSpecificQuickAction configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <actionName>{$ctx:actionName}</actionName>
    </salesforce.describeSpecificQuickAction>
    ```

    **Sample Request (JSON for a global action):**
    ```json
    {
      "actionName": "LogACall"
    }
    ```

    **Sample Response (describes layout, fields, etc.):**
    ```json
    {
       "label": "Log a Call",
       "name": "LogACall",
       "targetSobjectType": "Task",
       "layout": {
           "layoutSections": [
               {
                   "layoutRows": [
                       // ... details of fields in the layout, their properties, etc.
                       { "label": "Subject", "name": "Subject", "type": "string", "required": true },
                       { "label": "Comments", "name": "Description", "type": "textarea" }
                   ]
               }
           ]
       },
       "urls": { /* ... */ }
    }
    ```

    **Related Salesforce documentation:**
    [Describe Specific Quick Action](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_quickaction_describe.htm) (global) and [Describe sObject Specific Quick Action](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_sobject_quickaction_describe.htm)

??? note "salesforce.getDefaultValuesOfQuickAction"
    The `salesforce.getDefaultValuesOfQuickAction` operation retrieves default field values for a specific Quick Action, optionally in the context of a specific record ID if the action is sObject-specific and context-aware.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject if the action is sObject-specific. Omit for global actions.</td>
            <td>No (Yes if action is sObject-specific)</td>
        </tr>
        <tr>
            <td>actionName</td>
            <td>The API name of the Quick Action.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>contextId</td>
            <td>The ID of the context record (e.g., Account ID) if retrieving default values for an sObject-specific action that depends on context.</td>
            <td>No</td>
        </tr>
    </table>

    **Sample XML Configuration (Global Action):**
    ```xml
    <salesforce.getDefaultValuesOfQuickAction configKey="MySFConfig">
        <actionName>{$ctx:actionName}</actionName>
    </salesforce.getDefaultValuesOfQuickAction>
    ```
    **Sample XML Configuration (sObject-Specific Action with context):**
    ```xml
    <salesforce.getDefaultValuesOfQuickAction configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <actionName>{$ctx:actionName}</actionName>
        <contextId>{$ctx:contextId}</contextId>
    </salesforce.getDefaultValuesOfQuickAction>
    ```

    **Sample Request (JSON for a global action):**
    ```json
    {
      "actionName":"LogACall"
    }
    ```
    **Sample Request (JSON for an sObject action with context):**
    ```json
    {
      "sObjectName": "Account",
      "actionName": "Account.LogCall",
      "contextId": "001XXXXXXXXXXXXXXX"
    }
    ```

    **Sample Response:**
    ```json
    {
       "objectInfos": { // If the action creates/updates multiple sObjects
          "Task": {
             "apiName": "Task",
             "fields": {
                "Subject": "Call", // Default value
                "Status": "Not Started"
             }
          }
       },
       // If only one sObject, fields might be at the top level
       "fields": {
           "Subject": "Call",
           "Status": "Not Started"
           // ... other default field values
       },
       "targetSobjectType": "Task" // Or the primary target sObject
    }
    ```
    (Note: The response structure for default values can vary. The `objectInfos` map is used when an action might create multiple records, like a "New Opportunity with Contact" action. Simpler actions might have a flatter `fields` structure.)

    **Related Salesforce documentation:**
    [Quick Action Default Values](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_quickaction_defaultvalues.htm) (global) and [sObject Quick Action Default Values](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_sobject_quickaction_defaultvalues.htm)

### Record Operations

??? note "salesforce.createRecord"
    The `salesforce.createRecord` operation creates a new record for a specified sObject type.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject for which to create a record (e.g., <code>Account</code>, <code>Contact</code>, <code>MyCustomObject__c</code>).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>fieldAndValue</td>
            <td>A JSON object containing the fields and their values for the new record. Ensure all mandatory fields for the sObject are included.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.createRecord configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <fieldAndValue>{$ctx:fieldAndValue}</fieldAndValue>
    </salesforce.createRecord>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Account",
      "fieldAndValue": {
        "Name": "WSO2",
        "Description": "This Account belongs to WSO2",
        "Industry": "Technology",
        "NumberOfEmployees": 1000
      }
    }
    ```

    **Sample Response:**
    ```json
    {
       "id": "001XXXXXXXXXXXXXXX", // ID of the newly created record
       "success": true,
       "errors": []
    }
    ```

    **Related Salesforce documentation:**
    [Create an sObject Record](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)

??? note "salesforce.getRecord"
    The `salesforce.getRecord` operation retrieves a specific record by its ID for a specified sObject type, allowing you to select which fields to return.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>recordId</td>
            <td>The ID of the record to retrieve.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>fields</td>
            <td>Optional. A comma-separated list of field API names to retrieve (e.g., <code>Name,Industry,AnnualRevenue</code>). If not specified, Salesforce typically returns all fields the user has access to, which can be less performant.</td>
            <td>No</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.getRecord configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <recordId>{$ctx:recordId}</recordId>
        <fields>{$ctx:fields}</fields> <!-- Optional -->
    </salesforce.getRecord>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Account",
      "recordId": "001XXXXXXXXXXXXXXX",
      "fields": "Name,Industry,Phone,Website"
    }
    ```

    **Sample Response:**
    ```json
    {
        "attributes": {
            "type": "Account",
            "url": "/services/data/vXX.X/sobjects/Account/001XXXXXXXXXXXXXXX"
        },
        "Id": "001XXXXXXXXXXXXXXX",
        "Name": "WSO2",
        "Industry": "Technology",
        "Phone": "+1 408 123 4567",
        "Website": "wso2.com"
        // ... other requested fields ...
    }
    ```

    **Related Salesforce documentation:**
    [Retrieve sObject Record Details](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_retrieve_specific_fields.htm)

??? note "salesforce.updateRecord"
    The `salesforce.updateRecord` operation updates an existing record for a specified sObject type.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>recordId</td>
            <td>The ID of the record to update.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>fieldAndValue</td>
            <td>A JSON object containing the fields and their new values for the record. Only fields to be modified need to be included.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.updateRecord configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <recordId>{$ctx:recordId}</recordId>
        <fieldAndValue>{$ctx:fieldAndValue}</fieldAndValue>
    </salesforce.updateRecord>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Account",
      "recordId": "001XXXXXXXXXXXXXXX",
      "fieldAndValue": {
        "Description": "Updated description for WSO2 Account.",
        "Phone": "+1 650 789 0123"
      }
    }
    ```
    Salesforce responds with an HTTP 204 No Content status on successful update.

    **Related Salesforce documentation:**
    [Update an sObject Record](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_update_fields.htm)

??? note "salesforce.deleteRecord"
    The `salesforce.deleteRecord` operation deletes a specified record.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>recordId</td>
            <td>The ID of the record to delete.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.deleteRecord configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <recordId>{$ctx:recordId}</recordId>
    </salesforce.deleteRecord>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Account",
      "recordId": "001XXXXXXXXXXXXXXX"
    }
    ```
    Salesforce responds with an HTTP 204 No Content status on successful deletion.

    **Related Salesforce documentation:**
    [Delete an sObject Record](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_delete_record.htm)

??? note "salesforce.upsertRecord"
    The `salesforce.upsertRecord` operation creates a new record or updates an existing one based on the value of a specified external ID field.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>externalIdFieldName</td>
            <td>The API name of the External ID field on the sObject.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>externalIdValue</td>
            <td>The value of the external ID to match against.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>fieldAndValue</td>
            <td>A JSON object containing the fields and values for the record. If a match is found on the external ID, these fields are updated. If not, a new record is created with these fields (and the external ID field set to `externalIdValue`).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.upsertRecord configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <externalIdFieldName>{$ctx:externalIdFieldName}</externalIdFieldName>
        <externalIdValue>{$ctx:externalIdValue}</externalIdValue>
        <fieldAndValue>{$ctx:fieldAndValue}</fieldAndValue>
    </salesforce.upsertRecord>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "MyCustomObject__c",
      "externalIdFieldName": "LegacySystemID__c",
      "externalIdValue": "LEGACY-00123",
      "fieldAndValue": {
        "Name": "Upserted Record",
        "CustomField__c": "Some Value"
      }
    }
    ```

    **Sample Response (on create):**
    ```json
    {
        "id": "a01XXXXXXXXXXXXXXX", // ID of the created record
        "success": true,
        "errors": [],
        "created": true
    }
    ```
    **Sample Response (on update):**
    An HTTP 204 No Content status is returned if the record was updated. If `created` is true in response, it was an insert.

    **Related Salesforce documentation:**
    [Upsert an sObject Record](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_upsert.htm)

??? note "salesforce.createMultipleRecords"
    The `salesforce.createMultipleRecords` operation creates multiple records of the same sObject type in a single request using the Composite API. This is more efficient than making individual create calls.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject type for which records are being created.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>records</td>
            <td>A JSON array where each element is a record to be created. Each record object should have an `attributes` field specifying `{"type": "sObjectApiName", "referenceId": "uniqueRefId"}` and then the fields for that record.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>allOrNone</td>
            <td>Boolean. If `true`, all records must process successfully, or none will be committed. If `false` (default), successfully processed records will be committed even if others fail.</td>
            <td>No</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.createMultipleRecords configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName> <!-- Used to set "type" in attributes if not in payload -->
        <records>{$ctx:recordsPayload}</records>
        <allOrNone>false</allOrNone>
    </salesforce.createMultipleRecords>
    ```

    **Sample Request (JSON payload for `recordsPayload` property):**
    ```json
    {
      "allOrNone": false,
      "records": [
        {
          "attributes": {"type": "Account", "referenceId": "refAccount1"},
          "Name": "Bulk Account 1",
          "Industry": "Retail"
        },
        {
          "attributes": {"type": "Account", "referenceId": "refAccount2"},
          "Name": "Bulk Account 2",
          "Phone": "1234567890"
        }
      ]
    }
    ```
    (Note: The `sObjectName` in the XML can be used to default the `type` in `attributes` if not provided in the payload. The payload structure for this operation often directly maps to the Salesforce Composite API's "records" collection resource.)

    **Sample Response:**
    ```json
    {
        "hasErrors": false,
        "results": [
            {
                "id": "001XXXXXXXXXXXXXX1",
                "referenceId": "refAccount1"
            },
            {
                "id": "001XXXXXXXXXXXXXX2",
                "referenceId": "refAccount2"
            }
        ]
    }
    ```

    **Related Salesforce documentation:**
    [Composite API - sObject Collections](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections.htm)

??? note "salesforce.createNestedRecords"
    The `salesforce.createNestedRecords` (SObject Tree) operation creates one or more records, potentially including related child records, in a single request. This is useful for creating a parent record and its children (e.g., an Account and its Contacts) simultaneously.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the root sObject type you are creating (e.g., <code>Account</code>).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>records</td>
            <td>A JSON array containing one or more sObject trees. Each tree starts with a root record, which can have nested child records under a relationship name (e.g., `Contacts` for an Account). Each record should have an `attributes` field specifying `{"type": "sObjectApiName", "referenceId": "uniqueRefId"}`.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.createNestedRecords configKey="MySFConfig">
        <sObjectName>{$ctx:rootSObjectName}</sObjectName> <!-- Root sObject type -->
        <records>{$ctx:recordTreePayload}</records>
    </salesforce.createNestedRecords>
    ```

    **Sample Request (JSON for `recordTreePayload` property):**
    ```json
    {
      "records" :[{
        "attributes" : {"type" : "Account", "referenceId" : "refAccount1"},
        "Name" : "Tree Account 1",
        "Industry" : "Technology",
        "Contacts" : {
          "records" : [{
            "attributes" : {"type" : "Contact", "referenceId" : "refContact1"},
            "LastName" : "Smith",
            "Email" : "jsmith@treeaccount1.com"
          },{
            "attributes" : {"type" : "Contact", "referenceId" : "refContact2"},
            "LastName" : "Jones",
            "Email" : "tjones@treeaccount1.com"
          }]
        }
      }]
    }
    ```

    **Sample Response:**
    ```json
    {
        "hasErrors": false,
        "results": [
            {"id": "001XXXXXXXXXXXXXXA", "referenceId": "refAccount1"},
            {"id": "003XXXXXXXXXXXXXXB", "referenceId": "refContact1"},
            {"id": "003XXXXXXXXXXXXXXC", "referenceId": "refContact2"}
        ]
    }
    ```

    **Related Salesforce documentation:**
    [Composite API - SObject Tree](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobject_tree.htm)

??? note "salesforce.getRecentlyViewedItems"
    The `salesforce.getRecentlyViewedItems` operation retrieves a list of records recently viewed by the logged-in user.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>limit</td>
            <td>Optional. The maximum number of recently viewed items to return. Default is 200.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>since</td>
            <td>Optional. An ISO 8601 formatted date string (e.g., `2023-01-01T00:00:00Z`). Returns items viewed since this date/time.</td>
            <td>No</td>
        </tr>
        <!-- Add sObjectTypes if the API supports filtering by specific sObject types -->
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.getRecentlyViewedItems configKey="MySFConfig">
        <limit>{$ctx:limit}</limit>
    </salesforce.getRecentlyViewedItems>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "limit": 5
    }
    ```

    **Sample Response:**
    ```json
    [
        {
            "attributes": {"type": "Account", "url": "/services/data/vXX.X/sobjects/Account/001XXXXXXXXXXXXXXX"},
            "Id": "001XXXXXXXXXXXXXXX",
            "Name": "Recently Viewed Account"
        },
        {
            "attributes": {"type": "Contact", "url": "/services/data/vXX.X/sobjects/Contact/003YYYYYYYYYYYYYYY"},
            "Id": "003YYYYYYYYYYYYYYY",
            "Name": "Recent Contact Person"
        }
        // ... other recently viewed items
    ]
    ```
    (The original response `{"output":"[...]"}` was corrected to be a valid JSON array.)

    **Related Salesforce documentation:**
    [Recently Viewed Items](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_recent_items.htm)

??? note "salesforce.getDeletedRecords"
    The `salesforce.getDeletedRecords` operation retrieves a list of record IDs that have been deleted for a specific sObject type within a given date/time range.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject for which to retrieve deleted record information.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>startDate</td>
            <td>The start of the date/time range (UTC, ISO 8601 format: `YYYY-MM-DDTHH:mm:ssZ`).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>endDate</td>
            <td>The end of the date/time range (UTC, ISO 8601 format: `YYYY-MM-DDTHH:mm:ssZ`).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.getDeletedRecords configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <startDate>{$ctx:startDate}</startDate>
        <endDate>{$ctx:endDate}</endDate>
    </salesforce.getDeletedRecords>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Account",
      "startDate": "2023-10-01T00:00:00Z",
      "endDate": "2023-10-28T23:59:59Z"
    }
    ```

    **Sample Response:**
    ```json
    {
       "deletedRecords": [
           {
               "id": "001DELETEDXXXXXX1",
               "deletedDate": "2023-10-15T10:30:00.000+0000"
           },
           {
               "id": "001DELETEDXXXXXX2",
               "deletedDate": "2023-10-20T14:00:00.000+0000"
           }
       ],
       "earliestDateAvailable": "2023-09-01T00:00:00.000+0000", // Earliest date for which deletion info is available
       "latestDateCovered": "2023-10-28T23:59:59.000+0000"
    }
    ```

    **Related Salesforce documentation:**
    [Get Deleted Records](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_getdeleted.htm)

??? note "salesforce.getUpdatedRecords"
    The `salesforce.getUpdatedRecords` operation retrieves a list of record IDs that have been created or updated for a specific sObject type within a given date/time range.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject for which to retrieve updated record information.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>startDate</td>
            <td>The start of the date/time range (UTC, ISO 8601 format: `YYYY-MM-DDTHH:mm:ssZ`).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>endDate</td>
            <td>The end of the date/time range (UTC, ISO 8601 format: `YYYY-MM-DDTHH:mm:ssZ`).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.getUpdatedRecords configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <startDate>{$ctx:startDate}</startDate>
        <endDate>{$ctx:endDate}</endDate>
    </salesforce.getUpdatedRecords>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Lead",
      "startDate": "2023-10-27T00:00:00Z",
      "endDate": "2023-10-28T12:00:00Z"
    }
    ```

    **Sample Response:**
    ```json
    {
       "ids": [
           "00QUPDATEDXXXXXX1",
           "00QUPDATEDXXXXXX2"
       ],
       "latestDateCovered": "2023-10-28T12:00:00.000+0000"
    }
    ```

    **Related Salesforce documentation:**
    [Get Updated Records](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_getupdated.htm)

### sObject Operations

??? note "salesforce.describeGlobal"
    The `salesforce.describeGlobal` operation retrieves a list of all sObjects available in your organization, along with some basic metadata for each.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.describeGlobal configKey="MySFConfig"/>
    ```

    **Sample Request (JSON payload for the proxy - no parameters needed):**
    ```json
    {}
    ```

    **Sample Response (snippet):**
    ```json
    {
       "encoding": "UTF-8",
       "maxBatchSize": 200,
       "sobjects": [
          {
             "name": "Account",
             "label": "Account",
             "keyPrefix": "001",
             "custom": false,
             "queryable": true,
             // ... other attributes like createable, updateable, deletable ...
             "urls": {
                "sobject": "/services/data/vXX.X/sobjects/Account",
                "describe": "/services/data/vXX.X/sobjects/Account/describe",
                "rowTemplate": "/services/data/vXX.X/sobjects/Account/{ID}"
             }
          },
          {
             "name": "MyCustomObject__c",
             "label": "My Custom Object",
             // ...
          }
          // ... more sObjects
       ]
    }
    ```

    **Related Salesforce documentation:**
    [Describe Global (List sObjects)](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_describeGlobal.htm)

??? note "salesforce.describeSObject"
    The `salesforce.describeSObject` operation retrieves detailed metadata for a specific sObject type, including its fields, record type information, child relationships, and URLs.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject to describe (e.g., <code>Account</code>, <code>MyCustomObject__c</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.describeSObject configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
    </salesforce.describeSObject>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Account"
    }
    ```

    **Sample Response (snippet):**
    ```json
    {
       "name": "Account",
       "label": "Account",
       "fields": [
          {"name": "Id", "type": "id", "label": "Account ID", /* ... */},
          {"name": "Name", "type": "string", "label": "Account Name", /* ... */},
          {"name": "Industry", "type": "picklist", "label": "Industry", /* ... */}
          // ... all other fields
       ],
       "childRelationships": [
          {"childSObject": "Contact", "fieldName": "AccountId", "relationshipName": "Contacts", /* ... */}
       ],
       "recordTypeInfos": [ /* ... */ ],
       "urls": { /* ... */ }
       // ... many other metadata attributes
    }
    ```

    **Related Salesforce documentation:**
    [Describe sObject](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_sobject_describe.htm)

??? note "salesforce.sObjectBasicInfo"
    The `salesforce.sObjectBasicInfo` operation retrieves basic metadata information for a specific sObject, such as its label, key prefix, and URLs, but without the detailed field list or child relationships provided by `describeSObject`.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.sObjectBasicInfo configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
    </salesforce.sObjectBasicInfo>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Lead"
    }
    ```

    **Sample Response:**
    ```json
    {
       "objectDescribe": {
          "name": "Lead",
          "label": "Lead",
          "keyPrefix": "00Q",
          "custom": false,
          "queryable": true,
          // ... other basic attributes
          "urls": {
             "compactLayouts": "/services/data/vXX.X/sobjects/Lead/describe/compactLayouts",
             "describe": "/services/data/vXX.X/sobjects/Lead/describe",
             "layouts": "/services/data/vXX.X/sobjects/Lead/describe/layouts",
             "sobject": "/services/data/vXX.X/sobjects/Lead",
             "rowTemplate":"/services/data/vXX.X/sobjects/Lead/{ID}"
          }
       },
       "recentItems": [ /* ... list of recently viewed records for this sObject type ... */ ]
    }
    ```

    **Related Salesforce documentation:**
    [sObject Basic Information](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_sobject_basic_info.htm)

??? note "salesforce.getSObjectRows"
    The `salesforce.getSObjectRows` operation retrieves a specific record by its ID for a specified sObject type. This is functionally similar to `getRecord` in `records.md` but refers to the more generic sObject row retrieval endpoint.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>recordId</td>
            <td>The ID of the record (row) to retrieve.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>fields</td>
            <td>Optional. A comma-separated list of field API names to retrieve.</td>
            <td>No</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.getSObjectRows configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <recordId>{$ctx:recordId}</recordId>
        <fields>{$ctx:fields}</fields> <!-- Optional -->
    </salesforce.getSObjectRows>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Case",
      "recordId": "500XXXXXXXXXXXXXXX",
      "fields": "CaseNumber,Subject,Status,Priority"
    }
    ```

    **Sample Response:**
    ```json
    {
        "attributes": {
            "type": "Case",
            "url": "/services/data/vXX.X/sobjects/Case/500XXXXXXXXXXXXXXX"
        },
        "Id": "500XXXXXXXXXXXXXXX", // Though Id is usually not requested explicitly with fields, it's part of the record
        "CaseNumber": "00001023",
        "Subject": "Issue with login",
        "Status": "New",
        "Priority": "High"
    }
    ```

    **Related Salesforce documentation:**
    [Retrieve sObject Rows (Records)](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_sobject_retrieve.htm)

??? note "salesforce.listAvailableApiVersions"
    The `salesforce.listAvailableApiVersions` operation retrieves a list of summary information about each REST API version currently available in the Salesforce instance.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.listAvailableApiVersions configKey="MySFConfig"/>
    ```

    **Sample Request (JSON payload for the proxy - no parameters needed):**
    ```json
    {}
    ```

    **Sample Response:**
    ```json
    [
        {"label": "Winter '23", "url": "/services/data/v56.0", "version": "56.0"},
        {"label": "Spring '23", "url": "/services/data/v57.0", "version": "57.0"},
        {"label": "Summer '23", "url": "/services/data/v58.0", "version": "58.0"}
        // ... other available versions
    ]
    ```
    (The original sample `{"output":"[...]"}` was corrected to be a valid JSON array.)

    **Related Salesforce documentation:**
    [List Available API Versions](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_versions.htm)

??? note "salesforce.listOrganizationLimits"
    The `salesforce.listOrganizationLimits` operation retrieves various limits information for your Salesforce organization, such as daily API request limits, data storage limits, etc.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.listOrganizationLimits configKey="MySFConfig"/>
    ```

    **Sample Request (JSON payload for the proxy - no parameters needed):**
    ```json
    {}
    ```

    **Sample Response (snippet):**
    ```json
    {
       "DailyApiRequests": {"Max": 100000, "Remaining": 98500},
       "DataStorageMB": {"Max": 10240, "Remaining": 8000},
       "FileStorageMB": {"Max": 20480, "Remaining": 15000}
       // ... many other limits
    }
    ```

    **Related Salesforce documentation:**
    [Organization Limits](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_limits.htm) (The old link `dome_limits.htm` is correct)

??? note "salesforce.listResourcesByApiVersion"
    The `salesforce.listResourcesByApiVersion` operation retrieves a list of all available REST API resources for the API version specified in the connection configuration (e.g., `v59.0`).

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details. The API version from this configuration will be used.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.listResourcesByApiVersion configKey="MySFConfig"/>
    ```

    **Sample Request (JSON payload for the proxy - no parameters needed):**
    ```json
    {}
    ```

    **Sample Response (snippet):**
    ```json
    {
       "sobjects": "/services/data/vXX.X/sobjects",
       "connect": "/services/data/vXX.X/connect",
       "query": "/services/data/vXX.X/query",
       "chatter": "/services/data/vXX.X/chatter",
       "limits": "/services/data/vXX.X/limits"
       // ... many other resources
    }
    ```

    **Related Salesforce documentation:**
    [List Resources for API Version](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_discoveryresource.htm) (The old link `dome_discoveryresource.htm` is correct)

??? note "salesforce.sObjectPlatformActionInfo"
    The `salesforce.sObjectPlatformActionInfo` operation retrieves metadata about Platform Actions, which are a way to expose actions, such as Lightning components or flows, via the API.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <!-- Add sObjectName if this can be specific to an sObject, otherwise it's global -->
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.sObjectPlatformActionInfo configKey="MySFConfig"/>
    ```

    **Sample Request (JSON payload for the proxy - no parameters needed usually):**
    ```json
    {}
    ```

    **Sample Response (describing the PlatformAction sObject itself):**
    ```json
    {
       "objectDescribe": {
          "name": "PlatformAction",
          "label": "Platform Action",
          "keyPrefix": "0JV", // Example key prefix
          "custom": false,
          "queryable": true,
          // ... other describe attributes for the PlatformAction sObject
          "urls": {
             "rowTemplate": "/services/data/vXX.X/sobjects/PlatformAction/{ID}",
             "describe": "/services/data/vXX.X/sobjects/PlatformAction/describe",
             "sobject": "/services/data/vXX.X/sobjects/PlatformAction"
          }
       },
       "recentItems": [] // Recent PlatformAction records, if applicable
    }
    ```

    **Related Salesforce documentation:**
    [Platform Action Resource](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_sobject_platformaction.htm)

### Search Operations

??? note "salesforce.search"
    The `salesforce.search` operation executes a SOSL query to search for records across multiple sObject types based on a text string.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>searchString</td>
            <td>The SOSL query string (e.g., <code>FIND {searchTerm} IN ALL FIELDS RETURNING Account(Name), Contact(FirstName,LastName)</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.search configKey="MySFConfig">
        <searchString>{$ctx:searchString}</searchString>
    </salesforce.search>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "searchString": "FIND {Universal Containers} IN NAME FIELDS RETURNING Account(Id, Name, Industry), Contact(Id, Name, Email)"
    }
    ```

    **Sample Response:**
    A successful SOSL query returns a list of matching sObject records.
    ```json
    {
      "searchRecords": [
        {
          "attributes": {"type": "Account", "url": "/services/data/vXX.X/sobjects/Account/001XXXXXXXXXXXXXXX"},
          "Id": "001XXXXXXXXXXXXXXX",
          "Name": "Universal Containers",
          "Industry": "Manufacturing"
        },
        {
          "attributes": {"type": "Contact", "url": "/services/data/vXX.X/sobjects/Contact/003YYYYYYYYYYYYYYY"},
          "Id": "003YYYYYYYYYYYYYYY",
          "Name": "John Doe",
          "Email": "john.doe@universalcontainers.com"
        }
        // ... other matching records
      ]
    }
    ```
    (The original sample `{"output":"[...]"}` was corrected to be a valid JSON structure; actual SOSL responses are typically a direct array `searchRecords` if the query is successful and returns results, or an empty array `[]` if no results.)

    **Related Salesforce documentation:**
    [Search (SOSL)](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_search.htm)

??? note "salesforce.searchScopeAndOrder"
    The `salesforce.searchScopeAndOrder` operation retrieves the search scope (which sObjects are searched) and display order for the current user.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.searchScopeAndOrder configKey="MySFConfig"/>
    ```

    **Sample Request (JSON payload for the proxy - no parameters needed):**
    ```json
    {}
    ```

    **Sample Response:**
    ```json
    [
        {"name": "Account", "label": "Accounts"},
        {"name": "Contact", "label": "Contacts"},
        {"name": "Opportunity", "label": "Opportunities"}
        // ... other sObjects in the user's search scope and order
    ]
    ```
    (The original sample `{"output":"[]"}` was corrected. The actual response is an array of objects, each describing an sObject in the search scope.)

    **Related Salesforce documentation:**
    [Search Scope and Order](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_search_scope_order.htm)

??? note "salesforce.searchResultLayout"
    The `salesforce.searchResultLayout` operation retrieves the search result layouts (which fields are displayed in search results) for one or more specified sObjects.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectNameList</td>
            <td>A comma-separated list of sObject API names for which to retrieve search result layouts (e.g., <code>Account,Contact,Lead</code>).</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.searchResultLayout configKey="MySFConfig">
        <sObjectNameList>{$ctx:sObjectNameList}</sObjectNameList>
    </salesforce.searchResultLayout>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectNameList": "Account,Opportunity"
    }
    ```

    **Sample Response:**
    ```json
    [
        {
            "label": "Account Search Results", // Label for the layout
            "limitRows": 25,
            "objectType": "Account",
            "searchColumns": [
                {"field": "Account.Name", "label": "Account Name", "name": "Name"},
                {"field": "Account.Phone", "label": "Phone", "name": "Phone"},
                {"field": "Account.OwnerId", "label": "Account Owner", "name": "OwnerId"}
            ]
        },
        {
            "label": "Opportunity Search Results",
            "objectType": "Opportunity",
            "searchColumns": [ /* ... columns for Opportunity ... */ ]
        }
    ]
    ```
    (The original sample `{"output":"[...]"}` was corrected.)

    **Related Salesforce documentation:**
    [Search Result Layouts](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_retrieve_search_layouts.htm)

??? note "salesforce.searchSuggestedRecords"
    The `salesforce.searchSuggestedRecords` operation returns a list of suggested records whose names match the user’s partial search string, useful for type-ahead functionality.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>sObjectName</td>
            <td>The API name of the sObject to search within (e.g., <code>Account</code>, <code>Contact</code>).</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>stringForSearch</td>
            <td>The partial text string to search for in record names.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.searchSuggestedRecords configKey="MySFConfig">
        <sObjectName>{$ctx:sObjectName}</sObjectName>
        <stringForSearch>{$ctx:stringForSearch}</stringForSearch>
    </salesforce.searchSuggestedRecords>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "sObjectName": "Account",
      "stringForSearch": "Univer"
    }
    ```

    **Sample Response:**
    ```json
    {
      "autoSuggestResults": [
        {
          "attributes": {"type": "Account", "url": "/services/data/vXX.X/sobjects/Account/001XXXXXXXXXXXXXXX"},
          "Id": "001XXXXXXXXXXXXXXX",
          "Name": "Universal Containers"
        },
        {
          "attributes": {"type": "Account", "url": "/services/data/vXX.X/sobjects/Account/001YYYYYYYYYYYYYYY"},
          "Id": "001YYYYYYYYYYYYYYY",
          "Name": "University of Arizona"
        }
      ],
      "hasMoreResults": false // Indicates if there are more suggestions than returned
    }
    ```

    **Related Salesforce documentation:**
    [Search Suggested Records](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_search_suggest_records.htm)

### User Operations

??? note "salesforce.getUserInformation"
    The `salesforce.getUserInformation` operation retrieves information about a specific user by their User ID. This is typically equivalent to retrieving a User sObject record.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>userId</td>
            <td>The ID of the user whose information you want to retrieve.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>fields</td>
            <td>Optional. A comma-separated list of field API names from the User object to retrieve (e.g., <code>Name,Email,Profile.Name,IsActive</code>). If not specified, Salesforce returns a default set of fields.</td>
            <td>No</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.getUserInformation configKey="MySFConfig">
        <userId>{$ctx:userId}</userId>
        <fields>Id,Name,Email,Profile.Name,IsActive,LastLoginDate</fields> <!-- Example fields -->
    </salesforce.getUserInformation>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "userId": "005XXXXXXXXXXXXXXX"
      // "fields": "Id,Name,Email" // Optionally pass fields in payload if proxy is designed for it
    }
    ```

    **Sample Response:**
    ```json
    {
       "attributes": {"type": "User", "url": "/services/data/vXX.X/sobjects/User/005XXXXXXXXXXXXXXX"},
       "Id": "005XXXXXXXXXXXXXXX",
       "Name": "Jane Doe",
       "Email": "jane.doe@example.com",
       "ProfileId": "00eYYYYYYYYYYYYYYY",
       "IsActive": true,
       "LastLoginDate": "2023-10-27T10:30:00.000+0000",
       "Profile": {
           "attributes": {"type": "Profile", "url": "/services/data/vXX.X/sobjects/Profile/00eYYYYYYYYYYYYYYY"},
           "Name": "Standard User"
       }
       // ... other fields as requested or default set
    }
    ```

    **Related Salesforce documentation:**
    [User sObject](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_user.htm) (General User object reference)
    [Retrieve Records](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_retrieve_specific_fields.htm) (General record retrieval)

??? note "salesforce.resetPassword"
    The `salesforce.resetPassword` operation initiates the password reset process for a specified user. Salesforce typically sends an email to the user with instructions to set a new password.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>userId</td>
            <td>The ID of the user whose password needs to be reset.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.resetPassword configKey="MySFConfig">
        <userId>{$ctx:userId}</userId>
    </salesforce.resetPassword>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "userId": "005XXXXXXXXXXXXXXX"
    }
    ```
    This operation typically returns an HTTP 204 No Content status on success if it just initiates the reset flow. The previous sample response `{"NewPassword" : "myNewPassword1234"}` is for `setPassword` or if the API directly returns a temporary password, which is less common for a "reset" flow that involves user interaction. Salesforce's `UserManagement.initiatePasswordReset()` Apex method, for instance, just sends an email. If the API directly provides a new password, the response should reflect that. For now, assuming standard reset flow.

    **Sample Response (If API directly returns a new password, which is rare for a "reset" operation):**
    ```json
    {
        "newPassword": "aGeneratedPassword"
    }
    ```
    More commonly, a successful initiation of password reset by email would return HTTP 200 OK or 204 No Content with no body or a simple success message.

    **Related Salesforce documentation:**
    [User Password Management (Reset/Set)](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_sobject_user_password.htm)

??? note "salesforce.setPassword"
    The `salesforce.setPassword` operation sets a specific password for a user. This is typically an administrative action.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>userId</td>
            <td>The ID of the user for whom the password is being set.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>newPassword</td>
            <td>The new password to set for the user. Must comply with the organization's password policies.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.setPassword configKey="MySFConfig">
        <userId>{$ctx:userId}</userId>
        <newPassword>{$ctx:newPassword}</newPassword> <!-- Changed from fieldAndValue for clarity -->
    </salesforce.setPassword>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
      "userId": "005XXXXXXXXXXXXXXX",
      "newPassword": "NewComplexPassword123!"
    }
    ```
    Salesforce responds with an HTTP 204 No Content status on successful password set.

    **Related Salesforce documentation:**
    [User Password Management (Reset/Set)](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_sobject_user_password.htm)

### Report Operations

??? note "salesforce.getReportMetadata"
    The `salesforce.getReportMetadata` operation retrieves metadata for a specific report, such as its columns, groupings, and filters.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>reportId</td>
            <td>The ID of the report whose metadata you want to retrieve.</td>
            <td>Yes</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.getReportMetadata configKey="MySFConfig">
        <reportId>{$ctx:reportId}</reportId>
    </salesforce.getReportMetadata>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
        "reportId": "00O8d000004MWaGEAW"
    }
    ```

    **Sample Response:**
    ```json
    {
        "attributes": {"type": "Report", "url": "/services/data/vXX.X/analytics/reports/00O8d000004MWaGEAW"},
        "id": "00O8d000004MWaGEAW",
        "name": "Sales Key Metrics Q3",
        "developerName": "Sales_Key_Metrics_Q3",
        "folderId": "00lXXXXXXXXXXXXXXX",
        "reportMetadata": {
            "id": "00O8d000004MWaGEAW",
            "name": "Sales Key Metrics Q3",
            "developerName": "Sales_Key_Metrics_Q3",
            "aggregates": ["RowCount"],
            "detailColumns": ["ACCOUNT.NAME", "OPPORTUNITY.NAME", "AMOUNT"],
            "groupingsDown": [],
            "groupingsAcross": [],
            "reportFilters": [
                {"column": "FISCAL_QUARTER", "operator": "equals", "value": "THIS_FISCAL_QUARTER"}
            ]
            // ... and much more metadata
        },
        "reportTypeMetadata": { /* ... */ }
    }
    ```
    **Related Salesforce documentation:**
    [Get Report Metadata](https://developer.salesforce.com/docs/atlas.en-us.api_analytics.meta/api_analytics/analytics_api_reports_reportmetadata_example_get.htm)

??? note "salesforce.executeReport"
    The `salesforce.executeReport` operation executes a report. Reports can be run synchronously or asynchronously depending on their complexity and data volume. This example assumes a synchronous execution for simplicity. For large reports, asynchronous execution is recommended.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>reportId</td>
            <td>The ID of the report to execute.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>includeDetails</td>
            <td>Set to `true` to get detailed row data. `false` for summary data only. Defaults to `true`.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>reportFilters</td>
            <td>Optional. A JSON array of filter objects to apply to the report execution, overriding existing filters. Each filter object contains `column`, `operator`, and `value`.
            Example: `[{"column":"STAGE","operator":"equals","value":"Closed Won"}]`</td>
            <td>No</td>
        </tr>
    </table>

    **Sample XML Configuration (Synchronous):**
    ```xml
    <salesforce.executeReport configKey="MySFConfig">
        <reportId>{$ctx:reportId}</reportId>
        <includeDetails>true</includeDetails>
        <!-- <reportFilters>[{"column":"AMOUNT","operator":"greaterThan","value":"50000"}]</reportFilters> -->
    </salesforce.executeReport>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
        "reportId": "00O8d000004MWaGEAW",
        "includeDetails": true,
        "reportFilters": [
            {"column": "OPPORTUNITY.TYPE", "operator": "equals", "value": "New Business"}
        ]
    }
    ```

    **Sample Response (Simplified tabular structure):**
    ```json
    {
        "reportMetadata": { /* ... metadata ... */ },
        "factMap": {
            "T!T": { // Total records
                "aggregates": [{"label": "Sum of Amount", "value": 1250000.00}, {"label": "Record Count", "value": 15}],
                "rows": [ // if includeDetails is true
                    {"dataCells": [{"label": "WSO2", "value": "WSO2"}, {"label": "Large Deal", "value": "Large Deal"}, {"label": "100000.00", "value": 100000.00}]},
                    {"dataCells": [{"label": "ACME Corp", "value": "ACME Corp"}, {"label": "Medium Deal", "value": "Medium Deal"}, {"label": "50000.00", "value": 50000.00}]}
                    // ... more rows
                ]
            }
            // ... other groupings if present ...
        },
        "groupingsDown": { /* ... */ },
        "groupingsAcross": { /* ... */ },
        "hasDetailRows": true
    }
    ```
    **Related Salesforce documentation:**
    [Execute a Report Synchronously](https://developer.salesforce.com/docs/atlas.en-us.api_analytics.meta/api_analytics/analytics_api_reports_reportdata_sync_get_example.htm)
    [Execute a Report Asynchronously](https://developer.salesforce.com/docs/atlas.en-us.api_analytics.meta/api_analytics/analytics_api_reports_reportdata_async_post_example.htm)

??? note "salesforce.listReports"
    The `salesforce.listReports` operation retrieves a list of recently viewed reports or all reports accessible to the user.

    **Parameters:**
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>Salesforce Configuration Name</td>
            <td>The <code>salesforce.config.name</code> of the Salesforce configuration local entry (e.g., <code>MySFConfig</code>) containing connection details.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>scope</td>
            <td>Optional. Scope of reports to list. E.g., `RecentlyViewed` (default), `All`.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>pageSize</td>
            <td>Optional. Number of items to return per page.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>page</td>
            <td>Optional. Page number to retrieve.</td>
            <td>No</td>
        </tr>
    </table>

    **Sample XML Configuration:**
    ```xml
    <salesforce.listReports configKey="MySFConfig">
        <scope>All</scope>
        <pageSize>10</pageSize>
    </salesforce.listReports>
    ```

    **Sample Request (JSON payload for the proxy):**
    ```json
    {
        "scope": "RecentlyViewed",
        "pageSize": 5
    }
    ```

    **Sample Response:**
    ```json
    {
        "reports": [
            {
                "id": "00O8d000004MWaGEAW",
                "name": "Sales Key Metrics Q3",
                "url": "/services/data/vXX.X/analytics/reports/00O8d000004MWaGEAW",
                "describeUrl": "/services/data/vXX.X/analytics/reports/00O8d000004MWaGEAW/describe",
                "instancesUrl": "/services/data/vXX.X/analytics/reports/00O8d000004MWaGEAW/instances"
            }
            // ... other reports
        ],
        "nextPageUrl": "/services/data/vXX.X/analytics/reports?scope=All&page=2&pageSize=10", // if paginated
        "currentPageUrl": "/services/data/vXX.X/analytics/reports?scope=All&page=1&pageSize=10"
    }
    ```
    **Related Salesforce documentation:**
    [Report List](https://developer.salesforce.com/docs/atlas.en-us.api_analytics.meta/api_analytics/analytics_api_reports_list_get_example.htm)

### Fault Handler Sequence

This section provides a sample proxy service and a fault handler sequence (`faultHandlerSeq`) that you can use as a starting point for handling faults when integrating with Salesforce. You can customize this sample based on your specific error handling requirements.

**Sample Proxy Service with In-line Fault Handling Logic**

The following sample proxy demonstrates how to invoke a Salesforce operation and then check the HTTP status code (`$axis2:HTTP_SC`) to determine if an error occurred. If an error is detected (typically any status code not in the 2xx range), properties for `ERROR_CODE` and `ERROR_MESSAGE` are set, and then a common `faultHandlerSeq` is invoked.

```xml
<proxy xmlns="http://ws.apache.org/ns/synapse" name="Salesforce_SampleProxy" transports="https,http" statistics="disable" trace="disable" startOnLoad="true">
  <target>
    <inSequence onError="faultHandlerSeq"> <!-- General error catcher -->

      <!-- 1. Invoke a Salesforce Connector Operation -->
      <!-- Replace with your actual Salesforce operation call -->
      <!-- Example: Querying accounts -->
      <salesforce.query configKey="MySFConfig">
        <queryString>SELECT Id, Name FROM Account LIMIT 5</queryString>
      </salesforce.query>

      <!-- 2. Check HTTP Status Code after the operation call -->
      <filter source="$axis2:HTTP_SC" regex="^[^2][0-9][0-9]"> <!-- Checks if status is not 2xx -->
            <then>
               <log level="custom">
                  <property name="STATUS" expression="$axis2:HTTP_SC"/>
                  <property name="MESSAGE" value="An error occurred while invoking Salesforce operation."/>
               </log>
               <switch source="$axis2:HTTP_SC">
                  <case regex="401"> <!-- Unauthorized -->
                     <property name="ERROR_CODE" value="SF_AUTH_ERROR"/>
                     <property name="ERROR_MESSAGE" value="Salesforce authentication failed. Check credentials and token."/>
                  </case>
                  <case regex="400"> <!-- Bad Request -->
                     <property name="ERROR_CODE" value="SF_BAD_REQUEST"/>
                     <property name="ERROR_MESSAGE" expression="fn:concat('Salesforce API Bad Request: ', synapse:get-payload())"/>
                  </case>
                  <case regex="403"> <!-- Forbidden -->
                     <property name="ERROR_CODE" value="SF_FORBIDDEN"/>
                     <property name="ERROR_MESSAGE" value="Access to the requested Salesforce resource is forbidden."/>
                  </case>
                  <case regex="404"> <!-- Not Found -->
                     <property name="ERROR_CODE" value="SF_NOT_FOUND"/>
                     <property name="ERROR_MESSAGE" value="The requested Salesforce resource was not found."/>
                  </case>
                  <!-- Add other Salesforce-specific error codes as needed -->
                  <!-- e.g., 422 for Unprocessable Entity (validation errors) -->
                  <case regex="422">
                     <property name="ERROR_CODE" value="SF_UNPROCESSABLE_ENTITY"/>
                     <property name="ERROR_MESSAGE" expression="fn:concat('Salesforce Unprocessable Entity: ', synapse:get-payload())"/>
                  </case>
                  <case regex="500"> <!-- Internal Server Error (from Salesforce) -->
                     <property name="ERROR_CODE" value="SF_SERVER_ERROR"/>
                     <property name="ERROR_MESSAGE" value="Salesforce internal server error."/>
                  </case>
                  <default> <!-- Generic error based on HTTP status -->
                     <property name="ERROR_CODE" expression="fn:concat('HTTP_', $axis2:HTTP_SC)"/>
                     <property name="ERROR_MESSAGE" expression="fn:concat('An unexpected error occurred. HTTP Status: ', $axis2:HTTP_SC, ' Payload: ', synapse:get-payload())"/>
                  </default>
               </switch>
               <!-- Invoke the common fault sequence -->
               <sequence key="faultHandlerSeq" />
            </then>
            <else>
                <!-- Successful operation (2xx response) -->
                <log level="custom">
                    <property name="STATUS" expression="$axis2:HTTP_SC"/>
                    <property name="MESSAGE" value="Salesforce operation successful."/>
                </log>
                <respond/> <!-- Send the successful response back to the client -->
            </else>
      </filter>
    </inSequence>
    <outSequence>
      <!-- The respond mediator in the inSequence's 'else' block handles successful responses.
           If you need further processing for successful responses, add it here.
           Otherwise, an empty send can be used or this outSequence can be omitted if not needed. -->
      <send/>
    </outSequence>
    <faultSequence>
        <!-- This faultSequence is a global fallback for unhandled errors in inSequence -->
        <log level="full" category="ERROR">
            <property name="MESSAGE" value="**GLOBAL FAULT SEQUENCE TRIGGERED**"/>
            <property name="ERROR_CODE" expression="$ctx:ERROR_CODE"/>
            <property name="ERROR_MESSAGE" expression="$ctx:ERROR_MESSAGE"/>
            <property name="ERROR_DETAIL" expression="$ctx:ERROR_DETAIL"/>
            <property name="ERROR_EXCEPTION" expression="$ctx:ERROR_EXCEPTION"/>
        </log>
        <!-- Optionally, call the custom faultHandlerSeq here as well -->
        <sequence key="faultHandlerSeq"/>
    </faultSequence>
  </target>
</proxy>
```

**Common `faultHandlerSeq` Sequence**

This sequence formats the error response sent back to the client. It checks the `Content-Type` of the original request (or what's expected by the client) and formats the error payload as JSON or XML accordingly.

```xml
<sequence xmlns="http://ws.apache.org/ns/synapse" name="faultHandlerSeq">
    <property name="HTTP_SC" value="500" scope="axis2"/> <!-- Default to 500 Internal Server Error if not set by specific cases -->
    <property name="ERROR_CODE" expression="get-property('ERROR_CODE')" scope="default" type="STRING"
              description="Ensure ERROR_CODE is set before calling this sequence"/>
    <property name="ERROR_MESSAGE" expression="get-property('ERROR_MESSAGE')" scope="default" type="STRING"
              description="Ensure ERROR_MESSAGE is set before calling this sequence"/>

    <!-- Log the error -->
    <log level="custom" category="ERROR">
        <property name="FaultHandler" value="faultHandlerSeq"/>
        <property name="ErrorCode" expression="get-property('ERROR_CODE')"/>
        <property name="ErrorMessage" expression="get-property('ERROR_MESSAGE')"/>
        <property name="OriginalPayload" expression="synapse:get-payload()"/> <!-- Log original error payload from Salesforce if any -->
    </log>

    <!-- Determine response Content-Type; default to JSON if not specified -->
    <property name="contentTypeValue" expression="get-property('transport', 'Content-Type')" scope="default" type="STRING"/>
    <filter source="boolean(get-property('contentTypeValue'))" regex="false">
        <then>
            <property name="contentTypeValue" value="application/json"/>
        </then>
    </filter>

    <filter xpath="contains(get-property('contentTypeValue'), 'application/json')">
        <then>
            <payloadFactory media-type="json">
                <format>
                    {
                        "error": {
                            "code": "$1",
                            "message": "$2"
                        }
                    }
                </format>
                <args>
                    <arg expression="get-property('ERROR_CODE')" evaluator="xml"/>
                    <arg expression="get-property('ERROR_MESSAGE')" evaluator="xml"/>
                </args>
            </payloadFactory>
            <property name="messageType" value="application/json" scope="axis2"/>
        </then>
        <else> <!-- Default to XML if not JSON -->
            <payloadFactory media-type="xml">
                <format>
                    <error_info xmlns="">
                        <error_code>$1</error_code>
                        <error_message>$2</error_message>
                    </error_info>
                </format>
                <args>
                    <arg expression="get-property('ERROR_CODE')" evaluator="xml"/>
                    <arg expression="get-property('ERROR_MESSAGE')" evaluator="xml"/>
                </args>
            </payloadFactory>
            <property name="messageType" value="application/xml" scope="axis2"/>
        </else>
    </filter>
    <respond/> <!-- Send the formatted error response -->
</sequence>
```

**Key considerations for the `faultHandlerSeq`:**
*   **Error Codes and Messages**: The `ERROR_CODE` and `ERROR_MESSAGE` properties should be set appropriately in the main sequence (or the proxy's `inSequence`) before calling `faultHandlerSeq`.
*   **Content-Type**: The sequence attempts to respond in the same content type as the request (`application/json` or `application/xml`).
*   **HTTP Status Code**: Ensure the desired HTTP status code (e.g., 400, 401, 500) is set on the `axis2` scope using `<property name="HTTP_SC" value="500" scope="axis2"/>` before the final `respond` mediator in the fault sequence if you want to override the default. The example above sets it to 500.
*   **Logging**: It's crucial to log detailed error information for debugging and monitoring.

This setup provides a robust way to catch errors from Salesforce operations and return standardized error messages to the client. Remember to adapt the specific error codes and messages to match the semantics of your integration scenario.
